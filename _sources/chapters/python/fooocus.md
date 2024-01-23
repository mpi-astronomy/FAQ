# Image Generation with Stable Diffusion and Fooocus

Image generation tools are now available to anyone using open source tools and consumer grade hardware. In this note I will detail how to install [Fooocus](https://github.com/lllyasviel/Fooocus), an frontend built on [Gradio](https://www.gradio.app/) that can take advantage of Stability AI's Stable Diffusion ([SD](https://stability.ai/stable-diffusion)) model checkpoints. These checkpoints have already been trained (and in some cases, fine-tuned) making them ideal for quick image generation for a wide array of use cases. 

:::{note}
In order to generate images on reasonable time scales (e.g. less than a minute) it is necessary to have a decently powerful stand-alone GPU.
:::

## Installing Fooocus

The [Fooocus](https://github.com/lllyasviel/Fooocus) installation procedures are relatively straightforward for Linux, Windows, and macOS, including systems with either AMD or NVIDIA GPUs. In this guide I will focus on the installation of Fooocus on the MPIA Astro GPU Nodes which are equipped with enterprise GPUs that will be more than up to the task of processing our images. However, due to the software available on the nodes, the installation procedure requires a slight deviation from what's provided directly from Fooocus. 

Let's begin by logging into the node of our choice. In this example we will log in to astro-gpu-node1. Let's open an SSH connection and print out the GPU information (for NVIDIA GPUs). 

```bash
ssh user@astro-gpu-node1
nvidia-smi
```

```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.43.04    Driver Version: 515.43.04    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Quadro RTX 6000     On   | 00000000:3B:00.0 Off |                    0 |
| N/A   30C    P0    55W / 250W |   2863MiB / 23040MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  Quadro RTX 6000     On   | 00000000:D8:00.0 Off |                    0 |
| N/A   33C    P0    55W / 250W |   2053MiB / 23040MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```

```{important} 
We need to note the CUDA version listed here for following installation steps.
```

```{note}
This view also allows us to see what the GPU usage is. Of course, the less utilization, the faster our model will run. This is makes `nvidia-smi` a quick and easy way to check the current GPU utilization on the `astro-gpu-node` servers. 
```

We are going to follow the default Fooocus installation instructions with a slight modification to account for the outdated CUDA version available on the GPU nodes. We'll be loading the native Anaconda module on the astro-nodes to install the software. 

```bash
module purge # Optional, gets rid of any previously loaded modules
module load anaconda3-py3.10
git clone https://github.com/lllyasviel/Fooocus.git
cd Fooocus
conda env create -f environment.yaml
conda activate fooocus
```

We can now follow the instructions for [installing older versions of PyTorch](https://pytorch.org/get-started/previous-versions/) (our acceleration framework) to be compatible with our version of CUDA. Here I am following the instructions for CUDA 11.7 as this is the version available on the astro-gpu-node at the time of writing.

```bash
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.7 -c pytorch -c nvidia
pip install -r requirements_versions.txt
```

And there we are! That should be it for installation. 

## Starting Fooocus

Let's begin by activating the environment and running the main script. The first thing that will happen is a Stable Diffusion XL model checkpoint will have to be downloaded. These can several gigabytes in size so may take some time. 

```bash
conda activate fooocus
python entry_with_update.py
```

While the code is initalizing, a web browser might pop up on your local machine over an X-server. Feel free to close it, as we're going to be using our local web-browser than than the [KDE default](https://apps.kde.org/konqueror/) which will allow us to properly load the app. We'll know the model is ready to run once we've seen the output:


```text
App started successful. Use the app with http://127.0.0.1:XXXX/ or 127.0.0.1:XXXX
```

```{important} 
We will need to remember the port that the server is running on (i.e. the numbers in the `XXXX` spot above). 
```

The Fooocus/Gradio interface is a web app built on [Svelt](https://svelte.dev/). Therefore, in order to interact with the code, we're going to need to forward the traffic to our local machine. We can select any port on our local machine, which we'll label as `YYYY`. In a new terminal we can run the following:

```bash
ssh -L YYYY:127.0.0.1:XXXX user@astro-gpu-node1
```

In general, I just set use whatever port is used by the remote server. As the default port for Fooocus is `7865` I forward this `7865` on our local machine:

```bash
ssh -L 7865:127.0.0.1:7865 user@astro-gpu-node1
```

By leaving these two terminals open, one to run the server, and one to forward the web traffic, we can now open Fooocus on our local machine and start generating images.

## Generating Images

We can now open our web browser of choice, for me it's [Firefox](https://www.mozilla.org/en-US/firefox/new/), and navigate to the Fooocus web application by navigating to `http://localhost:YYYY/`, or in my case `http://localhost:7865/`. If an empty image appears with a text box beneath it, then the Fooocus application has launched correctly! 

Generating an image is now as simple as typing any prompt and hitting generate! We can watch the output logs in our original terminal session. The default settings will produce two images from our prompt. 
If the GPUs are not being used by other users, we should expect about 30-45s per image.
While the Fooocus documentation provides a description of the different options, I intend to provide a short introduction to the most important configurations we can tweak in the UI. 
If you are familiar with Midjourney, one of the more popular image generation services, I recommend reading the Fooocus documentation section on transitioning between the two.

### The Advanced Tab
By clicking the advanced checkbox at the bottom of the page, we can open the a panel whioch provides us with the fine grained control of our image generation process and consists of the following sections, each of which provides increasingly detailed control:
- Setting:
    - Performance: Enables balancing of speed versus quality of output image.
    - Aspect Ratios: Controls the output resolution of images (output images may still be upscaled using Fooocus).
    - Image Number: Number of images generated.
    - Negative Prompt: In contrast to the image prompt, the negative prompt enables us to describe what we do not want to see in our image.
    - Random: By de-selecting random we can force our RNG seed.
- Style: These are predefine prompt modifiers that have been tested with SDXL. In essence, these act on your prompts (and negative prompts) to modify your language in order to try to produce an output of a certain aesthetic quality. Checking a few of these can affect the look of your final image. Fooocus will select a few defaults, but play around by combining some of your favorite modifiers.
- Model: Here we can incorporate different SDXL model checkpoints which can be combined along with smaller "LoRA" models (and their corresponding weights). The default model should be enough for most cases, but see the section at the end of this guide if you are interested in adding additional models. 
- Advanced:
    - Guidance Scale: Details how strictly should the input image adhere to your prompt. Lower values give us more "creative" but more unexpected results. 
    - Sharpness: Details if textures should be fuzzier or sharper in the resultant image.

### Input Images

One of the most powerful features of Stable Diffusion is not just generation from prompts, but from input images. By clicking the Input Image selection box, we can now edit original images (or AI generated images) in a few specificy ways:
- Upscale or Variation: Here we can either upscale (e.g. improve the resolution of) or vary (e.g. modify with prompt) our input image. Selecting disabled will ignore the input image. Similarly, selected upscale will ignore the input text prompt. 
- Image Prompt: Using images as prompts, we can combine input images, or even place objects in the images in our scenes. This is fun to play around with, especially with the advanced settings turned on. For some more practical examples and discussion, see this [Fooocus announcement](https://github.com/lllyasviel/Fooocus/discussions/557).
- Input or Outpaint: These are powerful methods describing how to use AI to add and remove modify inside (inpaint) or generate content outside (outpaint) your image boundaries. In the top right of the image the brush size of the cursor can be modified, along with an undo tool and a tool to erase the current highlighted portion.
    - Inpaint or Outpaint: Selected the four directions will control which directions are "outpainted" in the resultant image. In addition, you can use your cursor to highlight portions in the image will be "inpainted". Both rely on the input text prompt. 
    - Improve Detail (face, hand, eyes, etc.): Let's face it, AI generated images sometimes have some glaring issues, especially with hands and facial features. These can be addressed by highlighting these areas using the cursor and describing what should be improved. 
    - Modify Content (add objects, change background, etc.): Here we can do some more specific kinds of inpainting to add features to our image. I haven't played around with it enough to exactly know how it varies or what it is better suited for. 

With all of these controls under your belt, you should be well on your way to producing your AI generated images with Stable Diffusion XL and Fooocus!

## Extra: Adding a new Model

One of the most exciting parts of image generation from Stable Diffusion XL checkpoints is the ability to start from _any_ SDXL checkpoint, not just the defaults provided here. 
In fact, Fooocus ships with two additional default models, one designed for photorealism and the other for anime-style images. 
If you run `entry_with_update.py` with the `--preset` flag set as `realistic` or `anime`, *both* additional models will be downloaded. 
Either of the three default models can then be selected in the Advanced settings tab. 

Additional models can be downloaded from the internet.
Fooocus currently supports the following types of models:
- The base model must always be an SDXL model. 
- The output of the SDXL model can be used as input to a secondary model, also known as the refiner. The refiner can either be an SDXL or an SD1.5 model (At least according to the documentation, Foocus may support other refiners between 1.5 and XL, but I haven't done extensive testing.).
- Low-Rank Adaptations or [LoRAs](https://aituts.com/stable-diffusion-lora/) are additional smaller models than can be combined with the base model to add additional concepts to the model. Fooocus can support up to four additional LoRAs which can broadly be separated into two categories:
    - Subjects which are characters, expressions, or even objects to be incorporated in the scene.  
    - Styles can include aesthetics, and, for want of a better word, styles, to be incorporated into the output.

Checkpoints (e.g. SDXL or SD1.5 models) should be placed in the `Fooocus/models/checkpoints` directory, while LoRAs should be placed in the `Fooocus/models/loras` directory and will then appear as options upon restarting the code. There are quite a few other directory to place additional configurations and tweaks, but at this point you're equipped to set off on this adventure on your own! 

Good luck!
