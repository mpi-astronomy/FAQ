## How do I publish my software?

This article briefly introduces what's essential when publishing software, and hopefully, it will demystify perfectionism requirements for open source publication.

> There is always more effort to convert an existing project than to start a new one with good practice in mind. 

### What is **open-source** software (in astronomy)?

An open-source code corresponds to a source code made freely available for possible modification and redistribution. It includes (limited) permissions to (re-)use the product's source code, design documents, or content. 

_It is somewhat similar to an ArXiv publication using tex source files._

> **Open source model**: A copyright holder grants users the rights to use, study, change, and distribute the software to anyone and for any purpose.

### Why should I publish my codes?

Whether to reduce, analyze, visualize data or simulate physical processes, all piece of research today employs software (e.g., survey from Momcheva & Tollerud, 2015).

There are at least **three reasons** one should open source their software: **credit, reproducibility, and visibility.**

* **Credit**: writing software requires effort from one or many. Recognizing contributions is essential. Authorship allows us to keep track of an individual's impact in the same way we measure the impact of scientific publications. 

* **Reproducibility**: an open-source code allows others to understand how you obtained a scientific result. Similar to listing assumptions or equations in a paper, a code contains your complete framework.

* **Visibility/Impact**: public software is more prevalent in general because it lowers the barrier to using it (e.g., you do not have to contact a person to run). More visibility means more impact, which increases the number of users. If your code is also open-source, it may be further "improved" by others advancing their research.

> see also our _how-to-cite-software_ post.

#### Where to publish?

In terms of where to publish your code, the primary goal is to share your source. You can easily publish your source code on platforms such as [GitLab](https://gitlab.com/), [GitHub](https://github.com/), [framagit](https://framagit.org/), and [Bitbucket](https://bitbucket.org/). You can refer to this [stackshare article](https://stackshare.io/stackups/bitbucket-vs-github-vs-gitlab) comparing some of these platforms. Other platforms also exist but note that their varied popularity may be important to consider.

Do not forget to provide information on how to cite your code with your source. A good practice introduced by GitHub is to define a [`CITATION.cff`](https://citation-file-format.github.io/).

> see also our _how-to-cite-software_ post.

In addition, you can assign a Digital Object Identifier (DOI) to your codes to make them citable and trackable, and Zenodo is the reference in this domain. Depending on the content of your repository, this may be the best way to provide a version reference. 

Finally, you can have an article dedicated to your code. The standard journals in astronomy (e.g., ApJ, MNRAS, A&A) now accept software papers. But outside these journals and computer science journals, the [Journal of Open Source Software (JOSS)](https://joss.theoj.org/) is is an academic journal with a formal peer review process dedicated to the publication of research software packages. Their publication procedure is entirely through GitHub, and the refereeing process is available publicly with the article. Maybe as important, the paper's length can be very minimal. JOSS offers a very low-effort way to have refereed publications for your codes.  

### What are the actions for software publication?

Again, let's emphasize that we are not writing for software developers in high-tech companies. These may have rigorous requirements.

In academic research, there are [in my opinion] three levels of publishability: strict minimum, good, and advanced states. Which stage to reach depends on your final goals and desired impact of the code.

#### The strict minimum: usability

> Your code is **usable** by others. _Technical discussions may be challenging, and comments from users may not be constructive_

Your code runs end-to-end correctly, and you want to publish for others to use (or to reproduce your results).
In practice, this state a way to archive legacy codes. 

You need to make sure that

1. All contributors agree to publish the code and that your collaboration or institute does not restrict you with specific policies (e.g., licensing).

2. You have a license (a LICENSE file). Various ones exist with different protections for the source/binary code and restriction levels (e.g., some impose that all dependencies have the same license). You can find comparative websites such as [ChooseALicense.com](https://choosealicense.com/licenses/).

3. You provide the necessary data to test your code with their expected outputs. Such input reference dataset is also essential to prevent breaking the code if any update happens. It is better if you also provide notes to run the code with this dataset (e.g., an example notebook)

4. You provide bare minimum documentation: in a README file. Your code needs a name, and it has a purpose to fulfill. The README could contain some usage examples and the necessary dependencies (e.g., python libraries)

> see also [The Whys and Hows of Licensing Scientific Code](https://www.astrobetter.com/blog/2014/03/10/the-whys-and-hows-of-licensing-scientific-code/)

#### The good state: popularity

>  your code is **usable** by others, and **welcomes new contributors**. _A solid code that is open to technical discussions_

Going from the bare minimum to a good state is where the heavy work happens. But the actual priority of updates depends on the publication goals. A "good" code aims to increase popularity by making it easier to use. The code is "clean," documented, and structured.

Before any change, you need to protect your code from introducing bugs. Mistakes are always easy to make. A good practice is to use a version control system to find and potentially revert changes (e.g., `git diff file.py`). The best practice is to have **unit tests**. 

Unit testing aims to isolate **each** part of the program and indicate that the individual components are correct. The code overall must give the right outputs (bare minimum state), but unit testing ensures each elementary brick of your code produces the proper outcomes.

> See `what-is-good-unittest` 

Once your code is "protected," you can start changing its source.  

Like any scientific article, you need to do some "spring cleaning": remove unnecessary pieces, uniformize style/layout and clarify (add documentation)

5. Remove deprecated functions and libraries. 

6. Adopt recommended language practice (e.g., [PEP8](https://www.python.org/dev/peps/pep-0008/) for python). Sometimes you may have the choice (similar to the flavor of English for papers), but you must pick a style and stick to it. The best practice recommends using formatting tools such as (e.g., [autopep8](https://github.com/peter-evans/autopep8) or [Black](https://github.com/psf/black) for python.

7. Document the source enough for others to follow (stick to a uniform style). One should primarily focus on the API doc strings. Various documentation styles exist, primarily `Javadoc`, `sphynx`, `Doxygen`; some languages have their recommendations. Best practice recommends at least 90% documentation coverage.

8. Avoid/comment/revise uninformative output messages during a code run.

9. Remove unused parts/variables of the code.

> "Spring cleaning" consists of time-consuming steps, each easily prone to breaking codes.

Like an article's section flow, the code's structure is also essential. You need to decide if your code aims at providing a "script" (project template) or a library/package to be integrated into other projects. Some refactoring may happen to make the source more accessible (see the `mpia-python-template`):

10. Arrange directory structure

11. Substitute hard-coded values for variables with default values (e.g., keywords in python, C++)

12. Adopt coding best practices. Primarily replace repeated pieces of code with calls to a single function and remove unnecessary convoluted parts (e.g., convert_to_bool(str) should use a cast declaration such as bool(str) or cast<bool>(str))

My tip if you have an existing code that needs to upgrade from a "bare minimum" to a "good" state: start from scratch! Such an approach forces you to look at every piece of code and identify which elements are key to being part of unit tests. It also makes adopting new directory structures easier.

#### Advanced stage: evolutivity

> Your code is **usable** by others and **welcomes new contributors**. The software can now get **"deep & fancy" development/updates**.
  
This stage is not commonly the first publication of a given code. It represents a stage in which a code can evolve in potentially many aspects.

You may want to target 
* the performance of your code, which requires profiling and optimization,
* the increase of the user community by polishing the documentation and tutorials,
* an improvement of internal algorithms, which requires the code to be modular and flexible,
* the reusability of your code, which needs a rigorous  API and packaging,
* the building of community development, which needs continuous integration tools and configurations.

All these targets could be equally attractive, but it is essential to remark these are independent of one another. 
Multiple aspects of your code can improve in parallel. You will need to merge efforts eventually.

In this context, version control is your friend: you can create branches for the aspects you want to tackle. (note the incentive from GitHub that makes websites from specific branches -- documentation!)

In addition, continuous integration is also your friend: make sure every change fits the overall project (source automated formatting, checking documentation coverage, and running unit tests can all be part of the integration!)
