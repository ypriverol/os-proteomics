# Letter from Editor

## Request for Formatting Changes

* Manuscript title page: 
Author affiliations: Provide postal codes for affiliations.

* Provide up to 10 words (place after Abstract section)

* A Table of Contents Graphic (TOC) also referred to as “Abstract graphic” is required for all papers. 
A well-designed TOC should give the reader a quick visual representation of the essence of the paper without providing details.
Specific rules apply to the TOC that do not to other manuscript graphics:
    - The TOC must be entirely original artwork, 100% created by authors ONLY, and unpublished.
    - Size should be approximately 3 inches x 3 inches (all images combined) as it is intended to be a very small graphic.
    - Label as "For TOC Only" on same page as graphic, and combine as last page of the manuscript (do not number as a figure or include a legend).

* Examples of correctly prepared TOCs are provided in attachment for further guidance.

* References:
    1) Use superscript numbers to cite references in the manuscript text. Number sequentially beginning with 1, in order of appearance in the paper
    2) Before submitting your revised paper, check all references to ensure the following:
        - Number of in-text citations match number of references at the end of the paper 
        - Each source is numbered separately (that is, multiple sources are not combined within a single numbered reference.)
        - All references are cited at least once, and there are no duplicates
        - Complete bibliographic information is provided for each reference. DOI may be included but NOT used instead of this information unless it is not available, such as for preprints or recently accepted papers which have not yet received issue placement. 

The ACS Guide to Scholarly Communication contains detailed information required for each type of reference. The following list includes needed information for the most commonly seen types:
    - Journal articles: Author names, article title, source, year, and first page. Articles not yet published and missing required information should be labeled “in press”.
    - Books: Author or editor names, book title, publisher name, and year.
    - Websites: URL and date of access (month and year minimum but day included is preferred).
    - Patents: Author names, title of patent, patent number including office code, and year.
    - Theses: Author name, title, institution name, and year.
    - Preprints: Author names, title of article, name of repository (section name, if provided)*, submission date, DOI or URL (accessed YYYY-MM-DD).  *An example of repository with section name would be: arXiv (Physics.Atomic and Molecular Clusters)
    - Conferences/Reports: Authors, paper or chapter title, book or proceedings title, publisher, and year.

## Reviewer(s)' Comments to Author:

### Reviewer: 1

Perez-Riverol et al. present a review of open-source software in proteomics, with a view toward the FAIR4RS principles. The manuscript is well written and interesting, but I have a few suggestions that the authors should consider to strengthen the manuscript:

1) At the top of page 13, the authors discuss the phenomenon of users uncovering bugs and reporting them and maintainers fixing them and assert that this “feedback loop is unique to OSS”. This happens continually in closed source software as well. Users report bugs/ask questions to software vendors of closed source software, which are often promptly fixed as well. Vendors can often have closer relationships with their customers than OSS projects since there may be payment involved. The only element in the paragraph that is more relevant to OSS is “or asked questions about the underlying code”. But even there, code can be visible even when is it is not truly FOSS. I suggest that this paragraph be given some more thought and adjusted to highlight was is truly unique to FOSS.

2) Figure 1 is somewhat interesting, but I have concerns about how good the data are. It is nice that the source code is provided, but I feel that “Scientific papers published in the Journal of Proteome Research that include a GitHub URL in their abstract” is a weak dataset to gain a true understanding of the status of the field. I reviewed the results of the query in the gist and it seems that several of the works being counted are not really software tools, but rather resources that leverage the social power of GitHub. And likely the majority of widely used proteomics tools are not captured by this query. I don’t think this figure captures the status of the field. I think it would be a far greater service to the readers and to the field to manually collect the top NNN tools in the field, and score them on a handful of basic FOSS metrics and usage statistics and present the results of this in one or more panels of a more useful figure. Each tool could have basic citation (or mentions without citation) metrics, license, categories (truly FOSS, free for academic, commercial, etc.), domain (DDA, DIA, Ident, Quant, etc.). These data are not easy to acquire, far more difficult than a quicky script on gist, but I would argue far more useful, and perhaps with 20+ coauthors to share the work, it could be readily acquired. Perhaps such data could be publicly gathered and managed on a GitHub site via PRs, such that the “current status of FOSS in proteomics” itself becomes a high quality publicly viewable dataset (subject to bug reports and refinement) that could be studied more carefully and inform the views presented in the manuscript. And perhaps even maintained in such a way that the status of the field could be re-measured in 5 years time, say, perhaps to assess/claim that this manuscript had a positive impact on the field.

3) The topic of interoperability seems nearly entirely absent in the manuscript. A text search for “interop” yields only 3 hits and 2 are just the definition of FAIR, and then last just an offhand remark. It would seem that interoperability is key topic that should be addressed in the manuscript. Should proteomics software support standards? Are ad-hoc TSV or JSON formats okay/good/better? I am startled to find no mention of the PSI or mzML or any such attempts (useful or not) to provide data formats, guidelines, and other standards whose stated goal is to enable interoperability of software. How common is the thought “well, this newly published software tool seems nice, but it does not interoperate with the input/output of my toolchain, so what value is it?” How can the field make progress with that problem? I think the manuscript should be enhanced to address this aspect.


### Reviewer: 2

This position paper advocates the use of open-source and FAIR research software practices in computational proteomics. To strengthen their position, the authors analyse the current OSS/FAIR4RS situation in computational proteomics, and survey relevant corresponding practices. Although all these techniques are obviously not novel, the careful tailoring to the computational proteomics domain make it a very valuable article. In the light of the transition to open science, these messages cannot be repeated often enough. I am therefor in favour of accepting this manuscript.

Some suggestions to improve the manuscript:
- Only some of the key challenges listed in the introduction are backed by concrete evidence or references. If possible, please provide same such also for the others.
- The fourth challenge mentions that "proteomics software is often distributed under restrictive licenses". Is there a specific reason for this?
- At the end of the introduction, some "the paper is structured as follow" would be nice, to get an overview of what to expect from the paper in more detail. Similarly, some sections (e.g., 2 and 4) directly jump into the first subsection, and Section 8 only contains a figure/box. Some "moderation text" would be helpful here.
- Section 2.1 starts off to "address misconceptions in proteomics". These don't seem very proteomics-specific, though. Rephrase?
- Section 2.2 is then again called "misconceptions", and indeed is partially redundant with 2.1. Could probably be consolidated, or should be clearly distinguished from each other.
- In Section 6, the link to NIH does not look "clickable", perhaps check if correctly formatted.
- Section 9 explicitly references the "academic setting", but my impression is that the whole article before actually focuses on academia. Please clarify.

- One of the recommendations in Box 2 is that "any new tools created by students or staff are incorporated into the code base". Here I would appreciate a discussion of potential pitfalls of using students' code, which in case of coursework or theses might only be legally possible if students explicitly agree.
- Reference 22 to FAIR4RS could probably be replaced or supplemented by the direct reference to the principles, https://doi.org/10.15497/RDA00068

-----------------------------------------------------------------------
