## How do I cite software in my papers?

This article briefly introduces citing software in your papers and why that is important. 

[tl;dr] Do cite software as you would science references. Put citations in the text, in a dedicated \software or acknowledgments sections. Anywhere. If you are unsure how to cite it, ask for help.

### Why should I cite software? 

All research today uses software ([Momcheva & Tollerud, 2015](https://ui.adsabs.harvard.edu/abs/2015arXiv150703989M/abstract)). These uses include reducing and analyzing data, creating visualizations and plots, and simulating physical processes, among many others. As such, software is an integral part of doing science. There are (at least) three main reasons why you should cite software in your papers: credit, reproducibility, and visibility.

1. Writing software, much like building instruments, requires significant effort. Citing software gives credit to its authors, especially those in academia. It allows them to keep track of the impact of their work in the same way we measure the impact of scientific publications by their number of citations. For projects which have used grant funding to produce software, citations can be reported to funding agencies and used to justify continued funding.
2. Citations help with research reproducibility and allow others to understand how a given task was carried out. 
3. Citations to software allow other researchers to discover that software. They can then use it for other purposes, advancing their own research field.

### What software should I cite?

According to the FORCE11 recommendations (Smith et al., 2016): _"software should be cited on the same basis as any other research product such as a paper or book; that is, authors should cite the appropriate set of software products just as they cite the appropriate set of papers."_ If a claim relies on the analysis done with particular software, you should cite it. 

### Where in my paper should I place the software citations? 

**Example 1:** Include citations to software in the body of the paper, in the same way, you would cite a relevant article. For example:

```The my_code library (Doe et al., 2021) was used to derive stellar masses and redshifts for the sources.```

For more examples, see the [AstroBetter post of citing astronomical software](https://www.astrobetter.com/blog/2019/07/01/citing-astronomy-software-inline-text-examples/).

**Example 2:** The AAS Journals (ApJ, ApJL, ApJS, and AJ) allow for a separate section dedicated to software. This section appears before the acknowledgments and is marked by a ```\software``` tag. The AAS journal template includes this tag. It is a good place to include citations to libraries and open source software projects that were necessary dependencies but did not get shout-outs in the text of the paper. Here is an example of what this section looks like from [Finkelstein et al. (2022)](https://arxiv.org/pdf/2207.12474.pdf):

```
_Software_: Astropy (Astropy Collaboration et al.
2013), Bagpipes (Carnall et al. 2018), Cigale (Burgarella et al. 2005; Noll et al. 2009; Boquien et al.
2019), Dense Basis (Iyer & Gawiser 2017; Iyer et al.
2019), Drizzle (Fruchter & Hook 2002), eazy (Brammer et al. 2008), GalfitM (Peng et al. 2010; Haußler
et al. 2013), Photutils (Bradley et al. 2020), Prospector (Johnson et al. 2021), SciPy (Virtanen et al. 2020),
Source Extractor (Bertin & Arnouts 1996), Statmorph (Rodriguez-Gomez et al. 2019), STScI JWST
Calibration Pipeline (jwst-pipeline.readthedocs.io)
```
The [(Astronomy) Acknowledgement Generator](https://github.com/astrofrog/acknowledgment-generator) can get you started on creating the ```\software``` section. 

**Example 3:** For journals that do not have a ```\software``` section, the current recommendation is to include software in the acknowledgments. For example, see the MNRAS submission of [Baffuret et al.](https://arxiv.org/pdf/2207.14733.pdf) (2022): 

```
Facilities: JWST, HST
Software: matplotlib (Hunter 2007), numpy (Oliphant 2015),
scipy (Virtanen et al. 2020), jupyter (Kluyver et al. 2016),
Astropy (Astropy Collaboration et al. 2013, 2018), grizli (Brammer 2018), 
SExtractor (Bertin & Arnouts 1996), bagpipes (Carnall et al. 2018).
```

### How should I format my software citations?

The best way to cite software is to include a bibliography entry to it. Only those entries in the bibliography are tracked by services that count citations! Footnotes and URLs included in the text of the paper without a reference in the bibliography do not give proper credit to the authors. 

Note that not all journals accept `@software` BibTeX entries. If you encounter issues (e.g., MNRAS), you can replace these with `@misc` entries. 

When trying to find how to cite software, we suggest you follow these steps:

#### Best: Use the information provided by the authors

1. If the software authors have a recommended way of getting cited, please use that. Examples: [`astropy`](https://www.astropy.org/acknowledging.html), [`exoplanet`](https://docs.exoplanet.codes/en/latest/tutorials/citation/) and [LMFIT](https://lmfit.github.io/lmfit-py/faq.html#how-should-i-cite-lmfit). If a paper is associated with the software, do include that reference in your bibliography just as you would with any other reference. 

2. If the software is on GitHub and it has a `CITATION.cff` file, use the handy option provided by GitHub to download a BIBTeX citation and include that in your bibliography. See, for example, the [`eazy-py`](https://github.com/gbrammer/eazy-py) repository.

3. If the software has a digital object identifier (DOI) mentioned anywhere on its repository or documentation page, you can usually follow the link or [resolve the DOI](https://dx.doi.org/). Most hosting platforms provide a way to download a BibTeX reference. Examples: 
    - The LMFIT GitHub [reposotory](https://github.com/lmfit/lmfit-py/tree/1.0.3) includes the Zenodo DOI [link](https://zenodo.org/record/11813#.YqKAgxNBxBw) which has the [BiBTeX reference](https://zenodo.org/record/5570790/export/hx#.YqKArBNBxBw).
    - The Virgo [repository](https://github.com/0xCoto/Virgo) has a JOSS DOI [link](https://joss.theoj.org/papers/10.21105/joss.03067) with an easy-to-copy citation in the left-hand bar (as well as a [CITATION.bib file](https://github.com/0xCoto/Virgo/blob/master/CITATION.bib))

4. If none of these are available, but there is a paper describing the algorithm and the standard reference, cite that one. Example: [LA Cosmic](http://www.astro.yale.edu/dokkum/lacosmic/) is described in [van Dokkum (2001)](https://ui.adsabs.harvard.edu/abs/2001PASP..113.1420V/abstract)

If more than one of these options exists, i.e., a `CITATION.cff` file in the repository AND a software paper, do cite both. Including a reference in your article is cheap, but giving proper credit to your colleagues is priceless.

#### Good: Search for other breadcrumbs

There are cases where the authors do not provide explicit directions on how to cite their software. These codes still deserve credits if they have contributed significantly to the results of your paper. Look for some external possibilities on a best effort basis:

1. Search [ADS](https://ui.adsabs.harvard.edu/) for papers by the software authors that describe the code. ADS now indexes papers by the [Journal of Open Source Software](https://joss.theoj.org/).

2. Search the [Astrophysics Source Code Library](https://ascl.net/) (ASCL). ASCL generates a unique identifier in ADS which can then be cited. For example, the [2dfdr](https://ascl.net/1505.015) code mentioned in [Martin et al. (2005)](https://ui.adsabs.harvard.edu/abs/2005PASA...22..236M/abstract) can be cited as [2015ascl.soft05015A](https://ui.adsabs.harvard.edu/abs/2015ascl.soft05015A/abstract). Use the ASCL entry only if the authors have not provided direct instructions. Many ASCL entries are auto-generated and divergent from the authors' instructions. For example the [`grizli`](https://github.com/gbrammer/grizli) library has a Zenodo DOI, which is not listed on the auto-generated [ASCL page](https://ascl.net/1905.001).

#### Better than nothing: Include a link to the software in a footnote 

If you have exhausted all other avenues, including a link to the software in a footnote is better than not citing it at all. Here are examples from an AstroBetter blog post: https://www.astrobetter.com/blog/2019/07/01/citing-astronomy-software-inline-text-examples/

We hope these recommendations are helpful. If in doubt, get in touch with the Data Science Group. 


## Additional resources

- [AstroBetter post on citing astronomical software](https://www.astrobetter.com/blog/2019/07/01/citing-astronomy-software-inline-text-examples/)
- Smith AM, Katz DS, Niemeyer KE, FORCE11 Software Citation Working Group.
(2016) Software Citation Principles. PeerJ Computer Science 2:e86.
DOI: [10.7717/peerj-cs.86](https://doi.org/10.7717/peerj-cs.86)
- Katz D. S. et al., "Software Citation Implementation Challenges", [arXiv:1905.08674](https://arxiv.org/abs/1905.08674)
- Crouch, Stephen et al., "The Software Sustainability Institute: Changing Research Software Attitudes and Practices," DOI: [10.1109/MCSE.2013.133](http://dx.doi.org/10.1109/MCSE.2013.133)
- AAS journals [software citation instructions](https://journals.aas.org/references/#software)
- [(Astronomy) Acknowledgement Generator](https://github.com/astrofrog/acknowledgment-generator)
