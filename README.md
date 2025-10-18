# 📘 SARSB Documentation Intelligence — Amazon Q Evaluation Framework

### Agência Nacional de Águas e Saneamento Básico (ANA)  
**Projeto Experimental de Avaliação de Modelos de Linguagem (LLMs) aplicados à Documentação Automatizada em Sistemas Legados**

---

## 🧩 Visão Geral
Este repositório contém os materiais, scripts e resultados associados ao estudo **“Avaliação do Amazon Q (AWS) para geração automatizada de documentação técnica no sistema SARSB”**, conduzido como parte da pesquisa de pós-graduação em Engenharia de Software aplicada à transformação digital do setor público.

O estudo avalia a **eficácia, utilidade e veracidade** de documentações geradas automaticamente por modelos de linguagem de grande escala (LLMs) — com foco no **Amazon Q**, utilizando o sistema **SARSB (Sistema Nacional de Saneamento Básico)** como estudo de caso empírico.

---

## 🧠 Objetivo
Avaliar a viabilidade do uso de **modelos de linguagem generativos (LLMs)** para apoiar a **documentação técnica automatizada de sistemas legados**, garantindo:
- **Completude estrutural (Completeness)**: aderência ao padrão Javadoc;  
- **Utilidade prática (Helpfulness)**: clareza e relevância percebidas;  
- **Veracidade factual (Truthfulness)**: consistência entre documentação e código real.

---

## ⚙️ Estrutura Metodológica

### **1. Goal–Question–Metric (GQM)**
Estrutura de rastreabilidade que conecta objetivos, perguntas de pesquisa e métricas mensuráveis:
- **Goal:** avaliar a eficácia do Amazon Q na documentação automatizada.  
- **Questions:** o conteúdo gerado é completo, útil e verdadeiro?  
- **Metrics:** derivadas das dimensões CHT — *Completeness*, *Helpfulness* e *Truthfulness*.

### **2. Evaluation Framework (CHT)**
Tripé de avaliação proposto para mensurar qualidade documental:
- **Completeness:** verificação automática via AST + Regex.  
- **Helpfulness:** avaliação com *LLM-as-a-Judge* (ChatGPT).  
- **Truthfulness:** checagem contra grafo de dependências do código.

---

## 🧮 Dataset

- **Sistema Avaliado:** SARSB (Sistema de Acompanhamento de Referência do Saneamento Básico)  
- **Linguagem:** Java  
- **Arquivos:** 563  
- **Linhas de Código:** ~35.000  
- **Métodos Totais:** 510  
- **Amostra Experimental:** 219 métodos (amostragem estratificada proporcional)  
- **Camadas Analisadas:** Config, Exception, Model, Report, Repository, Resource, Service, Util  

---

## 🧾 Indicadores de Avaliação

| Indicador | Descrição | Método de Cálculo |
|------------|------------|------------------|
| **C-score** | Completude estrutural | % de seções Javadoc presentes |
| **H-score** | Utilidade percebida | Média Likert (1–5) por LLM-as-a-Judge |
| **T-score** | Veracidade factual | Razão de entidades verificadas |
| **QDI** | Índice de ganho de completude | (Documentação gerada / Documentação original) |

---

## 🧰 Pipeline Experimental

1. **Extração dos métodos** do repositório Java (via scripts PowerShell e Python).  
2. **Geração automática de documentação** com **Amazon Q (AWS)** — modo *zero-shot* e *few-shot prompting*.  
3. **Análise CHT**:
   - *Completeness* → AST + Regex  
   - *Helpfulness* → LLM-as-a-Judge  
   - *Truthfulness* → Dependency Graph Checking  
4. **Cálculo de métricas (C, H, T, QDI)**.  
5. **Tratamento estatístico**: correlações, médias e análises inferenciais.  
6. **Reprodutibilidade**: todos os outputs armazenados e versionados em planilhas estruturadas.

## 🧪 Metodologia de Reprodutibilidade

A pasta **`/methodology/`** contém todos os arquivos necessários para **replicar o experimento completo**, seguindo boas práticas de *Empirical Software Engineering*.  

---

## 📊 Principais Resultados (Resumo)

- **Completude média:** 71%  
- **Helpfulness média:** 4,0 / 5  
- **Truthfulness (Existence Ratio):** 0,89  
- **Comparativo:** desempenho similar ao DocAgent (Meta AI, 2025)

Esses resultados demonstram que o **Amazon Q** é viável como ferramenta de apoio à documentação automatizada, especialmente em sistemas públicos legados de grande escala.

---

## 🧭 Conclusão
O framework proposto integra **rastreabilidade científica (GQM)**, **avaliação automatizada (CHT)** e **validação híbrida (IA + revisão humana)**.  
O estudo estabelece um **padrão metodológico reprodutível** para pesquisas sobre documentação técnica gerada por LLMs, contribuindo para a adoção segura e auditável de inteligência artificial na **engenharia de software pública**.

---

## 📚 Referências Principais
- Basili, V.R., Caldiera, G., & Rombach, H.D. (1994). *Goal Question Metric Approach*.  
- Yang, D. et al. (2025). *DocAgent: A Multi-Agent System for Automated Code Documentation Generation*. Meta AI.  
- Gu, J. et al. (2024). *Survey on LLMs for Software Engineering*. IEEE Software.  
- Esquivel, A. et al. (2023). *Detecção Automatizada de Estruturas de Código via AST*.  
- Treccani, M. et al. (2010). *Utilização de Métodos Empíricos em Engenharia de Software*.

---

## 🧩 Estrutura do Repositório

├── /src/ # Scripts de coleta e análise (PowerShell, Python)
├── /methodology/ # Metodologia de reprodutibilidade (documentos e notebooks)
├── /outputs/ # Resultados (planilhas e logs)
├── /docs/ # Relatórios e figuras metodológicas
├── /references/ # Arquivos BibTeX e PDFs científicos
├── README.md # Este arquivo
└── LICENSE # Licença pública institucional (ANA)


---

## 🏛️ Licença e Uso Institucional
Este repositório faz parte de um projeto de pesquisa vinculado à **Agência Nacional de Águas e Saneamento Básico (ANA)**.  
Os dados do sistema SARSB são de uso restrito e utilizados exclusivamente para fins acadêmicos e de pesquisa científica.  
O código auxiliar (scripts e pipelines) é disponibilizado sob **licença MIT**.

---

## 📬 Contato
**Autor:** Murillo Carvalho 
**Instituição:** Universidade de Brasília (UnB)  
**Orientador:** Prof. [Rodrigo Bonifácio de Almeida]  
**E-mail:** murillo.ed1402@gmail.com  
**Ano:** 2025  

---
