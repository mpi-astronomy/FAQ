# What to do with "legacy" code?

The goal of this article is to get you started on working with your own or someone else's "legacy" code. Legacy is not necessarily old code. Legacy is code that is lacking one or more of the following: documentation, tests and/or installation instructions.

[tl;dr]

So it has happened again: you are staring at some old code and you need to get it working. Maybe the code is your own or maybe it came from a collaborator.
You know the language it is written in or you may not. You may be able to just run it as it is or you may want to re-write major parts of it, sometimes even "translate" it into another language. How do you go about this without losing your mind?

## Clarify Your Intentions

Beware of scope creep. When working with legacy code, it is very easy for work to expand past the original intentions. What are you trying to get out of this? Once you are clear on the goals, identify the specific actions that are necessary to meet the goals. Here are some possible goals and actions:

- Replicating result: install and run current state of code.
- Repurpose parts for a new project: identify necessary parts, document code, and extract functionality to a new module.
- Running code on new data: this can have a wide range of scope, see below.
- Expand/upgrade code
- Make code available for collaboration

## Save the Current State

Before you touch anything, before you even change a single value, archive the current state of the code. Ideally, an archive will not live on your hard drive.
The easiest way is to create a zip file and upload it to Google Drive, Dropbox or any other document-sharing service your institution has. Alternatively/additionally,
upload the code to a private repository on GitLab, BitBucket or GitHub. If this code is not published, please seek the permission of the original authors
before you put it in a public repository (see [How to publish software?](https://mpi-astronomy.github.io/FAQ/chapters/publishing/how-to-publish-software.html)).

At his point, it is also useful to preserve any input/output files if these were not provided by the original author. Can you install and run the code? Do you have the needed inputs? Can you generate some outputs? If you can, document all these steps in a simple readme file. Write down what you had to do to get the code running. Archive any inputs or outputs together with the code. This may already be too much effort. Timebox this work. A day of solid effort trying to do this is good. More than that and you are probably going down a rabbit hole.

## Take Advantage of our Robot Overlords

Large language models (LLMs) can be very helpful in the task of understanding legacy code. You can paste a function or a snipet of code into an LLM and ask it to explain the code. Even more useful can be loading the codebase into a integrated development environment (IDE) like VSCode or PyCharm where tools like GitHub Copilot are available as extensions. These tools can "see" the whole codebase, create docstrings, tests and explain code. These tools can also be extremely helpful for the steps in the next section.

If you are trying to replicate results from existing work, this may be where you stop. This could also be the endpoint if you are trying to run the code on new data. More likely than not, however, you will have to make some changes to the code to accommodate new data (e.g., new file formats, new calibrations, etc.). This leads us to...

## Now What?

### Level One: If You Need to Change the Code

- try to understand as much of it as possible, draw a diagram of how it works, and add some doc strings that explain what different functions do
- maybe write some simple tests that work with the current code so you don't break the things that already work
- how big is the scope of change, small? are you sure?

### Level Two: If You Need to Extend the Code

Ok, at this point, you are making major contributions. If is worth rethinking how the whole thing works.

- Structure it properly.
- Add tests as you go.
- Add documentation as you go.

### Level Three: If You Need to Make the Code Available

Hopefully, you followed the instructions above, if not, go back to the previous.

### Level Four: If You Need to "Translate" the Code

So you have code that is written in language that can no longer be compiled or was gone out of style in your files (e.g., IRAG, IDL). It happens to the best of us.

DO NOT go line by line and transpose the code. Never. Ever.

- Identify the functionality you need. Rethink the structure, what was best for the previous language would not be best for this. For example, if you are translating from a functional/procedural to object-oriented language. It is likely that you only need 10-20% of the code base but you need to understand the whole code base to find this 10 - 20 %.
- Many legacy codes will have their implementations of common functions (e.g., a Gaussian). Use common libraries to replace these.
- Just because the legacy code made some questionable decisions about structure, hard-coding paths and looping over matrixes, it doesn't mean you should make the same mistakes.
- Talk to colleagues on how to re-implement complex functionality such as computationally intensive pieces, interactive graphics, etc.
- You can also leverage LLMs to translate from one programming language to another (as in [this example](https://youtu.be/jXu_-edmMzc?si=6IdWK4YXA9ASelTu) of converting from IDL to Python). 

## Publish your code.

[How to publish software?](https://mpi-astronomy.github.io/FAQ/chapters/publishing/how-to-publish-software.html)

## Resources:

- [Intermediate Research Software Development in Python](https://carpentries-incubator.github.io/python-intermediate-development/)
- [Packaging and Publishing with Python](https://carpentries-incubator.github.io/python-packaging-publishing/)
- [Best Practices for Scientific Computing](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745)
- [Good Enough Practices in Scientific Computing (PLoS Comp Bio)](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510)
- [Carpentries: Good Enough Practices in Scientific Computing](https://carpentries-incubator.github.io/good-enough-practices/index.html)
- [Python Testing and Continuous Integration](https://carpentries-incubator.github.io/python-testing/)
- Don't really want to do this but here for completeness: https://github.com/showyourwork/showyourwork
- [The Good Research Code Handbook](https://goodresearch.dev/index.html)
- [PyCon: Working Effectively with Legacy Code](https://www.youtube.com/watch?v=RMt43wyg-zg)
- [PyCon: What is this Mess](https://www.youtube.com/watch?v=LDdUuoI_lIg)
