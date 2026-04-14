# An Introduction to GWDG Services on Generative AI for MPIA Employees

Generative Artificial Intelligence (GenAI) and Large Language Models (LLMs) have rapidly become essential tools in modern academic research. From streamlining literature reviews to assisting in code debugging and data analysis, these tools offer significant potential to enhance productivity. However, the computational demands of running state-of-the-art models often exceed the capabilities of standard workstations, and commercial cloud solutions can raise concerns regarding data privacy and cost.

For researchers at the Max Planck Institute for Astronomy (MPIA), the Gesellschaft für wissenschaftliche Datenverarbeitung mbH Göttingen (GWDG) provides a robust, self-hosted solution that balances performance, ethics, and accessibility.

## The Role of GenAI in Academic Research

LLMs function as sophisticated pattern-matching engines, capable of understanding context, generating text, and writing code based on vast training datasets. In an astrophysical context, these capacities can be leveraged for:

*   **Scientific Writing**: Drafting abstracts, refining clarity, and formatting references.
*   **Code Generation & Debugging**: Writing Python scripts for data reduction (e.g., using `astropy` or `pandas`) and identifying errors in complex pipelines.
*   **Documentation**: Summarizing lengthy technical manuals or API documentation.
*   **Image Generation & Editing**: Creating figures, diagrams, or concept illustrations from text descriptions, and modifying existing images programmatically.

While these models are powerful, they require significant GPU resources to run efficiently. Budget aside, Running them locally on a laptop is often infeasible for larger models, while relying on public commercial APIs may expose sensitive research data to third-party training policies.

## Advantages of Self-Hosted Institutional Infrastructure

Utilizing a centralized, self-hosted service like GWDG's offers distinct advantages over local execution or public commercial clouds:

1.  **Cost & Accessibility**: High-performance GPU hardware is expensive. GWDG provides MPIA employees with free access to powerful compute resources, removing the financial barrier of procuring individual hardware or using cloud credits.
2.  **Data Privacy & Ethics**: Unlike some commercial providers, institutional services can be configured to prioritize data sovereignty. GWDG's self-hosted approach ensures that prompts and data are processed within the institution's controlled environment, mitigating the risk of sensitive research data being used to train public models.
3.  **Sustainability**: Centralized computing centers are generally more energy-efficient per computation than individual desktop GPUs. By consolidating workloads in a facility optimized for power usage effectiveness (PUE), researchers can reduce the carbon footprint of their computational workflows.

## GWDG AI Services

GWDG offers several interfaces for interacting with generative AI models: **Chat AI** and **CoCo AI** for text and code, and **Image AI** for visual content generation.

### Chat AI
**Chat AI** is a web-based interface similar to commercial chatbots. It provides access to various open-source models, allowing users to engage in conversational queries for text generation, coding assistance, and general problem-solving. It is designed for ease of use, requiring no setup beyond authentication via your institutional account.

*   **Documentation**: [GWDG Chat AI Overview](https://docs.hpc.gwdg.de/services/chat-ai/index.html)

### CoCo AI (Command & Control AI)
**CoCo AI** is designed for more advanced integration into research workflows. It allows users to interact with AI models directly from the command line or via scripts. This is particularly useful for automating tasks, such as batch processing text analysis or integrating AI assistance into shell scripts and Python pipelines used for data reduction.

*   **Documentation**: [GWDG CoCo AI Documentation](https://docs.hpc.gwdg.de/services/ai-services/coco/index.html)

### Image AI
**Image AI** is a web-based service for generating and editing visual content using open-weight diffusion models. It supports two primary workflows:

*   **Text-to-Image**: Generate new images from natural-language prompts. The current model, **FLUX.1-schnell** (Black Forest Labs), produces high-quality photorealistic and artistic outputs with fast inference times.
*   **Image-to-Image**: Upload an existing image and modify it via a text description. The **Qwen-Image-Edit-2511** model (Alibaba Cloud) supports semantic editing, appearance changes, and even adding, deleting, or modifying text within an image.

As with the other GWDG AI services, both models are self-hosted — prompts and images are never stored on GWDG systems and are not used for model training. The simple web interface requires only an AcademicCloud login.

*   **Documentation**: [GWDG Image AI Overview](https://docs.hpc.gwdg.de/services/image-ai/index.html)

## Available Models

Chat AI provides access to a broad selection of large language models. All self-hosted models run entirely on GWDG hardware with no data storage — prompts and message contents are never retained. The catalogue is updated regularly as newer models are released; the full, up-to-date list is maintained at the [Available Models](https://docs.hpc.gwdg.de/services/chat-ai/models/index.html) page. We list below some noteworthy models as of this writing, split into two categories: self-hosted open-weight models and externallyhosted models.

```{figure} https://docs.hpc.gwdg.de/img/services/chat-ai-data-privacy.png
:alt: Data privacy diagram
:align: center

overview of the GWDG service.
```

```{important}

GWDG constantly updates its model offerings as new releases become available. For the latest information on available models, please refer to the [GWDG Available Models](https://docs.hpc.gwdg.de/services/chat-ai/models/index.html) page.

```


### Self-Hosted Open-Weight Models (hosted by GWDG)

```{warning}These models offer the strongest data-privacy guarantees but may not entirely keep your data inside the GWDG infrastructure.
While GWDG protects your data, models provide tools that may send out information (e.g., for web search or code execution) that could potentially leak data outside the GWDG environment. Check the [data privacy documentation](https://docs.hpc.gwdg.de/services/ai-services/chat-ai/data-privacy/index.html).
```

Example of hosted models available in Chat AI:

| Model | Provider | Parameters | Context Window | Strengths |
|---|---|---|---|---|
| **Apertus 70B Instruct** | Swiss AI | 70B | 65k | Fully open-source; multilingual |
| **DeepSeek R1 Distill Llama 70B** | DeepSeek | 70B | 32k | Good overall performance; faster than R1 |
| **Devstral 2 123B** | Mistral AI | 123B | 256k | Coding and agentic software-engineering tasks |
| **Gemma 3 27B Instruct** | Google | 27B | 128k | Vision support; great general-purpose performance |
| **GLM-4.7** | Z.ai | — | 200k | Great overall performance |
| **InternVL 3.5 30B A3B** | OpenGVLab | 30B (3B active) | 40k | Vision; lightweight and fast |
| **MedGemma 27B Instruct** | Google | 27B | 128k | Vision; specialised medical knowledge |
| **Llama 3.3 70B Instruct** | Meta | 70B | 128k | Solid all-rounder; creative writing & reasoning |
| **Mistral Large 3 675B** | Mistral AI | 675B | 256k | Strong general-purpose & vision; multilingual |
| **GPT OSS 120B** | OpenAI (open-weight) | 120B | 128k | Great overall performance; fast inference |
| **Qwen 3 30B A3B Instruct** | Alibaba Cloud | 30B (3B active) | 256k | Good performance; fast |
| **Qwen 3.5 122B A10B** | Alibaba Cloud | 122B (10B active) | 256k | Vision; great overall performance |
| **Qwen 3.5 397B A17B** | Alibaba Cloud | 397B (17B active) | 256k | Vision; largest model in the lineup |
| **Qwen 3 Coder 30B A3B** | Alibaba Cloud | 30B (3B active) | 256k | Specialised for coding tasks |
| **Qwen 3 Omni 30B A3B** | Alibaba Cloud | 30B (3B active) | 256k | Multimodal (text, audio, video) |
| **Teuken 7B Instruct** | OpenGPT-X | 7B | 128k | Optimised for European languages |

This list is not exhaustive. For more models, please refer to the [official documentation](https://docs.hpc.gwdg.de/services/ai-services/chat-ai/models/index.html).

### External Models (hosted by OpenAI / Microsoft Azure)

OpenAI models are relayed through Microsoft Azure under GDPR terms. Microsoft may store messages for up to 30 days. OpenAI may do more on its side. For maximum data privacy, prefer the self-hosted models above.

| Model | Context Window | Notes |
|---|---|---|
| **Claude Opus 4.6** | 1M | State-of-the-art reasoning, coding, complex analysis |
| **Claude Sonnet 4.6** | 1M | Balanced performance; fast responses |
| **GPT-5.4 / 5.4 Mini / 5.4 Nano** | 272k | Latest flagship; professional knowledge work, coding, agentic workflows |
| **GPT-5.3 Chat** | 128k | Multimodal chat; adaptive chain-of-thought |
| **GPT-5 / 5 Chat / 5 Mini / 5 Nano** | 400k | Range of speed-vs-capability trade-offs |
| **o3 / o3-mini** | 200k | Complex reasoning (older knowledge cutoff) |
| **GPT-4.1 / 4.1 Mini** | 1M | Large context window; coding & instruction following |

> **Tip for MPIA users:** The ChatGPT (OpenAI) models are available free of charge to Max Planck Society employees. All self-hosted models are free for everyone with a GWDG account.

*   **Full model catalogue**: [GWDG Available Models](https://docs.hpc.gwdg.de/services/chat-ai/models/index.html)
  
```{important}

**Why my favorite model is not provided? Can we add model "X"?**

The landscape of large language models is evolving rapidly, with new releases appearing frequently. GWDG prioritizes models that offer strong performance, data privacy, and ethical considerations. The services operate as a rolling list of models, that means that older models may be removed as newer ones are added, based on performance and user demand. The selection process also considers the computational resources required to run each model effectively, as well as the relevance to the research community.

If you have a specific model in mind that you would like to see added to the service, please contact the GWDG support team with your suggestion. They regularly review user feedback and may consider adding new models based on demand and suitability for the research community.

```

## Getting Started

To access these services, MPIA employees should visit the [GWDG Chat AI portal](https://docs.hpc.gwdg.de/services/chat-ai/index.html) and log in using their standard GWDG credentials. We encourage researchers to experiment with these tools to identify how they can best support their specific scientific workflows.
