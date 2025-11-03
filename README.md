# Using Review Protocols to Train AI for Systematic Reviews: Guiding Considerations
> Authors: Ruhan Circi, Bhashithe Abeysinghe, Mario Kubek, Hemanth Venkateswara, David Miller (contact: Ruhan Circi, rcirci@air.org)

Recent advances in artificial intelligence (AI) have promising potential to transform the speed and scale of conducting systematic reviews. Technologies such as large language models (LLMs) can serve as powerful research assistants for helping to automate the mundane, repetitive tasks of synthesizing vast amounts of academic literature. Despite their potential, however, current applications of these technologies vary widely in their accuracy for systematic review tasks (e.g., judging study eligibility, extracting data; [Schmidt et al., 2025](https://f1000research.com/articles/10-401/v3)).

This post details a key ingredient for better harnessing the potential of AI-supported tools for systematic reviews: *the clarity of instructions given to LLMs*. Just like human assistants, LLMs will not perform well if given vague or ambiguous directions. And just like training human reviewers, creating written protocols of a review’s pre-specified plans should be a cornerstone of providing clear instructions.

Traditional protocols written for humans, however, require adaptation for optimal use by AI applications. This post is the first in a three-part series about adapting traditional review protocols to serve as machine-readable inputs for LLMs. This post introduces key guiding considerations, while later posts will apply these takeaways to a previously completed systematic review and detail empirical findings from that case example.

## Why LLMs Struggle with Traditional Protocols

A review protocol is a written, pre-specified plan that establishes the review’s rationale, scope, and procedures before selecting studies and extracting their data. These protocol documents help minimize bias, support transparency, undergird the training of reviewers, and allow other teams to replicate or update the findings ([Moher et al., 2015](https://systematicreviewsjournal.biomedcentral.com/articles/10.1186/2046-4053-4-1)). 

Traditional protocols, however, are not written with AI applications in mind. They are written for humans, tending to be narrative and open-ended. They support researcher judgment, not machine logic per se. Although LLMs can process natural language, their performance for tailored tasks depends heavily on providing clear and structural instructions ([Bender & Koller, 2020](https://aclanthology.org/2020.acl-main.463/)) as well as fine-tuning the models using context-specific examples ([Ouyang et al, 2022](https://proceedings.neurips.cc/paper_files/paper/2022/hash/b1efde53be364a73914f58805a001731-Abstract-Conference.html)). This limitation reflects that LLMs function primarily as statistical pattern matchers rather than entities capable of comprehension.

Here's where the mismatch occurs for LLMs and traditional review protocols:

- Protocols contain ambiguities and narrative flourishes that challenge AI interpretation.
- Criteria are embedded in prose, not structured prompts or logic statements.
- Domain-specific concepts often lack grounding in the model’s training data, which may lead to hallucinations or misclassifications.
- Human teams may make additional decisions on how to interpret the protocol, without specifying those decisions in the document itself.

## Toward AI-Ready Protocols: A Structured Solution

Addressing this mismatch requires adapting the review protocol. New formats are needed that are modularized by task and prompt friendly. These transformations can then support computational workflows of AI agents that are tailored and fine-tuned to discrete systematic review tasks. 

### 1. Modular Protocol Structure

Traditional protocols typically segment systematic review tasks into distinct stages (e.g., screening, extraction, synthesis). Likewise, AI-ready protocols should be divided into distinct modules with defined content, rule types, and LLM tasks instructions for a specific review stage (e.g., a screening module, a data extraction module).

Explicit rules will guide the LLM’s behavior for each stage. For example, a rule about an article’s year of publication may have different versions in various stages such as screening (study must be published before 1990) and data extraction (extract the year of publication). Table 1 shows a simplified example. 

Table 1: Example of modularized protocol structure

| Module          | Sub-module             | Content Focus            | Example Rule                                      | LLM Task    |
|-----------------|------------------------|---------------------------|---------------------------------------------------|-------------|
| Screening       | Study Characteristics  | Metadata, publication     | Study must be published before 1990               | Conditional |
| Screening       | Sample Characteristics | Population, subgroup      | Sample must have at least 80% PreK–12 students    | Conditional |
| Data extraction | Study Characteristics  | Metadata, publication     | Extract the year of publication                   | Retrieval   |
| Data extraction | Sample Characteristics | Population, subgroup      | Extract the grade levels of the sample            | Retrieval   |

Explicitly organizing each review stage into distinct rules with LLM task instructions distinguishes AI-ready protocols from traditional protocols. However, this difference may not always be extreme, depending on the existing structure of the traditional protocol. For instance, data extraction protocols in the [MetaReviewer platform](https://www.metareviewer.org/learn/coding-form-templates/) use an explicit, consistent structure in Google Docs for defining each data field to extract. Adapting for an AI-ready format is easier with that explicit structure already built in for each item.

### 2. Protocol-to-Prompt Transformation

Instead of narrative statements like:

"Studies must conduct an impact evaluation using a randomized controlled trial (RCT) or quasi-experimental design (QED)."

An AI-ready version might state ([Arvidsson & Axell, 2023](https://gupea.ub.gu.se/handle/2077/77967)):

"If the study design is a randomized controlled trial (RCT) or quasi-experimental design (QED), this rule passes. Otherwise, this rule fails."

Additional definitions and examples can then also instruct the LLM how to interpret terms such as "quasi-experimental design."

Such transformations allow LLMs to execute rules reliably. Recent research demonstrates that carefully designed prompts can effectively translate unstructured clinical protocols into structured instructions for LLMs ([Choi et al., 2023](https://www.e-roj.org/journal/view.php?doi=10.3857/roj.2023.00633)), underscoring the importance of prompt engineering.

### 3. Agent-Based Workflow

These changes to the review protocol can support multi-agent AI workflows. An agent in the context of AI and LLMs is an entity that is contained within an environment, has a unique task, and takes actions towards completing that task. An agent-based system can be implemented in the modularized mechanism introduced earlier:

- A Screener Agent applies inclusion/exclusion rules in the screening module.
- An Extractor Agent fills structured templates with data extracted from articles.
- An Analyzer Agent prepares summary statistics or identifies patterns across studies.

This distributed approach mimics the multi-stage and multi-reviewer practice in traditional systematic reviews and builds in redundancy and consensus mechanisms ([Yuksel et al., 2024](https://arxiv.org/abs/2412.17149)). 

## Harnessing the Potential of AI for High-Quality Research Synthesis

While review protocols vary in format and depth across disciplines, their purpose is universal: formalize design, reduce bias, and ensure transparency. Whether in public health, education, or social policy, transforming protocols into AI-friendly structured formats serves two critical goals:

1. Scalability: As evidence grows exponentially, manual review becomes a bottleneck. AI can help, but only with instructions it can follow.
2. Reproducibility: AI-assisted research synthesis must maintain rigorous standards. Structured, modular protocols ensure that AI outputs remain accountable and interpretable.

Critically, this transformation doesn’t eliminate human roles. Instead, it reimagines the roles. Minimally, humans design the protocol and review AI decisions. LLMs serve as research assistants that require training and oversight. And just like training human assistants, mechanisms for quality assurance are needed (e.g., dual coding where studies are reviewed by two independent coders). Creating an AI-friendly protocol is the starting place for designing such checks and balances.
The future of evidence synthesis may therefore involve a team of digital agents working alongside researchers, each aligned to protocol modules, contributing to a faster, more consistent, and still rigorous review process. To advance this shift, the review protocol of tomorrow should not be just a PDF; it should be a prompt system, an audit trail, and a collaborative blueprint for human-AI synthesis, enabling the AI models’ reasoning to be more transparent and attuned to precise human direction.

Stay tuned for our next blog post, which will apply these considerations to the protocol in a completed [past systematic review](https://journals.sagepub.com/doi/10.1177/23328584241269866)! Contact lead author Ruhan Circi (rcirci@air.org) with questions.

## References
- Arvidsson, S., & Axell, J. (2023). Prompt engineering guidelines for LLMs in Requirements Engineering. https://hdl.handle.net/2077/77967  
- Bender, E. M., & Koller, A. (2020). Climbing towards NLU: On meaning, form, and understanding in the age of data. Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics, 5185–5198. https://doi.org/10.18653/v1/2020.acl-main.463  
- Choi, H. S., Song, J. Y., Shin, K. H., Chang, J. H., & Jang, B. S. (2023). Developing prompts from large language models for extracting clinical information from pathology and ultrasound reports in breast cancer. Radiation Oncology Journal, 41(3), 209–216. https://doi.org/10.3857/roj.2023.00633  
- Moher, D., Shamseer, L., Clarke, M., Ghersi, D., Liberati, A., Petticrew, M., ... & Prisma-P Group. (2015). Preferred reporting items for systematic review and meta-analysis protocols (PRISMA-P) 2015 statement. Systematic Reviews, 4(1), 1. https://doi.org/10.1186/2046-4053-4-1   
- Ouyang, L., Wu, J., Jiang, X., Almeida, D., Wainwright, C., Mishkin, P., ... & Lowe, R. (2022). Training language models to follow instructions with human feedback. Advances in neural information processing systems, 35, 27730-27744.  
- Riaz, I. B., Naqvi, S. A. A., Hasan, B., & Murad, M. H. (2024). Future of evidence synthesis: Automated, living, and interactive systematic reviews and meta-analyses. Mayo Clinic Proceedings: Digital Health, 2(3), 361-365. https://doi.org/10.1016/j.mcpdig.2024.05.023   
- Schmidt, L., Mutlu, A. N. F., Elmore, R., Olorisade, B. K., Thomas, J., & Higgins, J. P. (2025). Data extraction methods for systematic review (semi)automation: Update of a living systematic review. F1000Research, 10, 401. https://doi.org/10.12688/f1000research.51117.3  
- Yuksel, K. A., & Sawaf, H. (2024). A Multi-AI Agent System for Autonomous Optimization of Agentic AI Solutions via Iterative Refinement and LLM-Driven Feedback Loops. https://doi.org/10.48550/ARXIV.2412.17149  
