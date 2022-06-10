## How do I cite software in my papers?

This is a brief introdution to citing software in your papers and why that is important. 

[tl;dr] Do cite software as you would science references. Put citations in the text, in a dedicated \software seciton or in the acknowledgements. Anywhere. If you are unsure how to cite it, ask for help.

### Why should I cite software? 

All research carried out today uses software (Momcheva & Tollerud, 2015). These uses include reducing and analysing data, creating visualizations and plots, simulating physical processes, among many others. As such, software is a integral part of doing science. There are (at least) three main reasons why you should cite software in your papers:

1. Writing software, much like building instruments, requires significant effort. Citing software gives credit to its authors, especially those in academia, and allows them to keep track of the impact of their work in the same way we measure impact by the number of citations of science papers. For  projects which have used grant funding to produce software, citations can be reported to funding agencies and used to justify continued funding.
2. Citations help with research reprodicibility and allows others to understand how a given task was carried out. 
3. Citations to software allow other researchers to discover it. They can then use it for other purposes, advancing their own research field.

### What software should I cite?

According to the FORCE11 recommendations (Smith et al., 2016): "software should be cited on the same basis as any other research product such as a paper or book; that is, authors should cite the appropriate set of software products just as they cite the appropriate set of papers". If a claim relies on the analysis done with a particular software, then you should cite it. It is generally not necessary to cite commercial software.

### Where in my paper should I put software citations? 



Example 1: Include citations to software in the body of the paper, in the same way as you would a cite a relevant paper. For example:

```The my_code library (Doe et al., 2021) was used to derive stellar masses and redshifts for the sources.```

For more examples, see the [AstroBetter post of citing astronomical software](https://www.astrobetter.com/blog/2019/07/01/citing-astronomy-software-inline-text-examples/).

Example 2: The AAS Journals (ApJ, ApJL, ApJS and AJ) allow for a separate section dedicated to software. This section appears before the acknowledgements and is marked by a ```\software``` tag. The tag is included in the AAS journals template. This is a good place to include citations to libraries and open source software projects that were key dependancies but did not get shout-outs in the text of the paper. For example:

```
```

Example 3: For journals that do not have a ```\software``` section, the current recommendation is to include software in the acknowledgements. For example:

```
```


### How should I format my software citations?

When trying to find how to cite software we suggest you follow these steps:

A. Try to use information provided by the authors.

1. If the authors of the software have a recommended way of getting cited, please use that. Examples: [astropy](https://www.astropy.org/acknowledging.html) and YYY (something other than paper). If there is a paper that is associated with the software, do include the reference to that paper in your bibliography just as you would with any other reference. 
2. If the software is on GitHub and it has a `CITATION.cff` file, use the handy option provided by GitHub to download a BIBTeX citation and include that in your bibliography. EXAMPLE.
3. If the software has a digital object identifier (DOI) mentioned anywhere on its repository or documentation page, you can usually follow the link or [resolve the DOI](https://dx.doi.org/). Most hosting platforms provide a way to download a BIBTeX reference. Examples: 
    - The LMFIT GitHub [reposotory](https://github.com/lmfit/lmfit-py/tree/1.0.3) includes the Zenodo DOI [link](https://zenodo.org/record/11813#.YqKAgxNBxBw) which has the [BiBTeX reference](https://zenodo.org/record/5570790/export/hx#.YqKArBNBxBw).
    - The Virgo [repository](https://github.com/0xCoto/Virgo) has a JOSS DOI [link](https://joss.theoj.org/papers/10.21105/joss.03067) with an easy-to-copy citation in the left-hand bar (as well as a [CITATION.bib file](https://github.com/0xCoto/Virgo/blob/master/CITATION.bib))
4. If none of these are available, but there is a paper that descibes the algorithm and is the standard reference, cite that. Example: [LA Cosmic](http://www.astro.yale.edu/dokkum/lacosmic/) is described in [van Dokkum (2001)](https://ui.adsabs.harvard.edu/abs/2001PASP..113.1420V/abstract)

If more than one of these options exist, i.e., there is a `CITATION.cff` file AND a paper describing the software, do cite both. 

B. Unfortunately, there are a lot of cases where the authors do not provide explicit directions on how their software should be cited. Look for some external posibilities:
1. ASCL
2. ADS

C: If all else fails, include a link to the software in a footnote. 

Examples form AstroBetter: https://www.astrobetter.com/blog/2019/07/01/citing-astronomy-software-inline-text-examples/

If in doubt, get in touch with the Data Science Group.


### Additional resources

- Smith AM, Katz DS, Niemeyer KE, FORCE11 Software Citation Working Group.
(2016) Software Citation Principles. PeerJ Computer Science 2:e86.
DOI: [10.7717/peerj-cs.86](https://doi.org/10.7717/peerj-cs.86)
- Katz D.~S. et al., "Software Citation Implementation Challenges", arXiv:1905.08674
- Crouch, Stephen et al., "The Software Sustainability Institute: Changing Research Software Attitudes and Practices," DOI: [10.1109/MCSE.2013.133](http://dx.doi.org/10.1109/MCSE.2013.133)
- AAS journals [software citation instructions](https://journals.aas.org/references/#software)

- Acknowledgement generator: https://github.com/astrofrog/acknowledgment-generator
