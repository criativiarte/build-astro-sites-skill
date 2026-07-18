# Convencoes Astro

## Versao e recursos nativos

- Preservar a versao do Astro e as integracoes oficiais de um template ou projeto existente, salvo pedido explicito de migracao.
- Respeitar uma versao definida pelo desenvolvedor.
- Quando nao houver template nem versao definida, verificar a documentacao oficial e o registro do pacote no momento da tarefa e usar a versao estavel mais recente do Astro. Nao fixar na skill um numero que ficara obsoleto.
- Ler a documentacao correspondente a major escolhida antes de configurar o projeto.
- Preferir recursos nativos estaveis dessa versao a bibliotecas externas ou implementacoes manuais equivalentes. Avaliar pelo menos assets, fontes, conteudo, componentes SVG, roteamento, prefetch, i18n, variaveis de ambiente e recursos de build quando forem pertinentes ao escopo.
- Nao habilitar recursos experimentais apenas para maximizar o uso de APIs nativas. Usar experimentais somente com justificativa e concordancia do desenvolvedor.
- Nao introduzir funcionalidades de backend apenas porque a versao escolhida as oferece.

## Estrutura preferida

Adaptar-se primeiro a estrutura existente. Para codigo novo sem convencao previa, usar:

```text
src/
  assets/
    images/
    icons/
  components/
    ui/
    layout/
    sections/
  content/
  layouts/
  pages/
  styles/
```

Colocar secoes completas em `src/components/sections`. Colocar primitives reutilizaveis em `ui` e componentes estruturais em `layout`.

## Componentes

- Nomear arquivos de componentes em PascalCase.
- Tipar todas as props.
- Usar slots quando o componente definir estrutura e o consumidor definir conteudo.
- Extrair componentes diante de repeticao real, consistencia compartilhada ou responsabilidade clara.
- Evitar componentes que apenas ocultem uma unica `div` sem semantica ou politica reutilizavel.
- Manter componentes de conteudo independentes de largura maxima.
- Criar ou reutilizar `src/components/layout/Container.astro` para o wrapper estrutural e os gutters. Fazer o componente encaminhar `class`, atributos HTML e o slot, sem impor uma largura de conteudo fixa.
- Declarar a largura em cada uso de `Container`. Na ausencia de valor fornecido pelo desenvolvedor, usar `class="mx-auto w-17/20 max-w-7xl"`.

## Imagens e assets

- Usar `Image` ou `Picture` de `astro:assets` para imagens locais quando aplicavel.
- Informar dimensoes e `alt` apropriado para evitar layout shift e preservar acessibilidade.
- Manter em `public` somente arquivos que nao devam passar pelo pipeline do Astro.
- Nomear assets em kebab-case por funcao e contexto, como `home-hero-team.webp`.
- Evitar `image-1`, `final`, `new` e nomes baseados somente na ordem de exportacao.

## Fontes

- Usar a Fonts API nativa do Astro disponivel na versao escolhida.
- Configurar familias e providers em `astro.config.*` e renderizar o componente `Font` de `astro:assets` no head compartilhado, como `BaseHead`, quando essa for a API documentada para a versao.
- Autohospedar as fontes: permitir que o Astro baixe e armazene os arquivos de um provider suportado ou usar arquivos locais. Nao carregar Google Fonts, Fontshare ou outro provider por `<link>` ou `@import` em runtime.
- Definir uma variavel CSS por familia e conecta-la aos tokens de tipografia no `@theme` do Tailwind CSS v4.
- Solicitar ou inferir a menor selecao necessaria de familias, pesos, estilos e subsets. Evitar baixar variantes sem uso.
- Aplicar preload somente a fontes realmente criticas para o primeiro viewport. Evitar preloads indiscriminados.
- Definir fallbacks coerentes e verificar layout shift, legibilidade e comportamento quando a fonte ainda nao estiver disponivel.
- Preservar a estrategia de fontes de um template existente quando ela fizer parte de sua arquitetura, salvo pedido explicito; preferir migracao para a API nativa somente quando estiver no escopo.

## Conteudo

Usar Content Collections para conteudo local estruturado, com schema e validacao. Preservar CMS ou collections existentes quando houver template. Nao duplicar o mesmo conteudo em props, arquivos e markup.

## Tailwind CSS v4

- Definir foundations e tokens semanticos no `@theme`.
- Reutilizar tokens antes de introduzir valores arbitrarios.
- Evitar listas longas de classes condicionais; modelar variantes tipadas quando necessario.
- Nao transformar valores de layout locais em tokens globais sem reutilizacao prevista.

## Icones

Usar `astro-icon` com nomes no padrao Iconify. Importar somente o necessario. Manter uma familia visual coerente e fornecer rotulo acessivel quando o icone representar uma acao sem texto visivel.

## Dependencias

- Inspecionar `package.json`, lockfile, scripts, configuracao de deploy e comandos de CI antes de classificar pacotes.
- Colocar em `devDependencies` ferramentas necessarias somente para desenvolvimento e verificacao, como lint, formatacao, testes, typecheck, Lighthouse CI e utilitarios locais.
- Colocar em `dependencies` bibliotecas importadas pela aplicacao e pacotes exigidos durante o build, deploy ou runtime de producao, conforme o contrato real da infraestrutura.
- Nao classificar um pacote apenas por ele aparecer ou nao no bundle do navegador. Considerar quando e onde ele precisa estar instalado.
- Preservar a classificacao do template quando ela refletir uma pipeline valida. Corrigir pacotes mal classificados somente depois de verificar scripts, imports e processo de deploy.
- Usar a opcao de dependencia de desenvolvimento do gerenciador escolhido, como `-D` ou `--save-dev`, para ferramentas locais.
- Nao manter o mesmo pacote simultaneamente em `dependencies` e `devDependencies`.
- Nao misturar gerenciadores de pacotes. Atualizar somente o lockfile correspondente ao projeto.
- Depois de mover ou adicionar pacotes, reinstalar de forma coerente, executar build e verificacoes e confirmar que a pipeline de producao continua encontrando tudo que precisa.

## Renderizacao e interatividade

- Pensar a implementacao visual como static-first.
- Preservar `output`, adapters e modo de renderizacao do projeto.
- Nao proibir SSR e nao o introduzir sem pedido.
- Nao tomar decisoes de backend na etapa inicial de layout.
- Preferir HTML e CSS. Adicionar JavaScript somente para comportamento real.
- Usar a menor ilha e a diretiva `client:*` mais restrita que atenda ao caso.
- Nao usar View Transitions sem pedido explicito.

## SEO e semantica

Reutilizar `BaseHead` ou equivalente. Centralizar title, description, canonical, Open Graph e demais metadados. Usar landmarks, headings hierarquicos, links e botoes de acordo com sua semantica.
