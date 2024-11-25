# Open—Source and FAIR Research Software in Proteomics

## Introduction

Research software is essential to modern science, with the majority of scientists recognizing it as indispensable for their work and often impossible to conduct research without it [28751965, https://zenodo.org/records/14809].
This reliance on software is equally crucial in proteomics, where researchers depend on a range of tools and algorithms for every step, from mass spectrometer configuration and data acquisition to the subsequent stages of processing, analysis, and interpretation [23467006, 34906327].

Since the original publication of the first peptide identification tool, SEQUEST [24226387], proteomics software has evolved into a sophisticated ecosystem encompassing multiple stages of data processing, advanced predictive models, and robust computational frameworks.
The publication of SEQUEST exemplifies a subsequent reoccurring pattern in MS-based proteomics; the development of software drives the adoption of novel experimental methodology. 
Numerous examples of open-source software tools are developed and used by the proteomics community. These include tools like Percolator [17952086], which is used to improve peptide and protein identification using machine learning, Prosit [31133760], which applies deep learning to predict fragment ion intensities, aiding in more accurate spectra matching, and Proteowizard [23051804] that has been providing shared libraries and tools for data access. Platforms like GalaxyP [29092937], or quantms [38965444] facilitate accessible, reproducible analyses through high-performance computing (HPC) and distributed workflows, supporting researchers in handling large datasets and complex analyses.
Together, these advances underscore how proteomics software has transformed into a multidisciplinary field, in a complex ecosystem of algorithms, models, and software tools requiring sophisticated computational and algorithmic expertise.

Computational proteomics, along with algorithm and software development, faces several key challenges common to other omics fields:

- The increasing complexity and size of data acquired by mass spectrometers, the complex sequence of steps, including spectral processing, statistical analysis, and biological interpretation, along with the need to manage algorithmic details and parameter settings, all contribute to making software development in proteomics a complex and demanding endeavor.
  
- Although most software tools are described in publications, the absence of open-source code, comprehensive documentation, and version control often impedes reproducibility and reuse. Such lack of transparency impedes researchers from extending existing algorithms and adapting software to keep pace with rapidly advancing instrumentation and acquisition methods. Transparency is especially important during the relatively frequent significant shifts in data processing paradigms, like the rapid adoption of data-independant acquisition over data-dependant acquisition.
  
- Ensuring reproducibility is a challenge due to the limited access to detailed algorithmic information, which hinders validation and extension of methods.

- Custom licenses and restrictions on software distribution can further complicate the situation, making it difficult to share, modify, or redistribute software, and hindering the development of a collaborative and open-source ecosystem.
 Proteomics software is often distributed under restrictive licenses and tailored to specific platforms (e.g., operating systems, computer architectures), limiting its use across diverse environments and services. Not surprisingly, such restrictive licenses restrict the field’s adaptability and hinder the integration of proteomics with other omics disciplines.

- Complex workflows and high-throughput data analysis are growing in proteomics [29092937, 38965444, 36648445]. Such complexity is complicated on its own because it requires managing dependencies, configurations, and environments consistently across diverse systems and architecture without human intervention.
 The community has tackled this challenge with CI/CD pipelines as, for example, described in 10.1101/gr.276963.122, but this relies on OSS and the permission to freely redistribute software along the entire dependency chain.
 If one piece in this supply chain is not OSS, exceptions need to be handled, and automation is harder or impossible.
 In sum, it creates a huge additional burden for the entire community downstream of the non-OSS software package, which on its own is a hidden cost.

- The lack of standardization in proteomics software development, including inconsistent documentation, variable code quality, and limited community engagement, can hinder the adoption and use of software tools, leading to inefficiencies and redundancies in software development.

- Closed-source, platform-specific software has caused lock-in effects, restricting users to specific tools and hindering innovation. 
Until recently, major instrument vendors lacked open-source, cross-platform libraries for data access, limiting data reuse and algorithm development. 
Thermo Fisher's RawFileReader library marks progress, enabling tools like ThermoRawFileParser [31755270] and PRIDE Archive USI [39494541,34183830]. This idea has been recently extended for Bruker timsTOF data with the timsrust library (https://github.com/MannLabs/timsrust/), which is open-source and already used by tools like Sage.

A solution to these challenges is offered by open-source software (OSS) which is also aligned with the FAIR Principles (Findable, Accessible, Interoperable, Reusable), initially established for scientific data [26978244]. FAIR principles were expanded in 2022 for research software (FAIR4RS) to address the growing recognition of research software as a foundational research asset [36241754]. Following FAIR4RS principles empowers proteomics with OSS tools that are not only accessible but also foster community-driven development, rigorous validation, and transparent sharing of methodologies [37768885, 36241754]. 
Although OSS is not an explicit requirement for implementing FAIR principles, it greatly facilitates the realization of these principles by making software more accessible, transparent, and reusable. 
OSS has demonstrated clear benefits in increasing the accessibility, usability, and visibility of scientific software [30212065].
OSS makes reproducibility, traceability and auditability possible.
With code freely available for inspection, modification, and distribution, OSS encourages collaboration and creates avenues for continuous improvement-factors that are critical in fields as data-intensive as proteomics.

In this manuscript, we aim to explore the role of OSS in computational proteomics and its implications for the development of FAIR research software.
We will discuss the benefits and challenges of OSS in proteomics, the role of OSS in the development of FAIR research software, and the importance of distribution, licensing, and citation of software in computational proteomics.
We will also explore how other omics fields deal with OSS and FAIR software and how these experiences can inform the development of proteomics software.
Our goal is to present a vision for a future where OSS and FAIR software are encouraged and supported in the proteomics community.

## What does it mean for software to be "open-source"?

### Attributes of an open-source project

Open-source software (OSS) is defined by its publicly accessible source code, allowing anyone to view, modify, and distribute it under an Open Source Initiative-approved license. Merely making source code available is not enough; licenses that restrict use or modification to specific fields (e.g., non-commercial use) do not qualify as open-source. Unlike closed-source, OSS guarantees transparency, fostering trust, collaboration, and scientific progress. To address misconceptions in proteomics, we aim to clarify for the community (users, developers, and reviewers) the essential criteria for OSS (https://opensource.org/osd):

- **Source Code Availability**: The source code—the instructions that define how software functions — is publicly accessible, allowing anyone to view, download, and examine the code’s details (https://opensource.org/osd).

- **OSI-Approved License**: The software must use an Open Source Initiative-approved license, which specifies rights to freely use, modify, and distribute the software, regardless of its application or environment (https://opensource.org/licenses).

- **Freedom to Modify and Distribute**: Open-source software, in contrast to source-available software, allows users not only to access the code but also to modify it and share these modifications, encouraging innovation and collaboration.

- **Transparency and Community Trust**: With open-source, the code is transparent by design, allowing the community to understand, verify, and contribute to the project. This fosters trust and credibility, especially crucial in scientific fields.

- **Collaborative Development**: Open-source projects are often maintained by communities or dedicated teams, and they welcome contributions, such as bug reports, enhancements, and new features, from a diverse group of users and developers.

- **Long-term Reliability**: Because the code is publicly accessible, open-source projects are less dependent on single organizations or developers, promoting continuity and stability even if original contributors leave.

- **No Restriction to Specific User Groups**: Unlike “free-for-academic-use” licenses, which restrict usage to academic settings, open-source licenses do not impose limitations on the types of users or institutions that can access or use the software.

- **Not Necessarily Free of Cost**: Open-source software is “free” in terms of freedom, not necessarily in terms of price. Users might pay for support, hosting, or additional services, but they retain freedom in how they use and modify the software.

### Misconceptions about open-source

In proteomics, and bioinformatics in general, multiple misconceptions exist about open/closed source software:

- Cost-free software is not always open-source. Many programs are freely available for non-commercial or academic use but do not meet open-source criteria. Similarly, "free and open-source software" (FOSS) refers to the freedom to run, modify, and share the software, not necessarily its financial cost. FOSS may involve expenses for services like support or hosting, but it ensures users retain the freedom to use, adapt, and distribute the software as they wish (https://www.gnu.org/philosophy/free-sw.html).
- Academic licenses only refer to free-for-academic-use. The source code is not necessarily open, shareable, or modifiable. Even the term "academic" is not well-defined as it can refer to a wide range of institutions and organizations. To simplify this complexity, we can define OSS as any software that uses an license approved by the Open Source Initiative (OSI, https://opensource.org/licenses).
- Accessible source code does not mean open-source. Open-source software does not only mean that the source code is available but that it is allowed to be freely modified and shared regardless of whether the users work in academia or commercial settings.
- Open-source software does not imply lack of professional quality. Many open-source projects are maintained by dedicated teams with robust testing and good programming practices. In genomics, projects like samtools (https://github.com/samtools/samtools) [19505943], an MIT-licensed project with over 80 contributors and 50,000+ citations, and the Genome Analysis Toolkit (GATK, https://github.com/broadinstitute/gatk) [20644199], now open-source with over 100 maintainers and 26,000+ citations, exemplify this standard. In proteomics, Percolator (https://github.com/percolator/percolator) [17952086] has over 700 citations and 20 contributors, serving as a core tool for projects like MS2Rescore [35803561], OpenMS [38366242], and Crux [36598107]. Other successful open-source projects in proteomics, such as OpenMS [38366242], Skyline [20147306], PeptideShaker [25574629], and ProteoWizard [23051804], demonstrate the benefits of transparency and collaboration. Despite these successes, academic open-source proteomics software is still perceived as lower quality. In 2018, Rob Smith highlighted the community’s concerns about academic proteomics and metabolomics software, including poor documentation, lack of transparency, and limited support [29546988], though much of this feedback was directed at academic and free-for-academic-use software, not necessarily open-source software.

### Detrimental practices in using public repositories

In addition to the described misconceptions and complexity, many journals and some funding agencies mandate code availability as part of publishing, which has prompted multiple bad practices from software developers and bioinformaticians aiming to fulfill these requirements. Notable examples include:

- **Open-source Facade**: Researchers may upload closed-source software to platforms like GitHub, giving an impression of openness with features such as issue tracking, while the actual source code remains inaccessible. Although often well-intentioned, this practice can mislead scientists and, in our view, should be discouraged. In these instances, a clear statement in the repository should indicate to the users that the software is not open source.
- **Alterations Post-Publication**: Software is deposited in GitHub as open-source during the submission of the manuscript, but after publication, software licenses in GitHub repositories are changed, or repositories are deleted or made private, all of which complicates efforts to ensure long-term accessibility.
- **License Misuse or Ambiguity**: Some repositories may use inappropriate or ambiguous licenses, causing confusion about the terms of use, distribution, and modification (more details discussed in the section Licenses in proteomics software).
- **Obscure Dependencies**: Software repositories may have dependencies that are not clearly documented, which may require closed-source or proprietary software. This can create barriers for other researchers attempting to run or build on the software, as they may not have access to necessary components or may need to purchase expensive licenses. Clear documentation of all dependencies along their licensing terms is essential to ensure transparency and reproducibility.

## Licenses in proteomics software

We want to emphasize a fundamental aspect and challenge in proteomics software development: the choice of software licenses. Licenses serve as the foundation for defining key aspects of software, including commercialization, code reuse, distribution, and proper citation.

As the gold standard for proteomics software development, we recommend to use a standard OSS license like Apache 2.0, MIT, BSD, LGPL, GPL, etc.; a list of them can be found at (https://opensource.org/licenses).
These licenses are well known, are in use across many fields, and are well understood by the community.
Additionally, they are compatible with the FAIR principles and the Open Source Initiative (OSI) guidelines [36241754].
These established licenses all have a clear definition of what is allowed and what is not, and how the software can be distributed, reused, and cited.

Many proteomics code repositories do not have a software license specified, in addition to several OSS and non-OSS licenses being used (**Figure 1**).
It is important to note that without a specified license the software is not open source, as in this case the software and contributions are exclusively owned by the authors, and no one can use, copy, or distribute the contributions.
Given the largest category of source code for proteomics tools have unspecified licenses suggests a misunderstanding of software licensing.

![jpr_oss_license](fig/jpr_oss_license.png)
**Figure 1.** Software licenses in use in proteomics.
Scientific papers published in the _Journal of Proteome Research_ that include a GitHub URL in their abstract were automatically retrieved from PubMed and information on the software license of the corresponding GitHub repository was retrieved through the GitHub API.
The code to generate these data is available at https://gist.github.com/bittremieux/70905e5d9dcc829ae49aab49e85954af.

In addition, as the field is evolving, and software becomes more complex and has multiple components, different components could have different licenses and the dependencies between them should be clearly stated.
It is therefore recommended to clearly state the dependencies that a piece of software might have and the licenses of each of them. Full disclosure of such dependencies is necessary to ensure that the user is aware of this, such that the community, developers, and journal reviewers are able to understand this challenge.

## Why open-source software is essential for scientific research

### Transparency promotes scientific rigor

The scientific community increasingly recognizes that algorithms, while not software or tools themselves but rather the underlying steps and methodology, are becoming significant research outputs in their own right. Algorithms are no longer seen merely as tools but are valued as core research outputs, reflecting the critical steps and methodologies at the heart of scientific innovation. For example, in proteomics, the fragment-indexing approach introduced by the MSFragger algorithm [28394336] has recently been implemented in two different search engines: Sage [37819886] and Comet [10.1101/2024.10.11.617953]. This shift highlights the importance of not only software as a means of implementation but also the reproducibility and reliability of computational methods that drive new discoveries. Both algorithms and their software implementations are now held to rigorous validation and reproducibility standards, similar to those for traditional experimental data and methodology.

Transparent computational methods open doors to innovation, enabling researchers to test hypotheses, refine methodologies, and build upon one another’s work with confidence. For instance, providing open-source implementations allows the scientific community to verify methods, adapt them to new challenges, and explore alternative approaches. Consider a proteomics experiment: without details on sample preparation or instrument settings or the raw data, the final results lack reproducibility. Similarly, open-source code ensures that computational methods can be accurately understood, replicated, and extended across labs worldwide. This transparency is particularly relevant for core proteomics workflows - as demonstrated by alphaDIA [https://doi.org/10.1101/2024.05.28.596182] - where understanding the underlying algorithms of protein search engines directly impacts data interpretation and research outcomes.

When algorithms and models are shared as open-source software, they inherently uphold the FAIR principles applied to scientific data. This level of openness strengthens scientific rigor, enabling others to examine the code, replicate findings, and contribute improvements. A transparent approach to computational research, through openly available code, fosters a collaborative environment where the community can validate results and improve tools, ultimately building trust in computational methodologies.

Moreover, open-source implementations guard against unintended variation in outcomes caused by minor differences in coding practices, dependencies, or hardware environments. Even small programming choices can lead to significant changes in results. Open code mitigates these risks by making the entire process visible, allowing other scientists to understand the nuances and make informed adjustments. Transparency is key in computational research, not just for ensuring rigor but for building a reliable foundation that drives the entire field forward.

Finally, open-source code allows researchers to apply and compare different implementations, revealing assumptions and enhancing understanding. For instance, discrepancies between implementations of common tools, such as variations in BLOSUM matrices for sequence alignment[18327232], demonstrate how essential code transparency is for ensuring scientific consistency. Open-source practices thus empower researchers to expand on established methods with confidence, propelling science toward more robust, reproducible, and innovative outcomes.

### Shared knowledge pushes the field forward

Open-source software (OSS) fosters a collaborative ecosystem where researchers across institutions can freely contribute, refine, and extend tools, accelerating scientific progress.
Unlike proprietary software that confines advancements to specific labs or companies, OSS allows researchers to rapidly build on each other’s work without duplicating efforts, promoting efficient resource use and transforming individual achievements into collective gains.
This is particularly vital in proteomics, where bioinformatics is integral to every workflow, and progress depends on the synergy between wet-lab experimentation and computational innovation. Exdending and building on top of existing algorithms is crucial for scientific progress.

Proteomics has greatly benefited from this open-source approach.
Projects like ProteoWizard [18606607,23051804], with tools such as Skyline [20147306] and msConvert [28188540], exemplify OSS’s impact.
Skyline, for instance, supports over 20 external plugins available in its Tool Store, allowing users to perform specialized tasks far more efficiently than if they had to build solutions from scratch. Similarly, msConvert provides a standardized interface for mass spectrometry data, sparing developers the need to manage proprietary formats.
These well-supported OSS projects create a foundational infrastructure that accelerates proteomics advancements.

However, sustaining successful OSS projects in proteomics requires ongoing community engagement, which has often proven challenging.
Despite their long history, projects like ProteoWizard and Skyline see few external contributions.
Many researchers opt to develop independent tools rather than contribute enhancements within Skyline, missing opportunities for broader collaboration.
Skyline’s external tools framework, which lowers technical barriers to contributions, has helped, but much of the development remains within the original labs.

Community contributions in proteomics face barriers associated with multiple challenges. 
Developing software for proteomics demands specialized technical skills that many labs lack, especially when resources are focused on biological research rather than software engineering.
The need for continuous updates to accommodate evolving data formats and instruments also requires substantial resources.
Additionally, academic incentives often prioritize novel software creation over contributions to existing projects, further deterring collaborative development.

To create a more robust and impactful OSS ecosystem in proteomics, stronger incentives for community involvement and frameworks that support sustained collaboration are essential.
With enhanced incentives, collaborative frameworks, and dedicated resources, the proteomics community can achieve a more sustainable, widely supported, and effective ecosystem of open-source tools.

Apart from the engagement needed from the community to foster the development of open-source software, proteomics could create and sustain some of the core functionalities of the field in small libraries and tools that could be used by the entire community: for example tools like MS2Rescore [35803561] (for rescoring peptide identifications), pyOpenMS [24420968] (for Python-based proteomics functions) or spectrum_utils [31809021] (for spectral data manipulation).

### The community can contribute to development

One of the greatest strengths of open-source software is that "given enough eyeballs, all bugs are shallow" (http://www.catb.org/~esr/writings/cathedral-bazaar/cathedral-bazaar/ar01s04.html). 
Many of the critical pieces of software that underpin the modern technology stack are open-source: Linux powers operating systems across the globe, Chromium serves as the foundation for multiple web browsers, PostgreSQL is a backbone of data storage, and Python and PyTorch have revolutionized machine learning and data science. Bringing this open-source ethos to proteomics holds the potential to accelerate advancements in the field, creating tools that are not only robust but also accessible to a global community of researchers.

Bugs and mistakes are inevitable in complex software, but collaborative scrutiny allows them to be addressed more efficiently. In proteomics, as in other scientific fields, the diverse expertise of the community enhances both the quality and the utility of open-source tools. Users who encounter issues or limitations often provide feedback, suggest solutions, or even contribute code to address the challenges, fostering continuous improvement. In our own work, users have uncovered bugs that we subsequently corrected, or asked questions about the underlying code that led to new features, fewer bugs, and more efficient algorithms.

This feedback loop is unique to OSS, where the contributions from the community enhance the quality and precision of the software over time.  Compared to proprietary software, OSS can often move faster and defray development costs by enabling users to build and contribute the features they need, rather than hoping that the maintainers of the software are willing or able to add the features themselves. This dynamic frees developers from the burden of predicting and implementing every possible use case and shifts some of the innovation to the broader community. For users, OSS reduces reliance on software maintainers, allowing research to advance even in the absence of formal support.

Without such transparency, computational research risks becoming a "black box" that stifles innovation rather than promoting it, hindering the growth of scientific knowledge.
OSS can foster a culture of shared accountability, where code is not just released but continuously scrutinized and refined, driving the field forward in a collective effort toward scientific rigor.
We have indeed observed this in our own projects: at the time of writing, quantms [38965444] and mokapot [33596079] now have 12 and 13 contributors, respectively.

## Open source and ML/AI models in proteomics

Machine learning and deep learning are increasingly used in proteomics, with examples like the MS2 prediction model MS2PIP [37140039] and the peptide _de novo_ sequencing models Casanovo [39080256] and InstaNovo [https://www.biorxiv.org/content/10.1101/2023.08.30.555055v3]. Many deep learning-based proteomics tools enhance reproducibility by clearly reporting source code, training parameters, and other details. While closed-source tools have contributed to research, their models may carry bias, and their potential usefulness can be hard to assess when code and models are not accessible. A more contentious issue arises when closed-source or commercial models are trained on publicly shared community datasets, often under open-source licenses.

Open-source software has proven its value by removing barriers to learning, sharing, and improving systems. For AI in proteomics, society needs similar freedoms: autonomy, transparency, ease of reuse, and collaborative improvement. The Open Source Initiative's Open Source AI Definition (OSAID) outlines these freedoms:

- Use the system for any purpose.
- Study how the system works and inspect its components.
- Modify the system, including changing its output.
- Share the system, with or without modifications, for any purpose.

AI and machine learning are more than software-they encompass data, configurations, documentation, and new artifacts like model weights and biases. Open source should apply to the entire system, including models, parameters, and structural elements. However, it is unclear what mechanisms or licenses ensure that these models, particularly their parameters, are freely available for use, research, modification, and sharing. We recommend clear assertions accompanying parameter distribution to ensure they remain freely accessible.

## Increasing emphasis on open science and open source by funding agencies

As open science gains prominence, major funding agencies worldwide are implementing mandates to ensure that software developed with public funds is openly accessible.
Horizon Europe, the European Commission's flagship research program, has set stringent requirements for open science, mandating that research outputs, including software, are shared under open or free licenses aligned with FAIR principles (https://commission.europa.eu/about-european-commission/departments-and-executive-agencies/digital-services/open-source-software-strategy_en).
Additionally, all Horizon Europe funded research is required to establish a data management plan (DMP), which is a structured document that outlines plans for open software and code sharing, including tools needed for interoperability.
In the United States, agencies like the National Institutes of Health (NIH) and the National Science Foundation (NSF) strongly encourage, and in some cases require, software and code sharing through public repositories, aiming to maximize reproducibility and scientific transparency (https://datascience.nih.gov/tools-and-analytics/best-practices-for-sharing-research-software-faq).
Similarly, the Wellcome Trust in the United Kingdom mandates that all research outputs, such as software integral to funded research, be made freely available under recognized open-source licenses to facilitate widespread accessibility and reuse (https://wellcome.org/grant-funding/guidance/policies-grant-conditions/data-software-materials-management-and-sharing-policy).
Many other funding agencies all over the world have similar open source guidelines and mandates.
This underscores a commitment from funders to foster collaborative scientific ecosystems, democratizing access to essential research tools and enhancing reproducibility across disciplines.

## Challenges of Maintaining Open-Source Scientific Software

Open-source software (OSS) in computational proteomics offers significant benefits but also poses challenges, particularly around sustainability. 
These challenges often deter long-term commitment, with some researchers transitioning to closed-source software after facing sustainability issues. 
Below, we outline key barriers to maintaining OSS and propose strategies—both practical and aspirational—to help advance OSS in the field.

### Financial Sustainability

Maintaining an OSS project requires ongoing funding for updates, bug fixes, testing, and user support. However, funding agencies like the NIH often prioritize novelty over software maintenance, leaving many projects to become "abandonware" once the initial grants end.

- **Problem**: Without consistent funding, OSS projects in proteomics lose momentum after the initial development phase.
- **Potential Solutions**:
  - **Dedicated Maintenance Grants**: Funding agencies should create grant mechanisms for software maintenance, such as the Chan—Zuckerberg Initiative’s "Essential Open Source Software for Science" grants, and expand these options to the NIH.
  - **Commercialization Models**: OSS projects could explore commercialization, potentially leading to academic spin-offs or new revenue streams (read the section about commercialization strategies).

### Misaligned Incentive Structures in Academia

The academic incentive structure prioritizes publications and novelty, encouraging researchers to develop new software instead of maintaining existing tools. 
Contributions to OSS, especially those owned by others, are undervalued and rarely recognized in tenure or promotion evaluations.

- **Problem**: The "publish-or-perish" culture discourages OSS maintenance, as it doesn’t align with traditional academic metrics.
- **Potential Solutions**:
  - **Recognition for OSS Contributions**: Institutions and funding agencies should acknowledge OSS maintenance as valuable scholarly work, similar to publications, and include it in grant and tenure evaluations.
  - **Community-driven Publications**: Journals should accept papers on software updates, offering academic recognition for maintenance work, as seen in the Journal of Proteome Research’s Software Tools and Resources issue.

### The Challenge of Consistent Maintainers

In academic settings, many OSS projects are led by students, postdocs, or temporary researchers who eventually leave for other opportunities, often in unrelated fields.
This results in a lack of long-term maintainers, leading to project stagnation or abandonment.

- **Problem**: The reliance on transient academic positions means OSS projects are vulnerable to disruptions as contributors move on.
- **Potential Solutions**:
  - **Governance Models**: Establishing community-driven governance structures, such as steering committees or core maintainer teams, can provide continuity even as individual contributors leave.
    Notably, this kind of governance is likely only feasible for larger, well-established open-source projects.
  - **Transition Plans**: Projects should develop clear transition plans, ensuring that new maintainers can seamlessly take over.
    This could involve thorough documentation, onboarding guidelines, and mentoring new contributors.

Addressing these challenges requires a multi-pronged approach, combining changes in funding structures, academic incentives, and community engagement.
The scientific community, funding agencies, companies, and academic institutions must collaborate to ensure that OSS can continue to thrive.
By addressing these challenges head-on, we can build a more sustainable and collaborative ecosystem for open-source scientific software, ultimately driving innovation and reproducibility in proteomics research.

## How to start a gold-standard OSS project in proteomics

| Box 1. How to get started with OSS. The following steps provide a guideline that can foster a successful open-source project that grows in adoption, value, and contributions over time.                                                                                                                                                                                                                                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------------------|
| 1. **Define clear goals and scope.** Start by defining the specific problem or gap your software aims to solve. Ensure it addresses an unmet need or provides a significant improvement over existing solutions. Before starting an independent OSS project, consider contributing to an existing OSS project by evaluating if your use case could take advantage of existing frameworks. For example, adding a new feature within Skyline or OpenMS would not require using your resources for implementing a raw data reading component and a user interface.                                  |
| 2. **Choose an open source license.** Choose an OSI approved license that aligns with the project's intended use and desired level of openness. For projects that may later require commercialization or enterprise use, dual licensing (e.g., open-source with an option for commercial licensing) can be considered to support sustainability.                                                                                                                                                                                                                                                 |
| 3. **Plan for sustainability.** Research potential funding sources, such as grants, academic support, or partnerships. Decide if the project will rely on donations, grants, or if it might later incorporate paid services. If applicable, consider models like SaaS, support-based revenue, or feature-based licensing that could sustain the project without sacrificing its open-source nature.                                                                                                                                                                                              |
| 4. **Set up a well-structured repository.** Use a version-control platform like GitHub or GitLab for easy access, community contributions, and versioning. Use clear folder structures, name conventions, and modular code design to enhance usability and maintainability. Provide a clear guide on how others can contribute to the project, including coding standards, pull request policies, and a Code of Conduct to foster a positive collaborative environment.                                                                                                                          |
| 5. **Incorporate early user feedback**. Develop a prototype and engage a select group of users as beta testers than can try the software and provide feedback to ensure its usefulness and effectiveness.                                                                                                                                                                                                                                                                                                                                                                                        |
| 6. **Implement rigorous testing and quality control.** Use continuous integration/continuous deployment (CI/CD) practices to automate testing and improve code quality. Platforms like GitHub Actions can be set up to run tests on each new code addition or pull request. Develop a robust suite of tests that ensure functionality and compatibility, minimizing the risk of bugs and ensuring reliability. Regularly review code for quality and potential improvements, inviting experienced contributors or external collaborators to audit the code.                                      |
| 7. **Develop thorough documentation.**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| - User documentation: Provide tutorials, installation guides, and usage examples that lower barriers to entry for new users.                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| - Developer documentation: Include technical details that make it easier for new developers to understand the codebase, contribute, and debug.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| - Version control and changelog: Maintain a detailed changelog for tracking updates, and consider using semantic versioning for releases to help users track changes and updates.                                                                                                                                                                                                                                                                                                                                                                                                                |
| 8. **Build a community.** Create forums, mailing lists, or a Slack channel to facilitate communication and support for users and contributors. Promote the project within academic and industry circles, social media, or conferences. Collaborations with other researchers can boost credibility and attract users. Encourage diverse participation, whether from seasoned developers, scientists, or students, by being open to questions, feedback, and contributions of varying levels.                                                                                                     |
| 9. **Ensure long-term maintenance and evolution.** Provide a roadmap that outlines planned features, updates, or long-term project goals. This helps maintainers and contributors stay aligned and gives users confidence in the project’s development. Foster a healthy, engaged community by recognizing contributors, hosting hackathons or sprints, and encouraging new ideas. Consider a governance model where a core group of maintainers or a steering committee manages long-term development, ensuring that the project's mission endures even as individual contributors come and go. |
| 10. **Monitor and measure success.** Track metrics like repository stars, downloads, citations, or code contributions to gauge adoption and impact. Regularly collect user feedback and address concerns or feature requests to ensure the project stays relevant and useful to its audience.                                                                                                                                                                                                                                                                                                    |
| 11: **Stable DOIs.** To address the challenge of license changes and code changes from public to private after publication; OSS projects should create permanent records on archival platforms like Zenodo, Figshare, or Software Heritage, which provide DOIs for long-term citation and access. These platforms integrate with GitHub for automated archival, ensuring enduring accessibility to the community.

## Strategies to commercialize OSS

A piece of software being open-source does not necessarily mean that it doesn't cost to be maintained, run it and developed. Because of this, strategies to commercialize OSS have been developed to ensure that the software can be maintained and developed in the long term.
OSS can be commercialized in a number of different ways depending on the owner's goals and principles.
Here, we intend for commercialization to refer to any process by which OSS is monetized, regardless of whether it remains part of an academic lab, is developed by a company, or is spun-out into its own startup.
In fact, we would argue that healthy OSS projects must be financially supported by methods such charitable means, grants, or commercialization, in order for the development of the project to be sustainable.
We discuss a few commercialization models that have become popular with OSS, which try to strike a balance between supporting openness and supporting future development.
It is worth noting that these strategies are not necessarily mutually exclusive.

**Dual licensing.**
A popular commercialization option for OSS has been to offer the software under both a strong copyleft license (like GPL or AGPL) and a more permissive commercial license. The code itself is typically the same for both license types. The difference lies in how the code can be used, modified, and redistributed depending on the license under which it is acquired.
Projects using this strategy are often available under a strong copyleft license (GPL, AGPL, etc.) with no financial cost.
However, the copyleft nature of these licenses requires any derivative works to be published under a compatible open-source license, which is often undesirable for corporate users.
Thus, projects also offer more permissive commercial licenses to paying customers, allowing them to use the OSS project within proprietary code.
Although this approach may seem prone to abuse (e.g., improper use of GPL code), our experience has been that companies tend to be risk-averse and prefer purchasing proper licenses to avoid the legal consequences of violating a copyleft license.
A successful example of this strategy from outside of proteomics has been RStudio by Posit.
RStudio is currently available under an open-source AGPLv3 license, or under a commercial license when AGPLv3 is incompatible.
Notably, developers should make sure to include a "contributor license agreement" as part of their requirements for new contributors to ensure their contributions can be distributed under both licenses.

**Support or services.**
Some OSS projects commercialize by offering support services or new feature development at a cost.
Often users, particularly from corporate entities, are willing to pay for specialized training and ongoing support for their use of OSS projects.
In special instances, it may even be the case that outside entities are able to pay for the prioritization of specific features. For example, the major mass spectrometry instrument vendors have been providing financial support to both the Skyline and Proteowizard projects to ensure features, support, and documentation are provided for their customers.
This road must be thread carefully though; while there is benefit to allowing sponsored features, and they do benefit everyone once implemented; such a model risks losing control over the direction of an OSS project. Features added to Skyline from a vendor are made available to all vendors if they have compatible instrumentation. 
Red Hat is the most prominent example of a company using this strategy to commercialize their enterprise Linux offering. 

**Software as a service (SaaS).**
The SaaS commercialization model has become increasingly popular in recent times.
When using a SaaS model, the OSS project remains open-source, but commercialization occurs by building a platform around it.
The platform then allows users to more easily use the OSS project.
This model often includes a managed hardware or cloud infrastructure component, where users pay to interact with a web application to use the OSS tool, reducing the barrier to entry.
In the bioinformatics space, NextFlow [28398311] is an open-source bioinformatics workflow engine that has been commercialized by Seqera Labs using the SaaS model.
Their current Seqera Platform product provides an interface to launch, observe, and explore workflow executions with NextFlow, in addition to other features.

**Open-core.**
The open-core commercialization model provides access to new features only to paying customers.
Rather than essential functionality, this refers to optional features such as a nicer user interface or early access to new features.
Some variants of this model use a time delay for new features, where paying users have access to new features sooner than those using the fully OSS version.
Practically, the implementation of this strategy often involves the creation of a private, upstream fork of the OSS code repository.
New features are then added to the private fork and synced to the OSS version at a later date.
Such a strategy can also be used by academic labs looking to protect new features while preparing for publication and until a manuscript is accepted. Although we advocate for developing those features in the open, we recognize that there are instances where this is not practical. For example, when a junior researcher is publishing a novel algorithm, they may want to avoid the risk of having their work preempted by others. Similarly, collaborators may request that the software be kept private to prevent other researchers from using it and publishing their findings first. While we believe that these situations are rare in the proteomics community, they could lead to the original researchers losing recognition and credit for their work.
The open-core model is quite common, and in proteomics it is used for ScaffoldDIA from Proteome Software: the open-source core of ScaffoldDIA is EncyclopeDIA [30510204]. 


## Concluding remarks

As proteomics research increasingly relies upon computational tools, embracing open-source and FAIR principles is essential for ensuring transparency, reproducibility, and accessibility.
We urge researchers, funding agencies, institutions, and companies to prioritize open-source and FAIR practices, especially in publicly funded work, to create a truly collaborative scientific ecosystem.
By collectively advancing open-source software, the scientific community can build an inclusive, rigorous foundation that fosters innovation and extends the benefits of research to scientists and the public alike.
As we venture into the future, we as a community should explore mechanisms to make OSS sustainable-for example, by creating a foundation for proteomics software to support the maintenance of OSS in our field.
Importantly, an emphasis on creating software that is scalable, easy to deploy, and integrates complex functionalities beneath an easy-to-navigate interface is paramount to ensure its widespread adoption and success [38438732]. Providing software that is accessible to end-users is a way to address the issues related to the negative perception of the quality of academic or OSS in mass spectrometry [29546988]. Additionally, we expect that AI-assisted software development will significantly improve the quality of proteomics OSS, by automating error detection, optimizing code performance, and enhancing feature integration, thereby increasing reliability and user satisfaction.
Regardless, let us come together and commit to open science for a shared, sustainable future in our exploration of the proteome.

## Conflicts of interest

WEF is an employee of Talus Bioscience, Inc, a drug-discovery biotechnology company that develops and contributes to OSS and does not currently sell software.
Additionally, Talus Bioscience has a collaborative research agreement with Bruker.
T.S. is an officer in OpenMS Inc., a non-profit foundation that manages the international coordination of OpenMS development.
MRL is an employee of Belharra Therapeutics, Inc., and an officer of Chaparral Labs, Inc., a company offering SaaS solutions for proteomics, in addition to commercial support for OSS software. 
JVG is an employee of InstaDeep Ltd.
The MacCoss Lab at the University of Washington receives funding from Agilent, Bruker, Sciex, Shimadzu, Thermo Fisher Scientific, and Waters to support the development of Skyline, an open source software tool for quantitative proteomics. MJM is a paid consultant for Thermo Fisher Scientific.

### Authors

| Name                 | Email                             | Affiliation                             | ORCID |
| -------------------- | --------------------------------- | --------------------------------------- |-------|
| Yasset Perez—Riverol | yperez@ebi.ac.uk                  | EMBL—EBI                                |
| William E. Fondrie   | wfondrie@talus.bio                | Talus Bioscience                        |
| Timo Sachsenberg     | timo.sachsenberg@uni—tuebingen.de | University of Tübingen                  |
| Robbin Bouwmeester   | robbin.bouwmeester@ugent.be       | VIB—UGent                               |
| Wout Bittremieux     | wout.bittremieux@uantwerpen.be    | University of Antwerp                   |
| Aivett Bilbao        | aivett.bilbao@pnnl.gov            | PNNL—EMSL                               |
| Chengxin Dai         | chengxin2024@126.com              | Beijing Proteome Research Center        |
| Daniel S. Katz       | d.katz@ieee.org                   | University of Illinois Urbana—Champaign |
| Lukas Käll           | lukas.kall@scilifelab.se          | KTH—Royal Institute of technology       | 0000-0001-5689-9797 |
| Michael R. Lazear    | mlazear@belharratx.com            | Belharra Therapeutics                   |
| Michael J. MacCoss   | maccoss@uw.edu       | Department of Genome Sciences, University of Washington 
| Georg Wallmann       | wallmann@biochem.mpg.de           | Max Planck Institute of Biochemistry    |
| Jeroen Van Goey      | j.vangoey@instadeep.com           | InstaDeep                               |
| Jimmy K. Eng         | engj@uw.edu                       | University of Washington                |
