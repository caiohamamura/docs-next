# Interligações em Formulários

<VideoLesson href="https://vueschool.io/lessons/user-inputs-vue-devtools-in-vue-3?friend=vuejs" title="Aprenda a manipular os inputs de formulários na Vue School">Aprenda a trabalhar com inputs de formulário com uma aula gratuita da Vue School</VideoLesson>

## Uso Básico

Você pode usar a diretiva `v-model` para criar interligações de dados de mão dupla _(two-way data binding)_ em elementos _input_, _textarea_ e _select_ de formulários. Ela, automaticamente, escolhe a maneira correta de atualizar o elemento baseado no tipo do _input_. Embora um pouco mágica, `v-model` é, essencialmente, uma forma simplificada _(syntax sugar)_ para atualizar dados nos eventos de entrada do usuário, além de cuidado especial com casos extremos.

::: tip Nota
`v-model` irá ignorar o estado inicial dos atributos `value`, `checked` ou `selected` encontrado em qualquer elemento de formulário. Ela sempre irá tratar os dados da instância ativa como a fonte de informação _(source of truth)_. Você pode declarar o valor inicial no lado do JavasScript, dentro da opção `data` de seu componente.
:::

`v-model` utiliza diferentes propriedades internamente e emite diferentes eventos para diferentes elementos _input_:

- elementos _text_ e _textarea_ usam a propriedade `value` e o evento `input`;
- _checkboxes_ e _radiobuttons_ utilizam a propriedade `checked` e o evento `change`;
- campos de seleção utilizam `value` como propriedade e `change` como um evento.

<span id="vmodel-ime-tip"></span>
::: tip Nota
Você pode notar que `v-model` não é atualizada durante a composição através de um editor de método de entrada ([IME](https://en.wikipedia.org/wiki/Input_method)), como em Chinês, Japonês, Coreano, etc. Se você também quiser responder a essas atualizações, use diretamente um evento de `input` e `value` vinculado ao invés da `v-model`.
:::

### Input

```html
<input v-model="message" placeholder="Me edite" />
<p>A mensagem é: {{ message }}</p>
```

<common-codepen-snippet title="Lidando com Fomulários: v-model simples" slug="rNeqvjd" :preview="false" />

### Textarea

```html
<span>Mensagem com múltiplas linhas:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<br />
<textarea v-model="message" placeholder="Escreva bastante"></textarea>
```

<common-codepen-snippet title="Lidando com Formulários: textarea" slug="bGpmMqw" :preview="false" />

Interpolação em _textareas_ (`<textarea>{{text}}</textarea>`) não funcionará. Em vez disso, use `v-model`.

```html
<!-- ruim -->
<textarea>{{ text }}</textarea>

<!-- bom -->
<textarea v-model="text"></textarea>
```

### Checkbox

Caixa de seleção única, valor do tipo _boolean_:

```html
<input type="checkbox" id="checkbox" v-model="checked" />
<label for="checkbox">{{ checked }}</label>
```

<common-codepen-snippet title="Lidando com Formulários: checkbox" slug="KKzGRWq" :preview="false" />

Múltiplos _checkboxes_, associados ao mesmo _array_:

```html
<div id="v-model-multiple-checkboxes">
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
  <br />
  <span>Nomes selecionados: {{ checkedNames }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      checkedNames: []
    }
  }
}).mount('#v-model-multiple-checkboxes')
```

<common-codepen-snippet title="Lidando com Formulários: múltiplos checkboxes" slug="ExKdLWp" :preview="false" />

### Radio

```html
<div id="v-model-radiobutton">
  <input type="radio" id="one" value="Primeiro" v-model="picked" />
  <label for="one">Um</label>
  <br />
  <input type="radio" id="two" value="Segundo" v-model="picked" />
  <label for="two">Dois</label>
  <br />
  <span>Escolhido: {{ picked }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      picked: ''
    }
  }
}).mount('#v-model-radiobutton')
```

<common-codepen-snippet title="Lidando com Formulários: radiobutton" slug="dyMgeRE" :preview="false" />

### Select

Seleção de um único item:

```html
<div id="v-model-select" class="demo">
  <select v-model="selected">
    <option disabled value="">Escolha um</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selecionado: {{ selected }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      selected: ''
    }
  }
}).mount('#v-model-select')
```

<common-codepen-snippet title="Lidando com Formulários: select" slug="VwaExpO" :preview="false" />

:::tip Nota
Se o valor inicial da expressão `v-model` não corresponder a nenhuma das opções, o elemento `<select>` será renderizado em um estado "não selecionado". No iOS, isso impedirá o usuário de selecionar o primeiro item, já que, neste caso, não há disparo do evento `change`. Portanto, é recomendado fornecer uma opção desabilitada com um valor vazio, como demonstrado no exemplo acima.
:::

Seleção de múltiplos itens (vinculando a um _array_):

```html
<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br />
<span>Selecionado: {{ selected }}</span>
```

<common-codepen-snippet title="Lidando com Formulários: seleção de múltiplos itens (vinculando a um array)" slug="abNRGWR" tab="result" :preview="false" />

Renderização dinâmica de _options_ com `v-for`:

```html
<div id="v-model-select-dynamic" class="demo">
  <select v-model="selected">
    <option v-for="option in options" :value="option.value">
      {{ option.text }}
    </option>
  </select>
  <span>Selecionado: {{ selected }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      selected: 'A',
      options: [
        { text: 'Um', value: 'A' },
        { text: 'Dois', value: 'B' },
        { text: 'Três', value: 'C' }
      ]
    }
  }
}).mount('#v-model-select-dynamic')
```

<common-codepen-snippet title="Lidando com Formulários: select com opções dinâmicas" slug="BaKqxRK" :preview="false" />

## Interligação de Valores

Para _radio_, _checkbox_ e _select_, a interligação de valores do `v-model` são sempre _strings_ estáticas (ou valores do tipo _boolean_, em _checkboxes_):

```html
<!-- `picked` é uma string "a" quando assinalado -->
<input type="radio" v-model="picked" value="a" />

<!-- `toggle` é verdadeiro ou falso -->
<input type="checkbox" v-model="toggle" />

<!-- `selected` é uma string "abc" quando a primeira opção for selecionada -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

Porém, às vezes, podemos querer vincular o valor a uma propriedade dinâmica na atual instância ativa. Nós podemos utilizar `v-bind` para alcançar isso. Além disso, utilizando `v-bind` nos permite vincular o valor de um _input_ para valores que não são uma _string_ _(non-string values)_.

### Checkbox

```html
<input type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
```

```js
// quando assinalado:
vm.toggle === 'yes'
// quando não assinalado:
vm.toggle === 'no'
```

:::tip Dica
Os atributos `true-value` e `false-value` não afetam o atributo `value` dos _inputs_, porque os browsers não incluem caixas de seleção não assinaladas nas submissões de formulários. Para garantir que um dos dois valores seja enviado em um formulário (p. ex. "sim" ou "não"), use _inputs_ do tipo _radio_.
:::

### Radio

```html
<input type="radio" v-model="pick" v-bind:value="a" />
```

```js
// quando assinalado:
vm.pick === vm.a
```

### Select

```html
<select v-model="selected">
  <!-- Objeto literal atribuído para demonstração -->
  <option :value="{ number: 123 }">123</option>
</select>
```

```js
//  quando está assinalado:
typeof vm.selected // => 'object'
vm.selected.number // => 123
```

## Modificadores

### `.lazy`

Por padrão, `v-model` sincroniza o elemento _input_ com os dados após cada evento `input` (exceto para o caso de composição _IME_, [como descrito anteriormente](#vmodel-ime-tip)). Você pode adicionar o modificador `lazy` para sincronizar depois do evento `change`:

```html
<!-- sincronizado depois do "change" ao invés de "input" -->
<input v-model.lazy="msg" />
```

### `.number`

Se você deseja que a entrada do usuário seja automaticamente tipificada como um Number, pode adicionar o modificador `number` ao `v-model` do elemento:

```html
<input v-model.number="age" type="text" />
```

Isso geralmente é útil quando o tipo dp _input_ é `text`. Se o tipo do _input_ for `number`, o Vue pode converter automaticamente o valor bruto da string para número, e você não precisa adicionar o modificador `.number` ao `v-model`. Se o valor não puder ser convertido com `parseFloat()`, então o valor original é retornado.

### `.trim`

Se você quiser que os espaços em branco excedentes de um _input_ sejam automaticamente removidos, é possível adicionar o modificador `trim` ao `v-model` do elemento:

```html
<input v-model.trim="msg" />
```

## `v-model` com Componentes

> Se você ainda não está familiarizado com os componentes Vue, pode pular esta parte, por enquanto.

Os tipos de _input_ nativos do HTML nem sempre atendem as suas necessidades. Felizmente, os componentes Vue te permitem construir _inputs_ reutilizáveis com comportamento completamente customizável. Estes componentes também funcionam com `v-model`! Para saber mais, leia sobre [_inputs_ customizados](./component-basics.html#using-v-model-on-components) no guia de Componentes.
