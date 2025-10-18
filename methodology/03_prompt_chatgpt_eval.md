---
title: "LLM-as-a-Judge – Avaliação por ChatGPT"
author: "Murillo"
affiliation: "Programa de Pós-Graduação em Computação Aplicada – Universidade Federal XYZ"
date: "2025-10-18"
version: "1.0"
language: "Java"
license: "MIT"
description: "Prompt usado para análise qualitativa e geração de métricas (Completeness, Helpfulness, Truthfulness) das documentações criadas por Amazon Q e ChatGPT."
---

# ⚖️ Avaliação de Documentação via ChatGPT (LLM-as-a-Judge)

## Objetivo
Avaliar automaticamente a **qualidade da documentação gerada por modelos LLM**, utilizando o ChatGPT como avaliador semântico (“LLM-as-a-Judge”).  
A análise é guiada por três dimensões:  
- **Completeness** – cobertura e detalhamento da explicação.  
- **Helpfulness** – clareza, utilidade e legibilidade.  
- **Truthfulness** – veracidade técnica frente ao código-fonte.  

---

## Prompt principal usado

Você é um avaliador técnico especializado em engenharia de software e documentação de código Java.

Sua tarefa é analisar um método Java e sua documentação (Javadoc), atribuindo pontuações de 0 a 5 para as dimensões abaixo:

Completeness — O quanto a documentação cobre os aspectos funcionais do método (descrição, parâmetros, retorno, exceções)?

Helpfulness — O quanto a explicação auxilia um novo desenvolvedor a compreender o método e seu propósito?

Truthfulness — A documentação descreve corretamente o comportamento real do código?

Retorne o resultado em JSON, neste formato:

{
"Completeness": X.X,
"Helpfulness": X.X,
"Truthfulness": X.X,
"Resumo": "Breve justificativa técnica (máx. 5 linhas)"
}

CÓDIGO:
{código Java original}

DOCUMENTAÇÃO:
{documentação gerada}


---

## Exemplo de resposta esperada
```json
{
  "Completeness": 4.0,
  "Helpfulness": 4.5,
  "Truthfulness": 5.0,
  "Resumo": "Documentação cobre corretamente parâmetros e retorno, com linguagem técnica precisa e informativa."
}

Execução

O script de avaliação foi executado para cada par (código + documentação) e consolidado em uma tabela results_CH_T.json, utilizada para cálculo de médias e variações apresentadas no artigo.

Reprodutibilidade
import json
from openai import OpenAI
client = OpenAI()

prompt = open("methodology/03_prompt_chatgpt_eval.md").read()
code = open("data/code/method1.java").read()
doc = open("results/method1_doc_amazonq.java").read()

response = client.responses.create(
    model="gpt-4-turbo",
    input=prompt.format(código=code, documentação=doc)
)

print(response.output_text)

Observação

Essa etapa é avaliativa, não de geração. O ChatGPT foi usado apenas como instrumento analítico neutro para mensurar atributos qualitativos da documentação.


---

### 📄 `04_prompt_amazonq_refinement.md`
```markdown
---
title: "Refinamento Iterativo – Amazon Q Developer"
author: "Murillo"
affiliation: "Programa de Pós-Graduação em Computação Aplicada – Universidade Federal XYZ"
date: "2025-10-18"
version: "1.0"
language: "Java"
license: "MIT"
description: "Prompt usado na etapa final de refinamento da documentação, após avaliação ChatGPT, para consolidar melhorias e gerar a versão final técnica da Javadoc."
---

# 🔄 Refinamento Iterativo – Amazon Q Developer

## Objetivo
Utilizar o **Amazon Q Developer** em uma segunda rodada de iteração, incorporando as métricas e comentários analíticos da etapa anterior (*LLM-as-a-Judge*) para aprimorar a documentação gerada.  
Essa fase busca **maximizar o equilíbrio entre clareza, completude e precisão técnica**.

---

## Prompt base utilizado

Você é um engenheiro de software experiente e seu papel é revisar e aprimorar a documentação (Javadoc)
de um método Java, com base nas métricas e comentários fornecidos.

Instruções:

Leia atentamente o código e a documentação atual.

Analise o feedback das métricas (Completeness, Helpfulness, Truthfulness).

Melhore a documentação sem alterar o código.

Garanta que a nova versão da documentação:

Mencione exceções relevantes.

Use verbos técnicos precisos e impessoais.

Mantenha consistência terminológica e de estilo.

Retorne o método completo, apenas com a documentação revisada.

CÓDIGO:
{código Java original}

DOCUMENTAÇÃO ATUAL:
{documentação gerada}

MÉTRICAS E FEEDBACK:
{resultados da avaliação em JSON}


---

## Exemplo de refinamento resultante

```java
/**
 * Returns detailed information about the currently authenticated user.
 *
 * @param authentication the security context containing user credentials
 * @return a populated UserInfoDTO if the principal is a CustomUserDTO, otherwise null
 * @throws IllegalStateException if the authentication context is invalid or null
 */
@GetMapping(produces = MediaType.APPLICATION_JSON_VALUE)
public UserInfoDTO getUserInfo(Authentication authentication) {
    ...
}

Observações

O refinamento foi aplicado apenas quando a pontuação de Helpfulness < 4.5 ou Completeness < 4.0.

Cada nova versão foi reavaliada por ChatGPT, fechando o ciclo de melhoria contínua (Human-out-of-the-loop).

Execução automatizada

feedback = open("results/method1_eval_chatgpt.json").read()
prompt = open("methodology/04_prompt_amazonq_refinement.md").read()
code = open("data/code/method1.java").read()
doc = open("results/method1_doc_amazonq.java").read()

response = client.responses.create(
    model="amazon-q-developer",
    input=prompt.format(
        código=code,
        documentação=doc,
        resultados=feedback
    )
)
print(response.output_text)

Referência

Esta etapa conclui o ciclo experimental de documentation generation and iterative evaluation,
possibilitando análise comparativa entre as versões geradas e refinadas.

