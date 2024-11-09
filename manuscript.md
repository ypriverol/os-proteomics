# Open-Source and FAIR Research Software in Proteomics]

## Introduction

Research software is essential to modern science, with the majority of scientists recognizing it as indispensable for their work and often impossible to conduct research without it [28751965, https://zenodo.org/records/14809].
This reliance on software is equally crucial in proteomics, where researchers depend on a range of tools and algorithms for every step, from data acquisition and mass spectrometer configuration, to the subsequent stages of processing, analysis, and interpretation [23467006, 34906327].

Since the original publication of the first peptide identification tool, SEQUEST [24226387], proteomics software has evolved into a sophisticated ecosystem encompassing multiple stages of data processing, advanced predictive models, and robust computational frameworks. 
There are numerous examples of software tools developed and used by the proteomics community. These include tools like Percolator [17952086] which is used to improve peptide and protein identification using machine learning, Prosit [31133760] which applies deep learning to predict fragment ion intensities, aiding in more accurate spectra matching, and Proteowizard [23051804] that attempts to provide shared libraries and tools for fileIO. Platforms like GalaxyP [29092937], or quantms [38965444] facilitate accessible, reproducible analyses through high-performance computing (HPC) and distributed workflows, supporting researchers in handling large datasets and complex analyses. 
Together, these advances underscore how proteomics software has transformed into a multidisciplinary field, in a complex ecosystem of algorithms, models, and software tools requiring sophisticated computational and algorithmic expertise.

Computational proteomics, along with algorithm and software development, faces several key challenges common to other omics fields:

- The increasing complexity and size of data acquired by mass spectrometers, the complex sequence of steps, including spectral processing, statistical analysis, and biological interpretation, along with the need to manage algorithmic details and parameter settings, all contribute to making software development in proteomics a complex and demanding endeavor.

- Ensuring reproducibility is a challenge due to the limited access to detailed algorithmic information, which hinders validation and extension of methods.

- Although most software tools are described in publications, the absence of open-source code, comprehensive documentation, and version control often impedes reproducibility and reuse. 
This lack of accessibility also limits opportunities for researchers and developers to contribute effectively to advancing proteomics software. 
- Custom licenses and restrictions on software distribution can further complicate the situation, making it difficult to share, modify, or redistribute software, and hindering the development of a collaborative and open-source ecosystem.
Proteomics software is often distributed under restrictive licenses and tailored to specific platforms (e.g., operating systems, computer architectures), limiting its use across diverse environments and services. This restricts the field’s adaptability and hinders the integration of proteomics with other omics disciplines. 

- Complex workflows and high-throughput data analysis are currently relying on (unattended) software deployment. This is complicated on its own because it requires managing dependencies, configurations, and environments consistently across diverse systems and  architecture without human intervention. 
The community has tackled this challenge with CI/CD pipelines as, for example, described in 10.1101/gr.276963.122, but this relies on OSS and the permission to freely redistribute software along the entire dependency chain. 
If one piece in this supply chain is not OS, exceptions need to be handled and automatization is harder or impossible. 
In sum, it creates a huge additional burden for the entire community downstream of the non-OS software package, which on its own is a hidden cost.

Open-source software (OSS) following FAIR principles (Findable, Accessible, Interoperable, Reusable) offers a solution to these challenges, empowering proteomics with tools that are not only accessible but also foster community-driven development, rigorous validation, and transparent sharing of methodologies [].
OSS has demonstrated clear benefits in increasing the accessibility, usability, and visibility of scientific software [30212065]. 
OSS makes reproducibility, traceability and auditability possible.
With code freely available for inspection, modification, and distribution, OSS encourages collaboration and creates avenues for continuous improvement—factors that are critical in fields as data-intensive as proteomics. 
OSS is also aligned with the FAIR Principles for software research (FAIR4RS) established for research data, which were expanded in 2022 [26978244] to address the growing recognition of research software as a foundational research asset [36241754].

In this manuscript, we aim to explore the role of OSS in computational proteomics and its implications for the development of FAIR research software. 
We will discuss the benefits and challenges of OSS in proteomics, the role of OSS in the development of FAIR research software, and the importance of distribution, licensing, and citation of software in computational proteomics. 
We will also explore how other omics fields are dealing with OSS and FAIR software, and how these experiences can inform the development of proteomics software. 

## What does it mean for software to be "open source"? 

OSS (open-source software) refers to software where the source code—the core instructions that define how the software functions—is freely accessible to anyone (https://opensource.org/osd). In contrast, closed source means that the source code of the software is not published, and it is not shared with the public for anyone to look at or change.

Unlike "closed-source" or "proprietary" software, where the code remains private, OSS provides transparency by design, which is essential for fostering trust, collaboration, and progress in science.
However, the open- or closed-source label simply addresses code visibility; it is the software license that determines who can use, modify, or distribute the software and under what conditions.

In proteomics, and bioinformatics in general, multiple misconceptions exist about open/closed source software: 

- Closed-source software with "academic" licenses are equivalent to open-source. This is not true as academic licenses only refer to free-for-academic-use. The source code is not necessarily open, shareable, or modifiable. Even the term "academic" is not well-defined as it can refer to a wide range of institutions and organizations. To simplify this complexity, we can define OSS as any software that uses an OSI-approved license (https://opensource.org/licenses). 
- Open-source means that only the code is accessible. This is not true. Open-source software does not only mean that the code is openly available but also that it is allowed to be modified and shared.
- Free open-source software (FOSS) means free of financial cost. In this context, "free" does not imply cost, lack of security or support. Instead, it emphasizes the freedom to run, copy, modify, and distribute the software as desired (https://www.gnu.org/philosophy/free-sw.html).
- OSS is often mistakenly viewed as lacking professional quality. However, many open-source projects are maintained by dedicated teams with robust testing and good best programming practices. In genomics, projects like samtools (https://github.com/samtools/samtools) [19505943], an MIT-licensed project with over 80 contributors and 50,000+ citations, and the Genome Analysis Toolkit (GATK, https://github.com/broadinstitute/gatk) [20644199], now open-source with over 100 maintainers and 26,000+ citations, exemplify this standard. In proteomics, Percolator (https://github.com/percolator/percolator) [17952086] has over 700 citations and 20 contributors, serving as a core tool for projects like MS2Rescore [35803561], OpenMS [38366242], and Crux [36598107]. Other successful open-source projects in proteomics, such as OpenMS [38366242], Skyline [20147306], PeptideShaker [25574629], and ProteoWizard [23051804], demonstrate the benefits of transparency and collaboration. Despite these successes, academic open-source proteomics software is still perceived as lower quality. In 2018, Rob Smith highlighted the community’s concerns about academic proteomics and metabolomics software, including poor documentation, lack of transparency, and limited support [29546988], though much of this feedback was directed at academic and free-for-academic-use software, not necessarily open-source. 

In addition to all these misconceptions and complexity, many journals mandate code availability as part of publishing, which has prompted multiple bad practices from software developers and bioinformaticians aiming to fulfill these requirements. 

- Researchers upload closed-source software to platforms like GitHub, giving an impression of openness with features such as issue tracking, while the actual source code remains inaccessible. Although often well-intentioned, this practice can mislead other scientists and, in our view, should be discouraged. 
- Software is deposited in GitHub as open-source during the submission of the manuscript, but after publication; software licenses in GitHub repositories are changed, repositories deleted or made private, complicating efforts to ensure long-term accessibility.

Given the many misconceptions and complexities surrounding open-source in proteomics, we aim to clarify for the entire community (users, developers, manuscript readers, and reviewers) what constitutes open-source, what does not, and how to transparently communicate the state of own software: [JKE: is "own software" meant to be "OSS software" here??]

- **Source Code Availability**: The source code is publicly accessible, allowing anyone to view, download, and examine the code’s details (https://opensource.org/osd).

- **OSI-Approved License**: The software must use an OSI-approved license, which specifies rights to freely use, modify, and distribute the software, regardless of its application or environment (https://opensource.org/licenses).

- **Freedom to Modify and Distribute**: Open-source software, in contrast to source-available software, allows users not only to access the code but also to modify it and share these modifications, encouraging innovation and collaboration.

- **Transparency and Community Trust**: With open-source, the code is transparent by design, allowing the community to understand, verify, and contribute to the project. This fosters trust and credibility, especially crucial in scientific fields.

- **Collaborative Development**: Open-source projects are often maintained by communities or dedicated teams, and they welcome contributions, such as bug reports, enhancements, and new features, from a diverse group of users and developers.

- **Long-term Reliability**: Because the code is publicly accessible, open-source projects are less dependent on single organizations or developers, promoting continuity and stability even if original contributors leave.

- **No Restriction to Specific User Groups**: Unlike “free-for-academic-use” licenses, which restrict usage to academic settings, open-source licenses do not impose limitations on the types of users or institutions that can access or use the software.

- **Not Dependent on Platform**: Open-source projects aim to be platform-agnostic, allowing integration across various environments and reducing dependency on proprietary systems or architectures.

- **Not Necessarily Free of Cost**: Open-source software is “free” in terms of freedom, not necessarily in terms of price. Users might pay for support, hosting, or additional services, but they retain freedom in how they use and modify the software.

## Why open-source software is essential for scientific research

### Transparency promotes scientific rigor

The scientific community increasingly recognizes that algorithms, while not software or tools themselves but rather the underlying steps and methodology, are becoming significant research outputs in their own right. Algorithms are no longer seen merely as tools but are valued as core research outputs, reflecting the critical steps and methodologies at the heart of scientific innovation. For example, in proteomics, the fragment-indexing approach introduced by the MSFragger algorithm has recently been implemented in two different search engines: SAGE [37819886] and Comet [10.1101/2024.10.11.617953]. This shift highlights the importance of not only software as a means of implementation but also the reproducibility and reliability of computational methods that drive new discoveries. Both algorithms and their software implementations are now held to rigorous validation and reproducibility standards, similar to those for traditional experimental data.

Transparent computational methods open doors to innovation, enabling researchers to test hypotheses, refine methodologies, and build upon one another’s work with confidence. For instance, providing open-source implementations allows the scientific community to verify methods, adapt them to new challenges, and explore alternative approaches. Open-source code therefore becomes a powerful tool for disseminating knowledge, facilitating shared standards, and accelerating the pace of discovery. Consider a proteomics experiment: without details on sample preparation or instrument settings or the raw data, the final results lack reproducibility. Similarly, open code ensures that computational methods can be accurately understood, replicated, and extended across labs worldwide.

When algorithms and models are shared as open-source software, they inherently uphold the FAIR principles applied to scientific data. This level of openness strengthens scientific rigor, enabling others to examine the code, replicate findings, and contribute improvements. A transparent approach to computational research, through openly available code, fosters a collaborative environment where the community can validate results and improve tools, ultimately building trust in computational methodologies.

Moreover, open-source implementations guard against unintended variation in outcomes caused by minor differences in coding practices, dependencies, or hardware environments. Even small programming choices can lead to significant changes in results. Open code mitigates these risks by making the entire process visible, allowing other scientists to understand the nuances and make informed adjustments. Transparency is key in computational research, not just for ensuring rigor but for building a reliable foundation that drives the entire field forward.

Finally, open-source code allows researchers to apply and compare different implementations, revealing assumptions and enhancing understanding. For instance, discrepancies between implementations of common tools, such as variations in BLOSUM matrices for sequence alignment[18327232], demonstrate how essential code transparency is for ensuring scientific consistency. Open-source practices thus empower researchers to expand on established methods with confidence, propelling science toward more robust, reproducible, and innovative outcomes.

### Shared knowledge pushes the field forward

Open-source software (OSS) fosters a collaborative ecosystem where researchers across institutions can freely contribute, refine, and extend tools, accelerating scientific progress. 
Unlike proprietary software that confines advancements to specific labs or companies, OSS allows researchers to build on each other’s work without duplicating efforts, promoting efficient resource use and transforming individual achievements into collective gains. 
By democratizing access to high-quality tools, OSS enables scientists from resource-limited settings to leverage the same technology as those in well-funded institutions, fostering a diverse global community that drives innovation forward.

Proteomics has greatly benefited from this open-source approach.
Projects like ProteoWizard [18606607,23051804], with tools such as Skyline [20147306] and msConvert [28188540], exemplify OSS’s impact. 
Skyline, for instance, supports over 20 external plugins available in its Tool Store, allowing users to perform specialized tasks far more efficiently than if they had to build solutions from scratch. 
Similarly, msConvert provides a standardized interface for mass spectrometry data, sparing developers the need to manage proprietary formats. 
These well-supported OSS projects create a foundational infrastructure that accelerates proteomics advancements.

However, sustaining successful OSS projects in proteomics requires ongoing community engagement, which has often proven challenging. 
Despite their long history, projects like ProteoWizard and Skyline see few external contributions. 
Many researchers opt to develop independent tools rather than contribute enhancements within Skyline, missing opportunities for broader collaboration. 
Skyline’s external tools framework, which lowers technical barriers to contributions, has helped but much of the development remains within the original labs.

Community contributions in proteomics face barriers unique to the field. 
Developing software for proteomics demands specialized technical skills that many labs lack, especially when resources are focused on biological research rather than software engineering. 
The need for continuous updates to accommodate evolving data formats and instruments also requires substantial resources. 
Additionally, academic incentives often prioritize novel software creation over contributions to existing projects, further deterring collaborative development.

To create a more robust and impactful OSS ecosystem in proteomics, stronger incentives for community involvement and frameworks that support sustained collaboration are essential. 
With enhanced incentives, collaborative frameworks, and dedicated resources, the proteomics community can achieve a more sustainable, widely supported, and effective ecosystem of open-source tools.

### The community can contribute to development

Open-source software also plays a critical role in iterative refinement.
Bugs and mistakes are inevitable in complex software, and these issues are often best addressed through collaborative scrutiny.
In our own work, users have uncovered bugs that we subsequently corrected, improving the reliability and robustness of our tools.
We have also experienced users asking questions about the underlying code, leading to new features and more efficient algorithms.
This feedback loop is unique to OSS, where the contributions from the community enhance the quality and precision of the software over time.
Without such transparency, computational research can become a "black box" that stifles innovation rather than promoting it, hindering the growth of scientific knowledge. 
OSS can foster a culture of shared accountability, where code is not just released but continuously scrutinized and refined, driving the field forward in a collective effort toward scientific rigor.
We have indeed observed this in our own projects: at the time of writing, quantms [38965444] and Mokapot [33596079] now have 12 and 13 contributors, respectively.

### Increasing emphasis on open science and open source by funding agencies

As open science gains prominence, major funding agencies worldwide are implementing mandates to ensure that software developed with public funds is openly accessible.
Horizon Europe, the European Commission's flagship research program, has set stringent requirements for open science, mandating that research outputs, including software, are shared under open or free licenses aligned with FAIR principles (https://commission.europa.eu/about-european-commission/departments-and-executive-agencies/digital-services/open-source-software-strategy_en).
Additionally, all Horizon Europe funded research is required to establish a data management plan (DMP), which is a structured document that outlines plans for open software and code sharing, including tools needed for interoperability.
In the United States, agencies like the National Institutes of Health (NIH) and the National Science Foundation (NSF) strongly encourage, and in some cases require, software and code sharing through public repositories, aiming to maximize reproducibility and scientific transparency (https://datascience.nih.gov/tools-and-analytics/best-practices-for-sharing-research-software-faq).
Similarly, the Wellcome Trust in the United Kingdom mandates that all research outputs, such as software integral to funded research, be made freely available under recognized open-source licenses to facilitate widespread accessibility and reuse (https://wellcome.org/grant-funding/guidance/policies-grant-conditions/data-software-materials-management-and-sharing-policy).
Many other funding agencies all over the world have similar open source guidelines and mandates.
This underscore a commitment from funders to foster collaborative scientific ecosystems, democratizing access to essential research tools and enhancing reproducibility across disciplines.

## How to get started with OSS

| Box 1. How to get started with OSS. The following steps provide a guideline that can foster a successful open-source project that grows in adoption, value, and contributions over time. |
| --- |
| 1. **Define clear goals and scope.** Start by defining the specific problem or gap your software aims to solve. Ensure it addresses an unmet need or provides a significant improvement over existing solutions. |
| 2. **Choose an open source license.** Choose an OSI approved license that aligns with the project's intended use and desired level of openness. For projects that may later require commercialization or enterprise use, dual licensing (e.g., open-source with an option for commercial licensing) can be considered to support sustainability. |
| 3. **Plan for sustainability.** Research potential funding sources, such as grants, academic support, or partnerships. Decide if the project will rely on donations, grants, or if it might later incorporate paid services. If applicable, consider models like SaaS, support-based revenue, or feature-based licensing that could sustain the project without sacrificing its open-source nature. |
| 4. **Set up a well-structured repository.** Use a version-control platform like GitHub or GitLab for easy access, community contributions, and versioning. Use clear folder structures, name conventions, and modular code design to enhance usability and maintainability. Provide a clear guide on how others can contribute to the project, including coding standards, pull request policies, and a Code of Conduct to foster a positive collaborative environment. |
| 5. **Implement rigorous testing and quality control.** Use continuous integration/continuous deployment (CI/CD) practices to automate testing and improve code quality. Platforms like GitHub Actions can be set up to run tests on each new code addition or pull request. Develop a robust suite of tests that ensure functionality and compatibility, minimizing the risk of bugs and ensuring reliability. Regularly review code for quality and potential improvements, inviting experienced contributors or external collaborators to audit the code. |
| 6. **Develop thorough documentation.** |
|   - User documentation: Provide tutorials, installation guides, and usage examples that lower barriers to entry for new users. |
|   - Developer documentation: Include technical details that make it easier for new developers to understand the codebase, contribute, and debug. |
|   - Version control and changelog: Maintain a detailed changelog for tracking updates, and consider using semantic versioning for releases to help users track changes and updates. |
| 7. **Build a community.** Create forums, mailing lists, or a Slack channel to facilitate communication and support for users and contributors. Promote the project within academic and industry circles, social media, or conferences. Collaborations with other researchers can boost credibility and attract users. Encourage diverse participation, whether from seasoned developers, scientists, or students, by being open to questions, feedback, and contributions of varying levels. |
| 8. **Ensure long-term maintenance and evolution.** Provide a roadmap that outlines planned features, updates, or long-term project goals. This helps maintainers and contributors stay aligned and gives users confidence in the project’s development. Foster a healthy, engaged community by recognizing contributors, hosting hackathons or sprints, and encouraging new ideas. Consider a governance model where a core group of maintainers or a steering committee manages long-term development, ensuring that the project's mission endures even as individual contributors come and go. |
| 9. **Monitor and measure success.** Track metrics like repository stars, downloads, citations, or code contributions to gauge adoption and impact. Regularly collect user feedback and address concerns or feature requests to ensure the project stays relevant and useful to its audience. |
| 10: **Stable DOIs.** To address the challenge of license changes and code changes from public to private after publication; OSS projects should create permanent records on archival platforms like Zenodo, Figshare, or Software Heritage, which provide DOIs for long-term citation and access. These platforms integrate with GitHub for automated archival, ensuring enduring accessibility to the community. |

[W: Open to discussion. Please carefully double-check whether these steps make sense and that I haven't forgotten anything.] [B: 7-9 is often not possible in our current funding system - we should make clear that the first bullet points are a must have and the last 3 are a goal][M: A major problem is that there are very very few examples of this in proteomics ... there are a handful tops. I think this needs to be toned down a lot. This should be a goal but the funding agencies have to be supportive of this first. The issue is that the NIH doesn't want to fund open source software development and they definitely don't want to fund repositories.

## Licenses in proteomics software

Before we delve into the role of OSS in computational proteomics, we would like to highlight one of the fundamental aspects and challenges in the development of proteomics software: the use of software licenses.
These licenses often target commercialization, code reuse, but also distribution and citation. 

As the gold standard for proteomics software development, we recommend to use a standard OSS license (**Figure 1**) like Apache 2.0, MIT, BSD, LGPL, GPL, etc.; a list of them can be found at (https://opensource.org/licenses).
These licenses are well known, are in use across many fields, and are well understood by the community.
Additionally, they are compatible with the FAIR principles and the Open Source Initiative (OSI) guidelines [REF].
These established licenses all have a clear definition of what is allowed and what is not, and how the software can be distributed, reused, and cited.

![jpr_oss_license](fig/jpr_oss_license.png)
**Figure 1.** Open source software licenses in use in proteomics. Scientific papers published in the _Journal of Proteome Research_ that include a GitHub URL in their abstract were automatically retrieved from PubMed and information on the software license of the corresponding GitHub repository was retrieved through the GitHub API.
Many proteomics code repositories do not have a license specified, in addition to several OSS licenses being used.
The code to generate these data is available at https://gist.github.com/bittremieux/70905e5d9dcc829ae49aab49e85954af.
[M: we need to point out that without a specified license it isn't open source. Without a specified license the software and contributions are exclusively owned by the authors and no one can use, copy, or distribute the contributions. I also think it is important to point out the legitimate concerns some institutions, like UW, have for Apache 2.0. Also, the problems of GPL, AGPL, and LGPL in discouraging use. Many in the MS community don't understand open source licenses and this might be an opportunity to explain them.]

In addition, as the field is evolving, and software becomes more complex and has multiple components, different components could have a different license and the dependencies between them should be clearly stated.
It is therefore recommended to clearly state the dependencies that a piece of software might have and the licenses of each of them.
This will help the user to understand the software, the developers to know what they can use, and the journal reviewers to understand the software and its implications.
For example, if a software tool that performs PTM-site localization is distributable, but the software that produces the PTMs, peptide identification inputs, etc., is not, it could be misunderstood that the software is open-source, when in reality, all the main components that it relies on are not.
Full disclosure of such dependencies is necessary to ensure that the user is aware of this, such that the community, developers, and journal reviewers are able to understand this challenge.

## Strategies to commercialize OSS

A piece of software being open-source does not necessarily mean that everyone can use it without financial cost. [B: that sentence could be misunderstood I think.]
Instead, OSS can be commercialized in a number of different ways depending on the owner's goals and principles.
Here, we intend for commercialization to refer to any process by which OSS is monetized, regardless of whether it remains part of an academic lab, is developed by a company, or is spun-out into its own startup.
In fact, we would argue that healthy OSS projects must be financially supported by methods such charitable means, grants, or commercialization, in order for the development of the project to be sustainable.
We discuss a few commercialization models that have become popular with OSS, which try to strike a balance between supporting openness and supporting future development.
It is worth noting that these strategies are not necessarily mutually exclusive.

**Dual licensing.**
A popular commercialization option for OSS has been to offer the software under multiple licenses.
Projects using this strategy are often available under a strong copyleft license (GPL, AGPL, etc.) with no financial cost.
However, the copyleft nature of these licenses requires any derivative works to be published under a compatible open-source license, which is often undesirable for corporate users.
Thus, these projects also offer more permissive licenses to paying customers, which allows using the OSS project within proprietary code.
Although this strategy may seem easy to abuse, our experience has been that companies are often risk-averse and would rather purchase proper licenses rather than risk legal ramifications of violating a copyleft license. 
A successful example of this strategy from outside of proteomics has been RStudio by Posit.
RStudio is currently available under an open-source AGPLv3 license, or under a commercial license when AGPLv3 is incompatible.
Notably, developers should make sure to include a "contributor license agreement" as part of their requirements for new contributors to ensure their contributions can be distributed under both licenses.

**Support or services.**
Some OSS projects commercialize by offering support services or new feature development at a cost.
Often users, particularly from corporate entities, are willing to pay for specialized training and ongoing support for their use of OSS projects.
In special instances, it may even be the case that outside entities are able to pay for the prioritization of specific features.
This road must be tread carefully though; while there is benefit to allowing sponsored features, and they do benefit everyone once implemented, such a model risks losing control over the direction of an OSS project.
Red Hat is the most prominent example of a company using this strategy to commercialize their enterprise Linux offering. 

**Software as a service (SaaS).**
The SaaS commercialization model has become increasingly popular in recent times. 
When using a SaaS model, the OSS project remains open-source, but commercialization occurs by building a platform around it.
The platform then allows users to more easily use the OSS project.
This model often includes a managed hardware or cloud infrastructure component, where users pay to interact with a web application to use the OSS tool, reducing the barrier to entry.
In the bioinformatics space, NextFlow [28398311] is an open-source bioinformatics workflow engine that has been commercialized by Seqera Labs using the SaaS model. [please check if they are earning money or if they still rely on venture capital]
Their current Seqera Platform product provides an interface to launch, observe, and explore workflow executions with NextFlow, in addition to other features. 

**Open-core.**
The open-core commercialization model provides access to new features only to paying customers.
Often this is not fundamental functionality, but rather optional features such as a nicer user interface or early access to new features.
Some variants of this model use a time delay for new features, where paying users have access to new features sooner than those using the fully OSS version.
Practically, the implementation of this strategy often involves the creation of a private, upstream fork of the OSS code repository.
New features are then added to the private fork and synced to the OSS version at a later date.
Such a strategy can also be used by academic labs looking to protect new features while preparing for publication, although we would advocate for developing those features in the open, when possible. [can we provide reasoning here? I think it might delay progress and issues with commitment to making it public?]
The open-core model is quite common and in proteomics it is used for ScaffoldDIA from Proteome Software: the open-source core of ScaffoldDIA is EncyclopeDIA [30510204]. [M: also I believe Scaffold makes use of Comet and X!tandem]

## The role of closed-source software

Is proprietary, closed-source software ever appropriate in scientific research?
We believe the answer to be yes, particularly when the software in question is not the subject of research. [Preferably any proteomics software will try to have biology in mind, right? I find it a bit vague where this boundary exactly is, can we define it with a bit more detail?] [B: I would say no. Public funded software, should be open.]
Indeed, there is great commercial opportunity to build proprietary software from OSS.
Although an OSS project may introduce a new algorithm or model to the scientific world, there are often improvements that can be made to the software regarding usability, scaling, and efficiency, all of which may require commercial investment.
Indeed, proprietary software can serve researchers well when they are most interested in using a tool to answer biological questions, rather than seeking to understand or benchmark the underlying algorithm. [JKE: this confuses me in the context of this OS manuscript. And if it confuses me, it's going to confuse anyone skeptical of the manuscript goals as it's sending a mixed message. I read it as it's ok to have proprietary software whether a derivative of OSS or not. I think it's worth clarifying under what context it's OK and I'm not sure the existing text covers this adequately.]

Perhaps more controversial is the idea of a company creating proprietary software that incorporates OSS, yet the OSS project was created by an unaffiliated academic lab.
Provided that the company is abiding by the terms of the OSS license, this is a legitimate use of the original OSS project.
However, if this is problematic for an OSS project, we would recommend looking into the strong copyleft licenses and/or adopting the dual licensing strategy that we previously discussed.
Regardless, it is important to remember that nearly all modern software builds upon foundational OSS that are often taken for granted.

[We could also add a very short section about data reuse in AI/ML/DL models, especially how this is questionable when close-sourcing the model or the code. Not even sure if this works with e.g., the PRIDE license/agreement]

## Concluding remarks

As proteomics research increasingly relies upon computational tools, embracing open-source and FAIR principles is essential for ensuring transparency, reproducibility, and accessibility.
We urge researchers, funding agencies, institutions, and companies to prioritize open-source and FAIR practices, especially in publicly funded work, to create a truly collaborative scientific ecosystem.
By collectively advancing open-source software, the scientific community can build an inclusive, rigorous foundation that fosters innovation and extends the benefits of research to scientists and the public alike.
As we venture into the future, we as a community should explore mechanisms to make OSS sustainable---for example, by creating a foundation for proteomics software to support the maintenance of OSS in our field.

[B: agreed, but, we also need to start paying for OSS. Who is paying for gitlab, dockerhub, nextcloud etc at the moment? If we as a community don't start to pay, such a foundation is useless.][M: a major problem was covered in this paper, https://pubs.acs.org/doi/10.1021/acs.jproteome.8b00015 ... most people don't trust open source and free software.]

Regardless, let us come together and commit to open science for a shared, sustainable future in our exploration of the proteome.

## Conflicts of interest

WEF is an employee of Talus Bioscience, a drug-discovery biotechnology company that develops and contributes to OSS and does not currently sell software.
Additionally, Talus Bioscience has a collaborative research agreement with Bruker.
T.S. is an officer in OpenMS Inc., a non-profit foundation that manages the international coordination of OpenMS development.

### Authors

| Name | Email | Affiliation |
|------|-------|-------------|
|Yasset Perez-Riverol | yperez@ebi.ac.uk | EMBL-EBI |
|William E. Fondrie | wfondrie@talus.bio | Talus Bioscience |
|Timo Sachsenberg | timo.sachsenberg@uni-tuebingen.de | University of Tübingen |
|Robbin Bouwmeester | robbin.bouwmeester@ugent.be | VIB-UGent |
|Wout Bittremieux | wout.bittremieux@uantwerpen.be | University of Antwerp |
