# Figma e design system

## Usar o plugin do Figma

Carregar as skills do plugin exigidas para cada operacao antes de chamar suas ferramentas. Usar `figma-generate-design` para traduzir telas ou layouts compostos e `figma-use` quando a operacao exigir execucao no contexto do arquivo.

Inspecionar antes de codificar:

- frames e hierarquia das paginas;
- variables, styles e modos de tema;
- componentes, variantes e instancias;
- Auto Layout, constraints e grids;
- tipografia, cores, espacos, raios, sombras e bordas;
- assets exportaveis;
- estados interativos e frames responsivos.

Nao trabalhar somente a partir de uma captura quando o arquivo Figma estiver acessivel.

## Mapear o sistema

Criar um mapa curto entre:

- tokens do Figma e tokens `@theme`;
- componentes do Figma e componentes Astro;
- frames e rotas;
- secoes visuais e `src/components/sections`;
- variantes visuais e props tipadas.

Reutilizar tokens existentes do projeto quando forem semanticamente equivalentes. Criar novos valores apenas quando necessario.

## Definir tokens semanticos

Preferir nomes por funcao, como:

- `--color-surface`, `--color-surface-muted`;
- `--color-text`, `--color-text-muted`;
- `--color-border`, `--color-action`, `--color-danger`;
- tokens de fonte, leading, tracking, spacing, radius, shadow e container.

Evitar nomes presos a aparencia como `blue-button` ou `gray-card`. Nao transformar todo valor pontual do Figma em token global.

## Projetar responsividade

- Implementar mobile-first.
- Tratar frames como pontos de referencia, nao como os unicos tamanhos validos.
- Testar larguras intermediarias, conteudo longo, quantidades variaveis e ausencia de imagem.
- Converter posicionamento em grid, flexbox e fluxo do documento.
- Evitar breakpoints especificos para modelos de dispositivo.

## Containers

Criar ou reutilizar um componente `Container` para padronizar o wrapper estrutural e os gutters. Nao embutir nele uma largura de conteudo rigida: receber e encaminhar `class` para que a largura seja visivel em cada ponto de composicao.

Quando o desenvolvedor nao fornecer uma largura, usar `w-17/20 max-w-7xl` como padrao e manter `mx-auto` no uso do `Container`:

```astro
<Section>
  <Container class="mx-auto w-17/20 max-w-7xl">
    <PostListing />
  </Container>
</Section>
```

Repetir a declaracao de largura em cada uso para preservar a intencao local e permitir variacoes explicitas. Quando o desenvolvedor especificar outro valor, respeita-lo no ponto de uso. Nao colocar largura ou largura maxima em `PostListing`, `Search`, `PostCard` ou outro componente de conteudo reutilizavel.

## Cobrir estados

Verificar hover, focus-visible, active, disabled, loading, vazio, erro, conteudo longo e imagem ausente. Nao inventar comportamento de negocio. Implementar estados visuais pertencentes ao escopo e registrar os demais.

Nao adicionar View Transitions sem pedido explicito.
