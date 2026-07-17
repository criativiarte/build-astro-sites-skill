# Build Astro Sites

`build-astro-sites` é uma skill para o Codex implementar interfaces do Figma em projetos Astro. Ela pode criar a estrutura visual de um site novo ou adaptar um projeto existente sem reescrever a lógica que já funciona.

O Figma orienta a apresentação visual. Quando um template é fornecido, o código existente orienta a arquitetura funcional: layouts, CMS, busca, listings, páginas de conteúdo, rotas, SEO e contratos de dados são preservados sempre que possível.

## O que a skill oferece

- Leitura do design pelo plugin do Figma.
- Implementação em Astro com abordagem static-first.
- Tailwind CSS v4 com tokens semânticos definidos em `@theme`.
- Componentes reutilizáveis e seções organizadas em `src/components/sections`.
- Content Collections para conteúdo local estruturado.
- `Image`, `Picture`, Fonts API e outros recursos nativos do Astro quando adequados.
- Fontes autohospedadas, sem dependência de serviços de fontes no navegador.
- `astro-icon` com nomes de ícones no padrão Iconify.
- Preservação da estratégia de SSG ou SSR de projetos existentes.
- Validação de responsividade, acessibilidade, SEO, tipos e build.

View Transitions não são habilitadas automaticamente. Recursos experimentais e decisões de backend também ficam fora do escopo, a menos que sejam solicitados explicitamente.

## Pré-requisitos

Antes de usar a skill, confirme que você possui:

- Codex com suporte a Agent Skills;
- plugin do Figma instalado e autorizado;
- acesso ao arquivo do Figma e aos frames que serão implementados;
- acesso de leitura e escrita ao projeto de destino.

Um template Astro é opcional. Caso exista, forneça o caminho local ou a URL do repositório junto com o pedido.

## Instalação

### Com o Skill Installer

Peça ao Codex para instalar diretamente a pasta da skill:

```text
Use $skill-installer para instalar esta skill:
https://github.com/criativiarte/build-astro-sites/tree/main/skills/build-astro-sites
```

Se a skill não aparecer após a instalação, reinicie o Codex.

### Instalação manual para o usuário

Copie `skills/build-astro-sites` deste repositório para:

```text
$HOME/.agents/skills/build-astro-sites
```

No Windows, `$HOME` normalmente corresponde a `C:\Users\SEU-USUARIO`.

### Instalação em um projeto

Para disponibilizar a skill apenas em um repositório, copie-a para:

```text
seu-projeto/
└── .agents/
    └── skills/
        └── build-astro-sites/
            ├── SKILL.md
            ├── agents/
            └── references/
```

O Codex detecta skills em `.agents/skills` quando trabalha dentro do projeto.

## Como usar

Invoque a skill pelo nome e informe, no mínimo, o arquivo do Figma, o projeto de destino e as páginas ou seções desejadas:

```text
Use $build-astro-sites para implementar este design em Astro.

Figma: <URL_DO_FIGMA>
Projeto: <CAMINHO_DO_PROJETO>
Páginas: Home, Busca e Post
```

Para obter um resultado mais previsível, também informe:

- frames ou node IDs que devem ser usados;
- breakpoints ou comportamentos responsivos conhecidos;
- conteúdo real ou fontes de conteúdo disponíveis;
- restrições de componentes, bibliotecas ou hospedagem;
- comandos de validação exigidos pelo projeto;
- versão do Astro, quando houver uma versão obrigatória.

## Uso sem template

Quando não houver projeto-base, deixe isso explícito:

```text
Use $build-astro-sites para criar em Astro o layout deste Figma.

Figma: <URL_DO_FIGMA>
Projeto: <CAMINHO_DO_NOVO_PROJETO>
Não há template existente.
Implemente apenas a camada visual e não introduza backend.
```

Se nenhuma versão for definida, a skill consulta e utiliza a versão estável mais recente do Astro. A implementação prioriza recursos nativos dessa versão antes de adicionar dependências externas.

## Uso com template

Quando houver um template ou projeto existente, informe sua localização e o que precisa ser preservado:

```text
Use $build-astro-sites para aplicar este Figma ao projeto existente.

Figma: <URL_DO_FIGMA>
Projeto: <CAMINHO_DO_PROJETO>
Template: <URL_OU_CAMINHO_DO_TEMPLATE>

Preserve BaseLayout, BaseHead, CMS, busca, listings, rotas e contratos de dados.
Adapte a camada visual sem reescrever a lógica existente.
```

Nesse fluxo, a skill primeiro identifica os componentes e contratos disponíveis. Cada elemento é classificado para reutilização, reestilização, composição, adaptação ou criação. A versão do Astro, o modo de renderização e as integrações existentes são mantidos, salvo solicitação explícita de migração.

## Convenções aplicadas

### Componentes e seções

Elementos repetitivos são extraídos para componentes quando existe responsabilidade clara ou ganho real de consistência. Seções completas de página ficam em `src/components/sections`.

### Container

A skill cria ou reutiliza `src/components/layout/Container.astro`. O componente oferece o wrapper estrutural, mas a largura continua visível no ponto de composição.

Quando nenhuma largura for especificada, o padrão é:

```astro
<Container class="mx-auto w-17/20 max-w-7xl">
  <PostListing />
</Container>
```

Componentes como `PostListing`, `Search` e `PostCard` não devem impor sua própria largura máxima.

### Fontes

As famílias tipográficas são configuradas com a Fonts API da versão escolhida do Astro. Os arquivos são baixados ou lidos localmente durante o processo de build e servidos pelo próprio site.

A skill evita `<link>` e `@import` para serviços externos de fontes em runtime, limita pesos e subsets ao necessário e aplica preload apenas às fontes críticas para o primeiro viewport.

### Assets e ícones

Imagens locais usam `Image` ou `Picture` de `astro:assets` quando aplicável. Assets recebem nomes descritivos em kebab-case, como `home-hero-team.webp`.

Ícones usam `astro-icon` e identificadores Iconify. A família visual deve permanecer consistente e ações sem texto visível precisam de nome acessível.

## Resultado esperado

Ao concluir a implementação, o Codex deve informar:

- componentes criados, reutilizados ou adaptados;
- tokens adicionados ao design system;
- decisões responsivas relevantes;
- comandos de validação executados;
- pendências que dependam de conteúdo, backend ou decisão do desenvolvedor.

## Licença

Distribuído sob a licença MIT. Consulte [LICENSE](LICENSE) para os termos completos.
