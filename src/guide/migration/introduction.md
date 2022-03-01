# Introdução

::: info
Novo no Vue.js? Veja nosso [Guia Essencial](/guide/introduction.html) para começar. 
:::

Este guia é sobretudo para usuários com experiência prévia em Vue 2 que desejam aprender sobre os novos recursos e mudanças do Vue 3. **Este não é um artigo que você precise ler do começo ao fim antes de experimentar o Vue 3.** Embora pareça que muita coisa mudou, muito do que você conhece e ama no Vue ainda é o mesmo; mas queríamos ser tão minuciosos quanto possível fornecendo explicações detalhadas e exemplos para cada alteração documentada. 

- [Início rápido](#inicio-rapido)
- [Migration Build](#migration-build)
- [Principais recursos novos](#principais-recursos-novos)
- [Incompatibilidades](#incompatibilidades)
- [Bibliotecas suportadas](#bibliotecas-suportadas)

## Visão Geral

<br>
<iframe src="https://player.vimeo.com/video/440868720" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

Comece aprendendo Vue 3 com [Vue Mastery](https://www.vuemastery.com/courses-path/vue3).

## Início Rápido

Se você quiser testar rapidamente o Vue 3 em um novo projeto:

- Via CDN: `<script src="https://unpkg.com/vue@next"></script>`
- Pelo navegador, via _playground_ em [Codepen](https://codepen.io/yyx990803/pen/OJNoaZL)
- Pelo navegador, via Sandbox em [CodeSandbox](https://v3.vue.new)
- Pré-estruturado, via [Vite](https://github.com/vitejs/vite):

  ```bash
  npm init vite hello-vue3 -- --template vue # OU yarn create vite hello-vue3 --template vue
  ``` 

- Pré-estruturado, via [vue-cli](https://cli.vuejs.org/):

  ```bash
  npm install -g @vue/cli # OU yarn global add @vue/cli
  vue create hello-vue3
  # selecione a predefinição vue 3
  ```

## Compilação de Migração

Se você tem um projeto ou biblioteca do Vue 2 existente que pretende atualizar para o Vue 3, fornecemos uma versão do Vue 3 que oferece APIs compatíveis com o Vue 2. Verifique a página [Compilação de Migração](./migration-build.html) para obter mais detalhes.

## Principais Recursos Novos

Alguns dos recursos novos para ficar de olho no Vue 3 incluem:

- [API de Composição](/guide/composition-api-introduction.html)
- [Teleporte](/guide/teleport.html)
- [Fragmentos](/guide/migration/fragments.html)
- [Opções para emitir eventos de componentes](/guide/component-custom-events.html)
- [API `createRenderer` de `@vue/runtime-core`](https://github.com/vuejs/vue-next/tree/master/packages/runtime-core) para criar renderizações custumizadas
- [Açúcar sintático para SFC que utilizem API de Composição (`<script setup>`)](/api/sfc-script-setup.html)
- [Variáveis CSS baseadas em estado de SFC (`v-bind` no `<style>`)](/api/sfc-style.html#state-driven-dynamic-css)
- [`<style scoped>` de SFC agora pode incluir regras globais ou regras que visam apenas conteúdo de _slot_](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0023-scoped-styles-changes.md)
- [Suspense](/guide/migration/suspense.html) <Badge text="experimental" type="warning" />

## Incompatibilidades

A seguir, uma lista de mudanças incompatíveis com v2.x:

### API Global

- [API Global do Vue agora utiliza uma instância da aplicação](/guide/migration/global-api.html)
- [API Global e internas foram reestruturadas para serem _tree-shakable_](/guide/migration/global-api-treeshaking.html)

### Diretivas de _Template_

- [O uso de `v-model` em componentes foi retrabalhado, substituindo o `v-bind.sync`](/guide/migration/v-model.html)
- [O atributo `key` em `<template v-for>` e nós que não sejam `v-for` foi alterado](/guide/migration/key-attribute.html)
- [A precedência de `v-if` e `v-for` quando usados no mesmo elemento foi modificada](/guide/migration/v-if-v-for.html)
- [`v-bind="object"` agora é sensível à ordem de disposição](/guide/migration/v-bind.html)
- [modificador `v-on:event.native` foi removido](./v-on-native-modifier-removed.md)
- [`ref` em `v-for` não resulta mais em um array de refs](/guide/migration/array-refs.html)

### Componentes

- [Componentes funcionais só podem ser criados usando uma função simples](/guide/migration/functional-components.html)
- [O atributo `functional` no `<template>` de Componentes Single File (CSF) e a opção de componente `functional` estão obsoletas](/guide/migration/functional-components.html)
- [Componentes assíncronos necessitam de um método `defineAsyncComponent` para serem criados](/guide/migration/async-components.html)
- [Os eventos de componente agora devem ser declarados com a opção `emits`](./emits-option.md)

### Funções de Renderização

- [A API da função de renderização foi modificada](/guide/migration/render-function-api.html)
- [A propriedade `$scopedSlots` foi removida e todos os seus _slots_ passam a ser obtidos como funções através de `$slots`](/guide/migration/slots-unification.html)
- [`$listeners` foi removida/mesclada em `$attrs`](./listeners-removed)
- [`$attrs` agora inclui os atributos `class` e `style`](./attrs-includes-class-style.md)

### Elementos Personalizados

- [A lista de permissões para elementos personalizados agora é realizada durante a compilação do _template_](/guide/migration/custom-elements-interop.html)
- [O atributo especial `is` está restrito apenas à _tag_ `<component>`](/guide/migration/custom-elements-interop.html#customized-built-in-elements)

### Outras Mudanças Menores

- A opção de ciclo de vida `destroyed` foi renomeada para `unmounted`
- A opção de ciclo de vida `beforeDestroy` foi renomeada para `beforeUnmount`
- [A função fabricadora de props `default` não acessa mais o contexto `this`](/guide/migration/props-default-this.html)
- [A API de diretivas customizadas foi modificada para se alinhar ao ciclo de vida do componente e `binding.expression` foi removido](/guide/migration/custom-directives.html)
- [A opção `data` deverá sempre ser declarada como uma função](/guide/migration/data-option.html)
- [A opção `data` dos _mixins_ agora é mesclada superficialmente](/guide/migration/data-option.html#mixin-merge-behavior-change)
- [Estratégia de coerção de atributos foi alterada](/guide/migration/attribute-coercion.html)
- [Algumas classes de transição foram renomeadas](/guide/migration/transition.html)
- [O `callback` de um `array` que está sendo observado só será acionado quando este for substituído. Caso você precise dispará-lo em mutação, a opção `deep` deve ser especificada.](/guide/migration/watch.html)
- As tags `<template>` sem diretivas especiais (`v-if/else-if/else`, `v-for`, ou `v-slot`) agora são tratadas como elementos simples resultando em um elemento `<template>` nativo ao invés de renderizar seu conteúdo interno.
- [O aplicativo montado não substitui o elemento no qual está montado](/guide/migration/mount-changes.html)
- [Prefixo `hook:` de eventos de ciclo de vida alterado para `vnode-`](/guide/migration/vnode-lifecycle-events.html)

### APIs Removidas 

- [Suporte a `keyCode` como modificadores `v-on`](/guide/migration/keycode-modifiers.html)
- [Métodos de instância $on, $off e $once](/guide/migration/events-api.html)
- [Filtros](/guide/migration/filters.html)
- [Atributos _inline_ em _templates_](/guide/migration/inline-template-attribute.html)
- [Propriedade de instância `$children`](/guide/migration/children.html)
- [Opção `propsData`](/guide/migration/props-data.html)
- Método de instância `$destroy`. Os usuários não devem mais acessar manualmente o ciclo de vida de componentes Vue individuais.
- Funções globais `set` e `delete`, e os métodos de instância `$set` e `$delete`. Eles não são mais necessários com a detecção de alterações baseada em proxy.

## Bibliotecas Suportadas

Todas as nossas bibliotecas e ferramentas oficiais agora oferecem suporte ao Vue 3, mas, algumas delas ainda estão em _status_ beta ou de candidata a lançamento. Você encontrará detalhes para as bibliotecas individuais abaixo. A maioria atualmente é distribuída usando a tag `next` no npm. Pretendemos mudar para `latest` assim que todas as bibliotecas oficiais tiverem versões estáveis ​​e compatíveis.

### Vue CLI

<a href="https://www.npmjs.com/package/@vue/cli" target="_blank" noopener noreferrer><img src="https://img.shields.io/npm/v/@vue/cli"></a>

A partir da v4.5.0, `vue-cli` agora oferece a opção integrada para escolher o Vue 3 ao criar um novo projeto. Você pode atualizar o `vue-cli` e executar o `vue create` para criar um projeto Vue 3 hoje.

- [Documentação](https://cli.vuejs.org/)
- [GitHub](https://github.com/vuejs/vue-cli)

### Vue Router

<a href="https://www.npmjs.com/package/vue-router/v/next" target="_blank" noopener noreferrer><img src="https://img.shields.io/npm/v/vue-router/next.svg"></a>

Vue Router 4.0 provê suporte ao Vue 3 e possui uma série de modificações incompatíveis próprias. Leia o [guia de migração](https://next.router.vuejs.org/guide/migration/) para verificar todos os detalhes.

- [Documentation](https://next.router.vuejs.org/)
- [GitHub](https://github.com/vuejs/vue-router-next)
- [RFCs](https://github.com/vuejs/rfcs/pulls?q=is%3Apr+is%3Amerged+label%3Arouter)

### Vuex

<a href="https://www.npmjs.com/package/vuex/v/next" target="_blank" noopener noreferrer><img src="https://img.shields.io/npm/v/vuex/next.svg"></a>

Vuex 4.0 provê suporte ao Vue 3 com basicamente a mesma API que o 3.x. A única modificação incompatível é em [como o plugin é instalado](https://next.vuex.vuejs.org/guide/migrating-to-4-0-from-3-x.html#breaking-changes).

- [Documentation](https://next.vuex.vuejs.org/)
- [GitHub](https://github.com/vuejs/vuex/tree/4.0)

### Extensão para Desenvolvedores

Estamos trabalhando em uma nova versão do _Devtools_ com uma nova interface e refatoração interna para oferecer suporte a várias versões do Vue. A nova versão está atualmente em beta e suporta apenas Vue 3 (por enquanto). A integração do Vuex e do Router também está em andamento.

- Para navegador Chrome: [Instale da Chrome web store](https://chrome.google.com/webstore/detail/vuejs-devtools/ljjemllljcmogpfapbkkighbhhppjdbg?hl=en)

  - Nota: o canal beta pode entrar em conflito com a versão estável do _devtools_, então pode ser necessário desabilitar temporariamente a versão estável para que a versão beta funcione corretamente.

- Para navegador Firefox: [Baixe a extensão assinada](https://github.com/vuejs/vue-devtools/releases/tag/v6.0.0-beta.20) (Arquivo `.xpi` em Assets)

### Suporte de IDE

É recomendado o uso do [VSCode](https://code.visualstudio.com/) com a extensão oficial [Volar](https://github.com/johnsoncodehk/volar), qual provê suporte à IDE para Vue 3.

### Outros Projetos

| Projeto               | NPM                           | Repositório          |
| --------------------- | ----------------------------- | -------------------- |
| @vue/babel-plugin-jsx | [![rc][jsx-badge]][jsx-npm]   | [[GitHub][jsx-code]] |
| eslint-plugin-vue     | [![ga][epv-badge]][epv-npm]   | [[GitHub][epv-code]] |
| @vue/test-utils       | [![beta][vtu-badge]][vtu-npm] | [[GitHub][vtu-code]] |
| vue-class-component   | [![beta][vcc-badge]][vcc-npm] | [[GitHub][vcc-code]] |
| vue-loader            | [![rc][vl-badge]][vl-npm]     | [[GitHub][vl-code]]  |
| rollup-plugin-vue     | [![beta][rpv-badge]][rpv-npm] | [[GitHub][rpv-code]] |

[jsx-badge]: https://img.shields.io/npm/v/@vue/babel-plugin-jsx.svg
[jsx-npm]: https://www.npmjs.com/package/@vue/babel-plugin-jsx
[jsx-code]: https://github.com/vuejs/jsx-next
[vd-badge]: https://img.shields.io/npm/v/@vue/devtools/beta.svg
[vd-npm]: https://www.npmjs.com/package/@vue/devtools/v/beta
[vd-code]: https://github.com/vuejs/vue-devtools/tree/next
[epv-badge]: https://img.shields.io/npm/v/eslint-plugin-vue.svg
[epv-npm]: https://www.npmjs.com/package/eslint-plugin-vue
[epv-code]: https://github.com/vuejs/eslint-plugin-vue
[vtu-badge]: https://img.shields.io/npm/v/@vue/test-utils/next.svg
[vtu-npm]: https://www.npmjs.com/package/@vue/test-utils/v/next
[vtu-code]: https://github.com/vuejs/vue-test-utils-next
[jsx-badge]: https://img.shields.io/npm/v/@ant-design-vue/babel-plugin-jsx.svg
[jsx-npm]: https://www.npmjs.com/package/@ant-design-vue/babel-plugin-jsx
[jsx-code]: https://github.com/vueComponent/jsx
[vcc-badge]: https://img.shields.io/npm/v/vue-class-component/next.svg
[vcc-npm]: https://www.npmjs.com/package/vue-class-component/v/next
[vcc-code]: https://github.com/vuejs/vue-class-component/tree/next
[vl-badge]: https://img.shields.io/npm/v/vue-loader/next.svg
[vl-npm]: https://www.npmjs.com/package/vue-loader/v/next
[vl-code]: https://github.com/vuejs/vue-loader/tree/next
[rpv-badge]: https://img.shields.io/npm/v/rollup-plugin-vue/next.svg
[rpv-npm]: https://www.npmjs.com/package/rollup-plugin-vue/v/next
[rpv-code]: https://github.com/vuejs/rollup-plugin-vue/tree/next

::: info
Para obter informações adicionais sobre a compatibilidade do Vue 3 com bibliotecas e plug-ins, certifique-se de verificar [esta issue no awesome-vue](https://github.com/vuejs/awesome-vue/issues/3544).
:::
