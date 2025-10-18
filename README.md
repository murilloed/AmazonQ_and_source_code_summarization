<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>SARSB Documentation Intelligence — Amazon Q Evaluation Framework</title>
  <style>
    :root{
      --bg:#fbfbfb;
      --card:#ffffff;
      --accent:#0b5fff;
      --muted:#6b7280;
      --mono: "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    }
    html,body{height:100%;margin:0;background:var(--bg);font-family:var(--mono);color:#111827}
    .container{max-width:980px;margin:32px auto;padding:28px;background:var(--card);box-shadow:0 6px 22px rgba(15,23,42,0.06);border-radius:8px}
    h1{margin:0 0 6px;font-size:26px}
    h2{color:var(--accent);margin-top:20px}
    p.lead{color:var(--muted);margin:8px 0 18px}
    hr{border:0;border-top:1px solid #eef2f7;margin:22px 0}
    ul{margin:8px 0 18px;padding-left:20px}
    code{background:#f3f4f6;padding:2px 6px;border-radius:4px;font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", "Courier New", monospace}
    .meta{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
    .badge{background:#eef2ff;color:var(--accent);padding:6px 10px;border-radius:999px;font-weight:600}
    table{width:100%;border-collapse:collapse;margin:12px 0 18px}
    table th, table td{border:1px solid #eef2f7;padding:12px;text-align:left}
    pre{background:#0f1724;color:#e6eef6;padding:12px;border-radius:6px;overflow:auto;font-size:13px}
    .footer{margin-top:22px;color:var(--muted);font-size:13px}
    .contact{margin-top:18px;padding:12px;border-left:3px solid #e6eef6;background:#fbfdff;border-radius:6px}
  </style>
</head>
<body>
  <main class="container" role="main">
    <header>
      <h1>📘 SARSB Documentation Intelligence — Amazon Q Evaluation Framework</h1>
      <p class="lead"><strong>Agência Nacional de Águas e Saneamento Básico (ANA)</strong><br>
      Projeto experimental de avaliação de modelos de linguagem (LLMs) aplicados à documentação automatizada em sistemas legados.</p>
    </header>

    <hr />

    <section id="overview">
      <h2>Visão Geral</h2>
      <p>Este repositório contém os materiais, scripts e resultados associados ao estudo <strong>“Avaliação do Amazon Q (AWS) para geração automatizada de documentação técnica no sistema SARSB”</strong>, conduzido como parte da pesquisa de pós-graduação em Engenharia de Software voltada à transformação digital do setor público.</p>
      <p>O estudo avalia a <strong>eficácia, utilidade e veracidade</strong> de documentações geradas por modelos de linguagem de grande escala (LLMs), com foco no <strong>Amazon Q</strong>, usando o sistema <strong>SARSB</strong> como caso empírico.</p>
    </section>

    <hr />

    <section id="objective">
      <h2>Objetivo</h2>
      <p>Avaliar a viabilidade do uso de <strong>LLMs</strong> para apoiar a documentação técnica automatizada de sistemas legados, garantindo:</p>
      <ul>
        <li><strong>Completude estrutural (Completeness)</strong>: aderência ao padrão Javadoc;</li>
        <li><strong>Utilidade prática (Helpfulness)</strong>: clareza e relevância percebidas;</li>
        <li><strong>Veracidade factual (Truthfulness)</strong>: consistência entre documentação e código real.</li>
      </ul>
    </section>

    <hr />

    <section id="methodology">
      <h2>Estrutura Metodológica</h2>

      <h3>1. Goal–Question–Metric (GQM)</h3>
      <p>Estrutura de rastreabilidade que conecta objetivos, perguntas de pesquisa e métricas mensuráveis:</p>
      <ul>
        <li><strong>Goal:</strong> avaliar a eficácia do Amazon Q na documentação automatizada.</li>
        <li><strong>Questions:</strong> o conteúdo gerado é completo, útil e verdadeiro?</li>
        <li><strong>Metrics:</strong> derivadas das dimensões CHT — <em>Completeness</em>, <em>Helpfulness</em> e <em>Truthfulness</em>.</li>
      </ul>

      <h3>2. Evaluation Framework (CHT)</h3>
      <p>Tripé de avaliação proposto para mensurar qualidade documental:</p>
      <ul>
        <li><strong>Completeness:</strong> verificação automática via AST + Regex.</li>
        <li><strong>Helpfulness:</strong> avaliação com <em>LLM-as-a-Judge</em> (ChatGPT).</li>
        <li><strong>Truthfulness:</strong> checagem contra grafo de dependências do código.</li>
      </ul>
    </section>

    <hr />

    <section id="dataset">
      <h2>Dataset</h2>
      <ul>
        <li><strong>Sistema Avaliado:</strong> SARSB (Sistema de Acompanhamento de Referência do Saneamento Básico)</li>
        <li><strong>Linguagem:</strong> Java</li>
        <li><strong>Arquivos:</strong> 563</li>
        <li><strong>Linhas de Código:</strong> ~35.000</li>
        <li><strong>Métodos Totais:</strong> 510</li>
        <li><strong>Amostra Experimental:</strong> 219 métodos (amostragem estratificada proporcional)</li>
        <li><strong>Camadas Analisadas:</strong> Config, Exception, Model, Report, Repository, Resource, Service, Util</li>
      </ul>
    </section>

    <hr />

    <section id="indicators">
      <h2>Indicadores de Avaliação</h2>
      <table aria-label="Indicadores de Avaliação">
        <thead>
          <tr>
            <th>Indicador</th>
            <th>Descrição</th>
            <th>Método de Cálculo</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>C-score</strong></td>
            <td>Completude estrutural</td>
            <td>% de seções Javadoc presentes</td>
          </tr>
          <tr>
            <td><strong>H-score</strong></td>
            <td>Utilidade percebida</td>
            <td>Média Likert (1–5) por LLM-as-a-Judge</td>
          </tr>
          <tr>
            <td><strong>T-score</strong></td>
            <td>Veracidade factual</td>
            <td>Razão de entidades verificadas</td>
          </tr>
          <tr>
            <td><strong>QDI</strong></td>
            <td>Índice de ganho de completude</td>
            <td>(Documentação gerada / Documentação original)</td>
          </tr>
        </tbody>
      </table>
    </section>

    <hr />

    <section id="pipeline">
      <h2>Pipeline Experimental</h2>
      <ol>
        <li><strong>Extração dos métodos</strong> do repositório Java (via scripts PowerShell e Python).</li>
        <li><strong>Geração automática de documentação</strong> com <strong>Amazon Q (AWS)</strong> — modos <em>zero-shot</em> e <em>few-shot prompting</em>.</li>
        <li><strong>Análise CHT</strong>:
          <ul>
            <li><em>Completeness</em> → AST + Regex</li>
            <li><em>Helpfulness</em> → LLM-as-a-Judge</li>
            <li><em>Truthfulness</em> → Dependency Graph Checking</li>
          </ul>
        </li>
        <li><strong>Cálculo de métricas</strong> (C, H, T, QDI).</li>
        <li><strong>Tratamento estatístico</strong>: correlações, médias e análises inferenciais.</li>
        <li><strong>Reprodutibilidade</strong>: outputs armazenados e versionados em planilhas estruturadas.</li>
      </ol>
    </section>

    <hr />

    <section id="results">
      <h2>Principais Resultados (Resumo)</h2>
      <ul>
        <li><strong>Completude média:</strong> 71%</li>
        <li><strong>Helpfulness média:</strong> 4,0 / 5</li>
        <li><strong>Truthfulness (Existence Ratio):</strong> 0,89</li>
        <li><strong>Comparativo:</strong> desempenho similar ao DocAgent (Meta AI, 2025)</li>
      </ul>
      <p>Estes resultados indicam que o <strong>Amazon Q</strong> é viável como ferramenta de apoio à documentação automatizada em sistemas públicos legados de grande escala.</p>
    </section>

    <hr />

    <section id="conclusion">
      <h2>Conclusão</h2>
      <p>O framework proposto integra <strong>rastreabilidade científica (GQM)</strong>, <strong>avaliação automatizada (CHT)</strong> e <strong>validação híbrida (IA + revisão humana)</strong>. O estudo estabelece um padrão metodológico reprodutível para pesquisas sobre documentação técnica gerada por LLMs, contribuindo para a adoção segura e auditável de IA na engenharia de software pública.</p>
    </section>

    <hr />

    <section id="references">
      <h2>Referências Principais</h2>
      <ul>
        <li>Basili, V.R., Caldiera, G., & Rombach, H.D. (1994). <em>Goal Question Metric Approach</em>.</li>
        <li>Yang, D. et al. (2025). <em>DocAgent: A Multi-Agent System for Automated Code Documentation Generation</em>. Meta AI.</li>
        <li>Gu, J. et al. (2024). <em>Survey on LLMs for Software Engineering</em>. IEEE Software.</li>
        <li>Esquivel, A. et al. (2023). <em>Detecção Automatizada de Estruturas de Código via AST</em>.</li>
        <li>Treccani, M. et al. (2010). <em>Utilização de Métodos Empíricos em Engenharia de Software</em>.</li>
      </ul>
    </section>

    <hr />

    <section id="repo-structure">
      <h2>Estrutura do Repositório</h2>
      <pre><code>├── /src/                     # Scripts de coleta e análise (PowerShell, Python)
├── /outputs/                 # Resultados (planilhas e logs)
├── /docs/                    # Relatórios e figuras metodológicas
├── /references/              # Arquivos BibTeX e PDFs científicos
├── README.md                 # Este arquivo
└── LICENSE                   # Licença pública institucional (ANA)
</code></pre>
    </section>

    <hr />

    <section id="license">
      <h2>Licença e Uso Institucional</h2>
      <p>Este repositório faz parte de um projeto de pesquisa vinculado à <strong>Agência Nacional de Águas e Saneamento Básico (ANA)</strong>. Os dados do sistema SARSB são de uso restrito e utilizados exclusivamente para fins acadêmicos e de pesquisa científica. O código auxiliar é disponibilizado sob <strong>licença MIT</strong>.</p>
    </section>

    <hr />

    <section id="contact">
      <h2>Contato</h2>
      <div class="contact">
        <p><strong>Autor:</strong> Murillo [Sobrenome]</p>
        <p><strong>Instituição:</strong> Agência Nacional de Águas e Saneamento Básico (ANA)</p>
        <p><strong>Orientador:</strong> Prof. [Nome do orientador]</p>
        <p><strong>E-mail:</strong> murillo.[sobrenome]@ana.gov.br</p>
        <p><strong>Ano:</strong> 2025</p>
      </div>
    </section>

    <footer class="footer">
      <p>Gerado automaticamente — README convertido para HTML</p>
    </footer>
  </main>
</body>
</html>
