# Auditoria automatica com Lighthouse CI

## Objetivo

Executar Lighthouse CI depois do build para detectar regressoes de performance, acessibilidade, boas praticas e SEO. Tratar o resultado como complemento, nao substituto, das verificacoes manuais de teclado, foco, semantica e conteudo.

## Preparar o projeto

1. Identificar o gerenciador de pacotes e os scripts existentes.
2. Procurar `lighthouserc.*`, dependencia `@lhci/cli` e scripts de auditoria.
3. Preservar a configuracao existente e seus limites. Nao reduzir um limite para fazer a auditoria passar.
4. Quando nao houver integracao, adicionar `@lhci/cli` como dependencia de desenvolvimento usando o gerenciador do projeto.
5. Criar `lighthouserc.cjs` ou o formato ja adotado pelo repositorio.
6. Adicionar `.lighthouseci/` ao `.gitignore`, salvo decisao explicita de versionar relatorios.

## Usar limites padrao

Quando o desenvolvedor ou o projeto nao definirem outros limites, usar:

- performance: `0.90`;
- accessibility: `1.00`;
- best-practices: `0.95`;
- seo: `0.95`.

Usar tres execucoes por rota para reduzir variacao. Configurar falha de processo quando um limite nao for atingido.

Exemplo base para um site estatico:

```js
module.exports = {
  ci: {
    collect: {
      staticDistDir: "./dist",
      numberOfRuns: 3,
    },
    assert: {
      assertions: {
        "categories:performance": ["error", { minScore: 0.9 }],
        "categories:accessibility": ["error", { minScore: 1 }],
        "categories:best-practices": ["error", { minScore: 0.95 }],
        "categories:seo": ["error", { minScore: 0.95 }],
      },
    },
    upload: {
      target: "filesystem",
      outputDir: "./.lighthouseci/reports",
    },
  },
};
```

Adaptar a sintaxe a versao instalada do Lighthouse CI e validar a configuracao na documentacao oficial atual antes de usa-la.

## Escolher as rotas

Auditar uma amostra pequena que represente arquiteturas diferentes:

- pagina inicial;
- um listing ou categoria;
- uma pagina de post ou detalhe;
- busca, quando puder ser executada localmente;
- qualquer pagina com estrutura ou interatividade substancialmente diferente.

Evitar auditar milhares de paginas estaticas equivalentes. Se `staticDistDir` descobrir rotas demais, configurar um servidor local com `collect.startServerCommand` e listar URLs representativas em `collect.url`.

## Executar

1. Executar o build de producao.
2. Executar `lhci autorun` pelo gerenciador do projeto.
3. Corrigir falhas introduzidas pela implementacao.
4. Repetir a auditoria depois das correcoes.
5. Informar scores, rotas auditadas e caminho dos relatorios.

Nao usar `temporary-public-storage`. Manter `upload.target` como `filesystem`, a menos que o desenvolvedor forneca uma infraestrutura privada de Lighthouse CI.

## Tratar impedimentos

Lighthouse CLI precisa de Chrome ou Chromium. Quando o navegador nao estiver disponivel:

- procurar um executavel configurado pelo projeto;
- nao instalar navegador ou alterar CI sem autorizacao;
- registrar a auditoria como nao executada;
- informar o comando que deve ser repetido em um ambiente compativel;
- nao apresentar scores presumidos nem declarar sucesso.

Se a instalacao de dependencias estiver bloqueada, preservar o projeto e informar o bloqueio. Falha de rede ou variacao de performance nao deve ocultar falhas deterministicas de acessibilidade, boas praticas ou SEO.
