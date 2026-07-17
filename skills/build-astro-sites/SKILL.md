---
name: build-astro-sites
description: Criar ou adaptar sites profissionais em Astro a partir de designs do Figma, atuando como web designer senior e desenvolvedor frontend. Usar quando Codex precisar transformar telas, paginas, secoes ou componentes do Figma em um site Astro com Tailwind CSS v4, astro-icon, imagens otimizadas, Content Collections, componentes reutilizaveis e foco static-first; preservar a arquitetura funcional de um template existente quando o desenvolvedor fornecer um, sem tomar decisoes de backend nao solicitadas.
---

# Build Astro Sites

Atuar como web designer senior e desenvolvedor frontend experiente. Tratar o Figma como fonte da apresentacao visual. Quando houver template, tratar o template como fonte da arquitetura funcional.

## Carregar orientacoes

- Ler [references/template-architecture.md](references/template-architecture.md) quando um template, repositorio ou projeto existente for fornecido.
- Ler [references/figma-design-system.md](references/figma-design-system.md) antes de inspecionar o Figma ou implementar estilos.
- Ler [references/astro-conventions.md](references/astro-conventions.md) antes de criar ou reorganizar codigo Astro.
- Ler [references/quality-checklist.md](references/quality-checklist.md) antes da validacao final.

## Seguir o fluxo

1. Inspecionar o pedido, o Figma, o repositorio atual e o template opcional antes de editar.
2. Usar o plugin do Figma. Carregar e seguir as skills obrigatorias do plugin antes de qualquer chamada, especialmente `figma-use` e `figma-generate-design` quando aplicaveis.
3. Inventariar paginas, secoes, componentes, estados, assets, tokens, conteudo e comportamentos.
4. Se houver template, mapear sua arquitetura funcional e classificar cada parte como reutilizar, reestilizar, compor, adaptar ou criar.
5. Definir o design system no `@theme` do Tailwind CSS v4. Criar valores personalizados somente quando o design ou a coerencia do sistema exigir.
6. Planejar componentes e limites de responsabilidade antes de montar as paginas.
7. Implementar foundations, layouts, elementos reutilizaveis e secoes, nessa ordem.
8. Integrar conteudo, imagens e icones sem alterar contratos funcionais desnecessariamente.
9. Validar fidelidade visual, responsividade, acessibilidade, SEO, performance, tipos e build.

## Aplicar regras obrigatorias

- Usar Astro e preferir sua renderizacao estatica para o trabalho de layout.
- Quando nao houver template nem versao especificada pelo desenvolvedor, consultar as fontes oficiais atuais e iniciar o projeto com a versao estavel mais recente do Astro. Nao atualizar por conta propria a versao de um template ou projeto existente.
- Conhecer a documentacao da versao escolhida e preferir o maximo de recursos nativos adequados antes de adicionar bibliotecas, integracoes ou implementacoes manuais.
- Nao proibir nem introduzir SSR. Preservar a configuracao existente e deixar decisoes de backend para o desenvolvedor, salvo pedido explicito.
- Nao instalar adapters, alterar `output`, redesenhar APIs, reescrever CMS ou mudar estrategia de renderizacao durante uma tarefa visual sem solicitacao.
- Usar componentes nativos do Astro quando houver solucao adequada, principalmente `Image` e `Picture` para assets locais.
- Usar a Fonts API nativa do Astro para fontes autohospedadas. Configurar as familias no Astro, servir os arquivos pelo proprio site e usar o componente `Font` de `astro:assets` conforme a API da versao escolhida. Nao depender de folhas de estilo de fontes carregadas em runtime por terceiros.
- Usar Content Collections para conteudo local estruturado quando fizer sentido ou preservar a integracao de conteudo existente.
- Usar Tailwind CSS v4 e definir tokens semanticos em `@theme`.
- Usar `astro-icon` com nomes de icones no padrao Iconify. Nao misturar familias visuais sem justificativa.
- Nao habilitar View Transitions, salvo pedido explicito.
- Preferir zero JavaScript no cliente. Adicionar uma ilha somente para interatividade real e usar a menor diretiva `client:*` adequada.
- Criar componentes para elementos realmente repetitivos, responsabilidades claras ou consistencia sistemica. Evitar abstracoes prematuras.
- Colocar secoes de pagina em `src/components/sections`.
- Criar ou reutilizar um componente `Container` externo para compor o conteudo. Manter largura e max-width fora dos componentes de conteudo e explicitos em cada uso do `Container`. Quando o desenvolvedor nao definir a largura, usar `mx-auto w-17/20 max-w-7xl` no ponto de uso ou composicao.
- Nomear componentes em PascalCase e assets em kebab-case com nomes descritivos e orientados ao uso.
- Preservar HTML semantico, navegacao por teclado, foco visivel, contraste, hierarquia de headings, labels e preferencias de movimento reduzido.
- Tipar props, evitar `any`, numeros magicos, estilos inline e classes arbitrarias repetidas.
- Manter a mudanca minima necessaria. Nao fazer refatoracoes amplas sem relacao com o design solicitado.

## Tomar decisoes de design senior

- Inferir comportamento responsivo entre os frames fornecidos sem copiar coordenadas absolutas.
- Converter Auto Layout em fluxo semantico com grid, flexbox e spacing tokens.
- Preservar ritmo visual, hierarquia, densidade, legibilidade e consistencia, nao apenas medidas isoladas.
- Identificar estados ausentes como hover, focus, active, loading, vazio, erro e conteudo longo. Implementar apenas os que pertencem ao escopo e registrar lacunas relevantes.
- Explicar brevemente qualquer decisao visual importante que nao esteja definida no Figma.

## Encerrar o trabalho

- Executar os comandos de verificacao definidos pelo projeto, incluindo typecheck e build quando disponiveis.
- Confirmar que nenhuma decisao de backend foi introduzida por acidente.
- Resumir componentes criados ou reutilizados, tokens definidos, comportamento responsivo, validacoes executadas e pendencias reais.
