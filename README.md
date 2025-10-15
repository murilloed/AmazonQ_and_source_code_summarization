# 🧠 Avaliação de Documentação Gerada por IA – Grupo Focal SASB

## 📘 Visão Geral
Este repositório contém o material, scripts e instrumentos utilizados no **grupo focal de avaliação da documentação gerada automaticamente** pelo **Amazon Q (AWS)** e revisada com suporte do **ChatGPT**.  
O estudo faz parte da POC conduzida no **Sistema SASB** e tem como objetivo **avaliar a qualidade, completude, utilidade e veracidade** da documentação técnica produzida por modelos de IA.

---

## 🎯 Objetivo do Experimento
Avaliar, de forma sistemática e reprodutível, a qualidade da documentação de métodos Java gerada por IA, utilizando três dimensões principais:

- **C (Completeness)** – Cobertura e detalhamento dos parâmetros, retornos e exceções.  
- **H (Helpfulness)** – Clareza, legibilidade e utilidade prática para desenvolvedores.  
- **T (Truthfulness)** – Coerência e fidelidade entre o conteúdo do Javadoc e o código real.

Além da coleta quantitativa via survey, o grupo focal permite **capturar percepções qualitativas** sobre o uso do Amazon Q e do ChatGPT no contexto de documentação automatizada.

---

## 🧩 Metodologia Resumida

### 1. Seleção de Métodos
- Universo: ~200 métodos Java do backend SASB.  
- Seleção: **30 métodos principais + 4 reservas**, com base em amostragem **estratificada por camada e complexidade**.  
- Critérios: camada (service, model, util etc.), presença de exceções, nível de documentação e LOC/ciclomática.

### 2. Distribuição entre Avaliadores
- 15 desenvolvedores participantes.  
- Cada dev avalia **10 métodos**, totalizando **150 avaliações** (30 × 5).  
- Algoritmo de alocação balanceado e reprodutível (seed controlada).

### 3. Instrumento de Coleta
- **Survey quantitativo** baseado em escala Likert (1–5) para C/H/T.  
- **Questões abertas** para observações qualitativas e percepção geral.  
- **Sessão de grupo focal** com roteiro temático sobre percepção, utilidade, impacto e ética.

### 4. Análise de Dados
- Estatísticas descritivas (médias, desvios, boxplots).  
- Confiabilidade interavaliadores (Fleiss’ Kappa, ICC).  
- Correlação entre complexidade e ganho de completude.  
- Codificação qualitativa de insights e percepções.

---

## 🧮 Estrutura do Repositório

