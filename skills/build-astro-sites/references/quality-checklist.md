# Checklist de qualidade

## Antes de editar

- Confirmar escopo, rotas e frames do Figma.
- Confirmar se existe template opcional.
- Inventariar arquitetura, componentes e consumidores existentes.
- Identificar tokens, assets e estados.

## Implementacao

- Preservar contratos funcionais e configuracao de renderizacao.
- Manter secoes em `src/components/sections`.
- Criar ou reutilizar o componente externo `Container`.
- Declarar a largura em cada uso do `Container`; usar `mx-auto w-17/20 max-w-7xl` quando o desenvolvedor nao especificar outro valor.
- Manter largura e max-width fora dos componentes de conteudo.
- Usar `Image` ou `Picture` quando aplicavel.
- Usar a Fonts API do Astro e servir fontes pelo proprio site, sem requisicoes de fontes a terceiros em runtime.
- Quando nao houver template nem versao especificada, confirmar o uso da versao estavel mais recente do Astro disponivel no momento da implementacao.
- Confirmar que recursos nativos adequados da versao escolhida foram preferidos a dependencias externas equivalentes.
- Revisar `dependencies` e `devDependencies`; manter ferramentas exclusivamente locais em `devDependencies` e pacotes exigidos pelo build, deploy ou runtime no grupo compativel com a infraestrutura.
- Confirmar que nao ha pacote duplicado entre os dois grupos nem lockfiles de gerenciadores diferentes.
- Usar `astro-icon` com padrao Iconify.
- Definir tokens no `@theme` sem duplicacao desnecessaria.
- Nao adicionar View Transitions.
- Nao introduzir backend, SSR, adapter ou JavaScript sem necessidade solicitada.

## Validacao visual

- Comparar hierarquia, espacamento, tipografia, cores, bordas e proporcoes com o Figma.
- Testar mobile, desktop e larguras intermediarias.
- Testar conteudo longo, listas variaveis e assets ausentes.
- Verificar estados interativos pertencentes ao escopo.

## Acessibilidade e SEO

- Verificar landmarks e hierarquia de headings.
- Navegar somente por teclado e confirmar foco visivel.
- Confirmar contraste, labels, nomes acessiveis e textos alternativos.
- Confirmar fallbacks tipograficos, apenas pesos e subsets necessarios, e preload restrito a fontes criticas.
- Respeitar `prefers-reduced-motion` quando houver animacao solicitada.
- Confirmar title, description, canonical e metadados sociais quando aplicaveis.

## Codigo e build

- Executar formatacao, lint, typecheck e testes configurados no projeto.
- Executar build de producao.
- Confirmar que a estrategia de instalacao usada pela CI ou hospedagem disponibiliza todas as dependencias necessarias antes do build e no runtime.
- Executar Lighthouse CI em tres rodadas por rota representativa depois do build.
- Exigir, na ausencia de limites do projeto: performance `0.90`, accessibility `1.00`, best-practices `0.95` e seo `0.95`.
- Salvar relatorios no filesystem, sem upload publico, e informar o caminho na entrega.
- Se Chrome ou Chromium estiver indisponivel, registrar a auditoria como nao executada e nunca como aprovada.
- Corrigir warnings introduzidos pela mudanca.
- Verificar rotas e links internos afetados.
- Confirmar que nenhuma configuracao de backend ou renderizacao mudou por acidente.
- Revisar o diff e remover duplicacao, codigo morto e assets sem uso introduzidos pela tarefa.

## Entrega

Informar componentes reutilizados e criados, tokens adicionados, principais decisoes responsivas, comandos executados, scores e rotas do Lighthouse, caminho dos relatorios e pendencias que dependam do desenvolvedor ou do backend.
