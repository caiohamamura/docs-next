# Fundamentos da Reatividade

> Esta seção usa a sintaxe de [componente single-file](single-file-component.html) para exemplos de código

## Declarando Estado Reativo

Para criar um estado reativo a partir de um objeto JavaScript, podemos usar o método `reactive`:

```js
import { reactive } from 'vue'

// estado reativo
const state = reactive({
  count: 0
})
```

`reactive` é equivalente à API `Vue.observable()` do Vue 2.x, renomeado para evitar confusões com os `Observables` do RxJS. Aqui, o estado retornado é um objeto reativo. A conversão reativa é "profunda" - ela afeta todas as propriedades aninhadas do objeto passado.

O caso de uso essencial para o estado reativo no Vue é que podemos usá-lo durante a renderização. Graças ao rastreamento de dependência, a exibição é atualizada automaticamente quando o estado reativo muda.

Esta é a própria essência do sistema de reatividade do Vue. Quando você retorna um objeto de `data()` em um componente, ele é tornado reativo internamente pelo `reactive()`. O _template_ é compilado em uma [função de renderização](render-function.html) que faz uso dessas propriedades reativas.

Você pode aprender mais sobre `reactive` na seção [Básico da API de Reatividade](../api/basic-reactivity.html)

## Criação de Valores Reativos Avulsos como `refs`

Imagine o caso em que temos um valor primitivo avulso (por exemplo, uma string) e queremos torná-la reativa. Claro, poderíamos fazer um objeto com uma única propriedade igual à nossa string e passá-la para `reactive`. Vue tem um método que fará o mesmo para nós - ele é o `ref`:

```js
import { ref } from 'vue'

const count = ref(0)
```

`ref` retornará um objeto reativo e mutável que serve como uma **ref**erência reativa para o valor interno que está mantendo - é daí que vem o seu nome. Este objeto contém uma única propriedade chamada `value`:

```js
import { ref } from 'vue'

const count = ref(0)
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```

### Ref Desempacotada

Quando um `ref` é retornado como uma propriedade no contexto de renderização (o objeto retornado de [setup()](composition-api-setup.html)) e acessado no _template_, ele automaticamente se desempacota rasamente para o valor interno. Apenas o ref aninhado exigirá `.value` no _template_:

```vue-html
<template>
  <div>
    <span>{{ count }}</span>
    <button @click="count++">Incrementar contador</button>
    <button @click="nested.count.value ++">Incrementar contador aninhado</button>
  </div>
</template>

<script>
  import { ref } from 'vue'
  export default {
    setup() {
      const count = ref(0)
      return {
        count,

        nested: {
          count
        }
      }
    }
  }
</script>
```

:::tip Dica
Se você não quiser acessar a instância do objeto real, pode envolvê-lo em um `reactive`:

```js
nested: reactive({
  count
})
```
:::

### Acesso em Objetos Reativos

Quando um `ref` é acessado ou alterado como uma propriedade de um objeto reativo, ele se desempacota automaticamente para o valor interno para que se comporte como uma propriedade normal:

```js
const count = ref(0)
const state = reactive({
  count
})

console.log(state.count) // 0

state.count = 1
console.log(count.value) // 1
```

Se uma nova `ref` for atribuída à uma propriedade vinculada à uma `ref` existente, ela substituirá a antiga ref:

```js
const otherCount = ref(2)

state.count = otherCount
console.log(state.count) // 2
console.log(count.value) // 1
```

O desempacotamento de um `ref` só acontece quando aninhado dentro de um `Object` reativo. Não há desempacotamento executado quando o `ref` é acessado de um `Array` ou um tipo de coleção nativo como [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map):

```js
const books = reactive([ref('Guia do Vue 3')])
// precisa usar .value aqui
console.log(books[0].value)

const map = reactive(new Map([['count', ref(0)]]))
// precisa usar .value aqui
console.log(map.get('count').value)
```

## Desestruturar Estado Reativo

Quando queremos usar algumas propriedades do grande objeto reativo, pode ser tentador usar [desestruturação do ES6](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) para obter as propriedades que desejamos:

```js
import { reactive } from 'vue'

const book = reactive({
  author: 'Equipe Vue',
  year: '2020',
  title: 'Guia do Vue 3',
  description: 'Você está lendo esta documentação agora ;)',
  price: 'grátis'
})

let { author, title } = book
```

Infelizmente, com tal desestruturação, a reatividade para ambas as propriedades seria perdida. Para tal, precisamos converter nosso objeto reativo em um conjunto de refs. Esses refs manterão a conexão reativa com o objeto de origem:

```js
import { reactive, toRefs } from 'vue'

const book = reactive({
  author: 'Equipe Vue',
  year: '2020',
  title: 'Guia do Vue 3',
  description: 'Você está lendo esta documentação agora ;)',
  price: 'grátis'
})

let { author, title } = toRefs(book)

title.value = 'Guia detalhado do Vue 3' // precisamos usar .value porque `title` é uma `ref` agora
console.log(book.title) // 'Guia detalhado do Vue 3'
```

Você pode aprender mais sobre `refs` na seção [API de Refs](../api/refs-api.html#ref)

## Evite Mutar Objetos Reativos com `readonly`

Às vezes, queremos rastrear as alterações do objeto reativo (`ref` ou` reactive`), mas também queremos evitar alterá-lo de um determinado local do aplicativo. Por exemplo, quando temos um objeto reativo [provido](component-provide-inject.html), queremos evitar a sua mutação onde ele é injetado. Para fazer isso, podemos criar um _proxy_ somente leitura (readonly) para o objeto original:

```js
import { reactive, readonly } from 'vue'

const original = reactive({ count: 0 })

const copy = readonly(original)

// a mutação do original fará com que os observadores confiem na cópia
original.count++

// alterar a cópia irá falhar e resultar em um aviso
copy.count++ // warning: "Set operation on key 'count' failed: target is readonly."
```
