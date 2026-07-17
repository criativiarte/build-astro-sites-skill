# Template opcional e arquitetura existente

## Principio

Usar o template somente quando o desenvolvedor o fornecer. Nao exigir um template para iniciar e nao embutir, procurar ou escolher um template por conta propria.

Quando houver template, considerar:

- o template como fonte da arquitetura funcional;
- o Figma como fonte da apresentacao visual;
- o pedido do desenvolvedor como autoridade para excecoes.

## Inventariar antes de editar

Localizar e entender, quando existirem:

- `BaseLayout`, `BaseHead` e layouts especializados;
- CMS, Content Collections, schemas e tipos;
- busca, filtros, ordenacao e paginacao;
- listings, cards, grids, resultados e estados vazios;
- paginas de post, categoria, tag, autor e busca;
- rotas, slugs e `getStaticPaths()`;
- SEO, canonical, Open Graph, JSON-LD, sitemap e robots;
- imagens, fontes, icones, analytics e utilitarios;
- configuracao `output`, adapters, endpoints e integracoes externas.

Usar `rg` e leitura direcionada para encontrar definicoes e consumidores. Nao concluir que um componente esta sem uso antes de procurar referencias.

## Classificar cada elemento

- **Reutilizar:** logica e visual ja atendem.
- **Reestilizar:** manter props, markup essencial e comportamento; trocar a apresentacao.
- **Compor:** inserir componentes funcionais existentes em uma nova secao ou layout.
- **Adaptar:** criar uma camada visual fina sobre uma interface existente.
- **Criar:** implementar somente quando nao existir equivalente util.

Evitar duplicatas como `PostCardNew`, `PostCardV2` ou `SearchUpdated`. Preferir evoluir o componente correto ou criar uma variante tipada quando os usos realmente divergirem.

## Preservar contratos

Preservar por padrao:

- props e tipos publicos;
- origem, formato e transformacao dos dados;
- consultas e integracao com CMS;
- busca, filtros, paginacao e ordenacao;
- rotas, slugs e metadados;
- regras de negocio;
- configuracao de SSG, SSR e deploy.

Antes de alterar uma interface, localizar todos os consumidores e avaliar compatibilidade. Preferir adaptadores locais a uma alteracao transversal durante trabalho visual.

## Limitar o escopo

- Nao reescrever CMS, busca, collections, endpoints ou autenticacao por conveniencia.
- Nao substituir bibliotecas funcionais sem motivo verificavel.
- Nao alterar adapters, deploy ou estrategia de renderizacao.
- Nao remover recursos apenas porque nao aparecem no frame atual do Figma.
- Registrar uma necessidade de backend como pendencia quando ela nao puder ser resolvida somente na apresentacao.

## Sem template

Criar somente a base necessaria para o pedido. Usar as convencoes Astro da skill, manter a arquitetura pequena e permitir extensao futura. Nao inventar CMS, busca, autenticacao ou backend sem requisito.
