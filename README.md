# 📘 SARSB Documentation Intelligence — Amazon Q Evaluation Framework

### National Water and Basic Sanitation Agency (ANA)  
**Experimental Research Project on Large Language Models (LLMs) for Automated Documentation in Legacy Systems**

---

## 🧩 Overview
This repository contains materials, scripts, and results related to the study **“Evaluation of Amazon Q (AWS) for Automated Technical Documentation Generation in the SARSB System”**, conducted as part of a graduate research project in **Software Engineering** applied to the digital transformation of the public sector.

The study evaluates the **effectiveness, usefulness, and factual accuracy** of automatically generated documentation produced by **Large Language Models (LLMs)** — focusing on **Amazon Q**, using the **SARSB (National Basic Sanitation System)** as an empirical case study.

---

## 🧠 Objective
To assess the feasibility of using **Generative Language Models (LLMs)** to support **automated technical documentation** for legacy systems, ensuring:
- **Structural Completeness:** adherence to the Javadoc standard;  
- **Practical Helpfulness:** clarity and usefulness for developers;  
- **Factual Truthfulness:** consistency between documentation and actual code.

---

## ⚙️ Methodological Framework

### **1. Goal–Question–Metric (GQM)**
A traceability structure linking research goals, guiding questions, and measurable metrics:
- **Goal:** Evaluate the effectiveness of Amazon Q in generating technical documentation.  
- **Questions:** Is the generated content complete, helpful, and factually correct?  
- **Metrics:** Derived from the CHT dimensions — *Completeness*, *Helpfulness*, and *Truthfulness*.

### **2. Evaluation Framework (CHT)**
A three-dimensional evaluation model for assessing documentation quality:
- **Completeness:** automated verification via AST and regular expressions.  
- **Helpfulness:** evaluation using *LLM-as-a-Judge* (ChatGPT).  
- **Truthfulness:** validation against the system’s dependency graph to reduce hallucinations.

---

## 🧮 Dataset

- **System Evaluated:** SARSB (National Basic Sanitation System of Brazil)  
- **Language:** Java  
- **Files:** 563  
- **Lines of Code:** ~35,000  
- **Total Methods:** 510  
- **Experimental Sample:** 219 methods (proportional stratified sampling)  
- **Analyzed Layers:** Config, Exception, Model, Report, Repository, Resource, Service, Util  

---

## 🧾 Evaluation Indicators

| Indicator | Description | Calculation Method |
|------------|-------------|--------------------|
| **C-score** | Structural Completeness | % of required Javadoc sections present |
| **H-score** | Perceived Helpfulness | Likert average (1–5) by LLM-as-a-Judge |
| **T-score** | Factual Truthfulness | Ratio of verified entities in code |
| **QDI** | Quality Deviation Index | (Generated Documentation / Original Documentation) |

---

## 🧰 Experimental Pipeline

1. **Method Extraction** from the Java repository (via PowerShell and Python scripts).  
2. **Automated Documentation Generation** using **Amazon Q (AWS)** — *zero-shot* and *few-shot prompting* modes.  
3. **CHT Evaluation**:
   - *Completeness* → AST + Regex  
   - *Helpfulness* → LLM-as-a-Judge  
   - *Truthfulness* → Dependency Graph Checking  
4. **Metric Calculation:** C, H, T, and QDI scores.  
5. **Statistical Analysis:** correlations, averages, and inferential analyses.  
6. **Reproducibility:** all outputs versioned and stored in structured datasets.

---

## 🧪 Reproducibility Methodology

The **`/methodology/`** folder contains all files required to **replicate the full experiment**, following best practices in *Empirical Software Engineering*.  

---


These resources ensure:
- **Scientific Transparency:** all parameters and scripts are documented.  
- **Full Traceability:** every run linked to reproducible logs and versioned results.  
- **Cross-validation:** combined automated and human evaluation for robustness.  

> 💡 Researchers can use this package to reproduce the pipeline on other Java repositories, compare results, or adapt the framework for new software documentation contexts.

---

## 📊 Key Results (Summary)

- **Average Completeness:** 71%  
- **Average Helpfulness:** 4.0 / 5  
- **Average Truthfulness (Existence Ratio):** 0.89  
- **Comparison:** similar performance to DocAgent (Meta AI, 2025)

These results demonstrate that **Amazon Q** is a feasible and effective tool for automated documentation, particularly within large-scale public sector systems.

---

## 🧭 Conclusion
The proposed framework integrates **scientific traceability (GQM)**, **automated evaluation (CHT)**, and **hybrid validation (AI + human review)**.  
It establishes a **reproducible and auditable methodology** for evaluating LLM-generated documentation, contributing to the **safe adoption of AI in public software engineering**.

---

## 📚 Key References
- Basili, V.R., Caldiera, G., & Rombach, H.D. (1994). *Goal Question Metric Approach*.  
- Yang, D. et al. (2025). *DocAgent: A Multi-Agent System for Automated Code Documentation Generation*. Meta AI.  
- Gu, J. et al. (2024). *Survey on LLMs for Software Engineering*. IEEE Software.  
- Esquivel, A. et al. (2023). *Automatic Detection of Code Structures via AST*.  
- Treccani, M. et al. (2010). *Empirical Methods in Software Engineering*.  

---

## 🧩 Repository Structure

├── /src/ # Data collection and analysis scripts (PowerShell, Python)
├── /methodology/ # Reproducibility methodology (docs and notebooks)
├── /outputs/ # Results (spreadsheets, logs)
├── /docs/ # Reports and methodological figures
├── /references/ # BibTeX files and reference papers
├── README.md # This file
└── LICENSE # Institutional license (ANA)


---

## 🏛️ License and Institutional Use
This repository is part of a research project linked to the **National Water and Basic Sanitation Agency (ANA)**.  
SARSB system data are restricted and used exclusively for academic and scientific purposes.  
Auxiliary code (scripts and pipelines) is released under the **MIT License**.

---

## 📬 Contact
**Author:** Murillo Carvalho  
**Institution:** University of Brasília (UnB)  
**Advisor:** Prof. Rodrigo Bonifácio de Almeida  
**E-mail:** murillo.ed1402@gmail.com  
**Year:** 2025  

---


