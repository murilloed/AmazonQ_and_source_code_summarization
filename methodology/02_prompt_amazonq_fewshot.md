---
title: "Few-Shot Prompt – Amazon Q Developer"
author: "Murillo"
affiliation: "Programa de Pós-Graduação em Computação Aplicada – Universidade Federal XYZ"
date: "2025-10-17"
version: "1.0"
language: "Java"
doi: "10.5281/zenodo.placeholder"
license: "MIT"
description: "Instrução de few-shot prompting utilizada na geração inicial de documentação técnica (Javadoc) para métodos Java legados com Amazon Q Developer."
---

# 🧠 Few-Shot Prompt – Amazon Q Developer

## 1️⃣ Objetivo
Gerar documentação técnica (Javadoc) para métodos Java legados **sem alterar o código-fonte**, utilizando o modelo **Amazon Q Developer** com a técnica de *few-shot prompting*.  
A meta é avaliar a **capacidade de generalização e consistência** do modelo ao replicar padrões de documentação de alta qualidade a partir de poucos exemplos.

---

## 2️⃣ Estratégia
A abordagem *few-shot* consistiu em apresentar **dois exemplos curtos e bem documentados** (exemplos de referência) antes do código alvo.  
Os exemplos seguem o padrão de documentação da Oracle e práticas recomendadas da engenharia de software.

O modelo foi instruído a:
- Preservar a estrutura do método e suas anotações (@GetMapping, @PreAuthorize etc.);
- Inserir Javadoc imediatamente acima do método;
- Incluir seções obrigatórias `@param`, `@return`, e `@throws` (quando aplicável);
- Manter tom técnico, impessoal e objetivo.

---

## 3️⃣ Instrução completa utilizada

System Instruction:
Você é um assistente técnico especializado em engenharia de software e Java.
Sua tarefa é gerar documentação técnica (Javadoc) para métodos Java legados,
seguindo as convenções da linguagem Java 8+ e padrões de documentação da Oracle.

Instruções:

Não altere a lógica, parâmetros ou retornos do método.

Gere apenas comentários Javadoc.

Inclua as seções: descrição geral, @param, @return, @throws (quando aplicável).

Use linguagem técnica, objetiva e impessoal.

Utilize nomes das classes e tipos exatamente como aparecem no código.

Não adicionar exemplos de uso.

Retorne apenas o código com o Javadoc inserido.

EXEMPLO 1:
/**

Calculates the sum of two integer numbers.

@param a the first integer

@param b the second integer

@return the sum of both integers
*/
public int add(int a, int b) {
return a + b;
}

EXEMPLO 2:
/**

Retrieves customer data by ID.

@param id unique identifier of the customer

@return Customer object if found, null otherwise

@throws IllegalArgumentException if id is null or invalid
*/
public Customer getCustomerById(String id) { ... }

AGORA DOCUMENTE O SEGUINTE MÉTODO:


*(aqui o código Java alvo é inserido, ex: `getUserInfo(Authentication authentication)`)*

4️⃣ Exemplo aplicado ao método 1 (getUserInfo)

Código de entrada:
@GetMapping(produces = MediaType.APPLICATION_JSON_VALUE)
public UserInfoDTO getUserInfo(Authentication authentication) {
    var userDetails = (UserDetails) authentication.getPrincipal();
    if (userDetails instanceof CustomUserDTO) {
        CustomUserDTO customUser = (CustomUserDTO) userDetails;
        return UserInfoDTO.builder()
                .name(customUser.getFullName())
                .email(customUser.getMail())
                .preferredUsername(customUser.getUsername())
                .build();
    }
    return null;
}

Saída gerada pelo Amazon Q:

/**
 * Retrieves user information from the authenticated user's details.
 *
 * @param authentication the authentication object containing user details
 * @return a UserInfoDTO containing user information if the principal is a CustomUserDTO, null otherwise
 */
@GetMapping(produces = MediaType.APPLICATION_JSON_VALUE)
public UserInfoDTO getUserInfo(Authentication authentication) {
    var userDetails = (UserDetails) authentication.getPrincipal();
    if (userDetails instanceof CustomUserDTO) {
        CustomUserDTO customUser = (CustomUserDTO) userDetails;
        return UserInfoDTO.builder()
                .name(customUser.getFullName())
                .email(customUser.getMail())
                .preferredUsername(customUser.getUsername())
                .build();
    }
    return null;
}

5️⃣ Observações experimentais

O modelo gerou documentação sintática e semanticamente consistente, mas sem a tag @throws.

A estrutura few-shot mostrou-se estável e replicável para outros métodos similares.

Essa etapa representa a primeira iteração do pipeline experimental, antecedendo a análise LLM-as-a-Judge e a revisão pelo Amazon Q.

6️⃣ Reprodutibilidade

Para replicar esta etapa experimental:

# Exemplo de uso em Python
from openai import OpenAI
client = OpenAI()

prompt = open("methodology/02_prompt_amazonq_fewshot.md").read()
code = open("data/codigo_original/UserResource.java").read()

response = client.responses.create(
    model="amazon-q-developer",
    input=f"{prompt}\n{code}"
)
print(response.output_text)
🧩 Notas finais

Este arquivo faz parte do repositório público murillo-llm-code-docs, voltado à reprodutibilidade científica da pesquisa
“Avaliação de LLMs na Documentação Técnica Automatizada de Sistemas Java Legados” (Murillo, 2025).

📘 Citação sugerida:
Murillo, M. (2025). Few-Shot Prompt – Amazon Q Developer.
In: Repositório Experimental murillo-llm-code-docs, Zenodo DOI:10.5281/zenodo.placeholder.
