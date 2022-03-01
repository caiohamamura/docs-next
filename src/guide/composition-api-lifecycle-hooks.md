# Gatilhos de Ciclo de Vida

> Esta seção usa a sintaxe de [componente single-file](single-file-component.html) para exemplos de código

> Este guia assume que você já leu a [Introdução à API de Composição](composition-api-introduction.html) e [Fundamentos da Reatividade](reactivity-fundamentals.html). Leia elas primeiro se você for novo no assunto de API de Composição.

<VideoLesson href="https://www.vuemastery.com/courses/vue-3-essentials/lifecycle-hooks" title="Saiba mais sobre como os Gatilhos de Ciclo de Vida funcionam com o Vue Mastery">Assista à um vídeo grátis sobre Gatilhos de Ciclo de Vida no Vue Mastery</VideoLesson>

Você pode acessar um gatilho de ciclo de vida de um componente prefixando o gatilho com "on".

A tabela a seguir contém como os gatilhos de ciclo de vida são chamados dentro de [setup()](composition-api-setup.html):

| API de Opções     | Gatilho dentro de `setup`  |
| ----------------- | -------------------------- |
| `beforeCreate`    | Não é necessário\*         |
| `created`         | Não é necessário\*         |
| `beforeMount`     | `onBeforeMount`            |
| `mounted`         | `onMounted`                |
| `beforeUpdate`    | `onBeforeUpdate`           |
| `updated`         | `onUpdated`                |
| `beforeUnmount`   | `onBeforeUnmount`          |
| `unmounted`       | `onUnmounted`              |
| `errorCaptured`   | `onErrorCaptured`          |
| `renderTracked`   | `onRenderTracked`          |
| `renderTriggered` | `onRenderTriggered`        |
| `activated`       | `onActivated`              |
| `deactivated`     | `onDeactivated`            |

:::tip Nota
Visto que `setup` é executado em torno dos gatilhos de ciclo de vida `beforeCreate` e `created`, você não precisa defini-los explicitamente. Em outras palavras, qualquer código que seria escrito dentro desses gatilhos deve ser escrito diretamente na função `setup`.
:::

Essas funções aceitam um retorno de chamada que será executado quando o gatilho for chamado pelo componente:

```js
// MyBook.vue

export default {
  setup() {
    // mounted
    onMounted(() => {
      console.log('Componente montado!')
    })
  }
}
```
