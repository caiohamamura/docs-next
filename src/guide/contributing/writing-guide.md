# Guia de Escrita da Documentação do Vue

Escrever documentação é um exercício de empatia. Não estamos descrevendo uma realidade objetiva - o código-fonte já faz isso. Nosso trabalho é ajudar a moldar a relação entre usuários e o ecossistema Vue. Este guia em constante evolução fornece algumas regras e recomendações sobre como fazer isso de forma consistente dentro do ecossistema Vue.


## Princípios

- **Uma funcionalidade não existe até que esteja bem documentada.**
- **Respeite a "energia cognitiva" dos usuários.** Quando um usuário começa a ler, ele tem uma certa quantidade de energia cognitiva, quanto ela acaba o usuário pára de aprender.
  - A energia cognitiva **acaba mais rapidamente** com frases complexas, ter que aprender mais de um conceito ao mesmo tempo e exemplos abstratos que não se relacionam diretamente com o trabalho do usuário.
  - A energia cognitiva **acaba mais lentamente** quando os ajudamos a se sentirem consistentemente inteligentes, poderosos e curiosos. Dividir as conceitos em partes menores e cuidar do fluxo do documento pode ajudar a mantê-los nesse estado.
- **Sempre tente ver do ponto de vista do usuário.** Quando entendemos algo por completo ele se torna óbvio para nós. Isso é chamado de a maldição do conhecimento. Para escrever uma boa documentação, tente lembrar do que você precisava saber quando aprendeu esse conceito. Que jargões você precisou aprender? O que você entendeu mal? O que demorou muito para realmente entender? Uma boa documentação atende aos usuários no ponto do aprendizado em que eles se encontram naquele momento. Você pode praticar explicando o conceito para alguém pessoalmente antes de escrever.
- **Descreva o problema primeiro e depois a solução.** Antes de mostrar como um recurso funciona, é importante explicar por que ele existe. Caso contrário, os usuários não terão o contexto para saber se essa informação é importante para eles (isto é um problema que eles enfrentam?) ou a que conhecimento/experiência anterior conectá-lo.
- **Enquanto escreve, não tenha medo de fazer perguntas**, especialmente se você tem medo de que elas possam ser "estúpidas". Ser vulnerável é difícil, mas é a única maneira de entendermos mais completamente o que precisamos explicar.
- **Participe das discussões de funcionalidades.** As melhores APIs vêm do desenvolvimento orientado pela documentação, em que construímos funcionalidades que são fáceis de explicar, em vez de tentar descobrir como explicá-las depois. Fazer perguntas (especialmente "estúpidas") mais cedo frequentemente ajuda a elucidar confusões, inconsistências e comportamentos problemáticos antes que seja necessário introduzir uma mudança que quebraria a funcionalidade anterior.


## Organização

- **Instalação/Integração**: forneça uma visão geral de como integrar o software em tantos tipos diferentes de projetos quanto necessário.
- **Introdução/Primeiros Passos**:
  - Forneça, em menos de 10 minutos, uma visão geral do projeto, explicando os problemas que ele resolve e por que ele existe.
  - Forneça, em menos de 30 minutos, uma visão geral de como o projeto resolve os problemas, incluindo quando e por que usá-lo, e alguns exemplos simples de código. No final, inclua links para a página de instalação e para guias essenciais.
- **Guia**: faça os usuários se sentirem inteligentes, poderosos e curiosos e que mantenham esse estado para que tenham a motivação e a energia cognitiva para continuar aprendendo mais. As páginas devem ser lidas sequencialmente, portanto, devem ser ordenadas pelo grau de dificuldade/esforço.
  - **Essenciais**: não deve demorar mais de 5 horas para ler os itens essenciais, embora menos tempo seja ainda melhor. Seu objetivo é fornecer os 20% do conhecimento que ajudarão os usuários a lidar com 80% dos casos de uso. Os itens essenciais podem vincular-se a guias mais avançados e à API, na maioria dos casos, você deve evitar fazer hiperlinks. Se necessários, você também precisa fornecer um contexto para que os usuários estejam cientes se devem clicar neste link durante sua primeira leitura. Caso contrário, muitos usuários acabam esgotando sua energia cognitiva, tentando aprender completamente todos os aspectos de um recurso antes de seguir em frente e, como resultado, nunca terminam a primeira leitura essencial. Lembre-se de que uma leitura suave é mais importante do que ser minuciosa. Queremos dar às pessoas as informações necessárias para evitar uma experiência frustrante, mas elas sempre podem voltar e ler mais ou pesquisar um problema menos comum quando o encontrar.
  - **Avançado**: enquanto o essencial ajuda as pessoas a lidar com ~80% dos casos de uso, os guias subsequentes ajudam a levar os usuários a 95% dos casos de uso, além de informações mais detalhadas sobre recursos não essenciais (ex. transições, animações), mais complexos, recursos de conveniência (ex. mixins, diretivas personalizadas) e melhorias de experiência do dev (ex. JSX, plugins). Os 5% finais dos casos de uso são de nicho específico, complexo e/ou propensos a abusos e deixados para o livro de receitas e a referência da API, que podem ser apresentados como links dentro do guia.
- **Referência/API**: forneça uma lista completa de recursos, incluindo informações de tipo, descrições do problema que cada um resolve, exemplos para cada combinação de opções e links para guias, livros e outros recursos internos que fornecem mais detalhes. Ao contrário das outras páginas, esta não é criada para ser lida de cima para baixo, então muitos detalhes podem ser fornecidos. Essas referências também devem ser mais facilmente ignoradas do que nos guias, portanto o formato deve estar mais próximo de um dicionário do que o formato de contar histórias dos guias.
- **Migrações**:
  - **Versões**: quando alterações importantes são feitas é importante incluir uma lista completa de alterações, incluindo uma explicação detalhada de por que a mudança foi feita e como migrar seus projetos.
  - **De outros projetos**: como esse software se compara a outro software semelhante? Isso é importante para ajudar os usuários a entender quais problemas adicionais podemos resolver ou criar para eles e até que ponto eles podem transferir o conhecimento que já têm.
- **Guia do estilo**: existem necessariamente algumas peças-chave no desenvolvimento que precisam de uma tomada de decisão, mas não são essenciais para a API. O guia de estilo fornece recomendações educadas e opinativas para ajudar a orientar essas decisões. Elas não precisam ser seguidas cegamente, mas podem ajudar as equipes a economizar tempo padronizando os detalhes menores.
- **Livro de receitas**: as receitas no livro de receitas são escritas com alguma suposição de familiaridade com o Vue e seu ecossistema. Cada uma é um documento altamente estruturado que descreve alguns detalhes de implementações comuns que um dev Vue pode encontrar.


## Gramática e Escrita

### Estilo

- **Os títulos devem descrever problemas**, não soluções. Por exemplo, "usando props" seria um título menos adequado, pois descreve uma solução. Um título melhor poderia ser "passando dados para componentes filhos com props", porque fornece o contexto do problema. Os usuários realmente não começarão a prestar atenção à explicação de um recurso até que tenham uma ideia do porque/quando o usariam.
- **Quando assumir conhecimento prévio, declare** no início e crie links para os recursos de conhecimento mais avançando.
- **Apresente apenas um novo conceito de cada vez, sempre que possível** (incluindo exemplos de texto e código). Mesmo que muitos sejam capazes de entender mais de um conceito simulteneamente, também há outros que se perderão - e mesmo aqueles compreendem esgotarão mais rapidamente sua energia cognitiva.
- **Evite blocos especiais de conteúdo para dicas e advertências quando possível.** Geralmente é preferível misturá-las mais naturalmente ao conteúdo principal utilizando exemplos para demonstrar casos extremos.
- **Não inclua mais de duas dicas e advertências entrelaçadas por página.** Se você achar que mais de duas dicas são necessárias em uma página, considere adicionar uma seção de advertências para resolver esses problemas. O guia deve ser lido linearmente, e dicas e advertências podem ser distratores para alguém que tenta entender os conceitos básicos.
- **Evite apelos à autoridade** (ex. "você deve fazer x, porque essa é uma prática recomendada" ou "X é melhor porque oferece a você uma separação completa de responsabilidades"). Em vez disso, demonstre com exemplos os problemas específicos causados e/ou resolvidos por um padrão.
- **Ao decidir o que ensinar primeiro, pense em qual conhecimento fornecerá a melhor relação de poder/esforço.** Isso ajuda os aprendizes a se sentirem inteligentes, poderosos e curiosos, e sua energia cognitiva dura mais tempo.
- **A menos que o contexto assuma um *string template* ou *build system*, apenas escreva código que funcione em qualquer ambiente pelo software (por exemplo, Vue, Vuex, etc).**
- **Mostre, não diga**. Por exemplo, "para usar Vue em uma página, você pode adicionar ao seu HTML:" (mostre o tag script), em vez de "para usar Vue em uma página, adicione um elemento de script com um atributo src, cujo valor deve ser um link para a fonte compilada da Vue".
- **Nunca assuma um contexto mais avançado do que precisar.**
- **Na maioria dos casos, prefira links entre as seções dos documentos a repetir o mesmo conteúdo em várias seções.** Alguma repetição no conteúdo é inevitável e até essencial para o aprendizado. No entanto, muita repetição também torna os documentos mais difíceis de manter, porque uma mudança na API exigirá mudanças em muitos lugares e é fácil se perder. Este é um equilíbrio difícil de acertar.
- **O específico é melhor que o genérico.** Por exemplo, um componente de exemplo `<BlogPost>` é melhor do que `<ComponenteA>`.
- **Claro é melhor que obscuro.** Por exemplo, um componente de exemplo `<BlogPost>` é melhor do que `<ConfiguraMoedaCambio>`.
- **Seja emocionalmente relevante.** Explicações e exemplos que envolvam experiências que as pessoas vivenciam e se importam serão sempre mais efetivas.
- **Sempre prefira uma linguagem mais simples e clara do que uma complexa e cheia de jargões.** Por exemplo:
  - "Você pode usar o Vue com um elemento de script" em vez de "para iniciar o uso do Vue, uma opção possível é realmente injetá-lo por meio de um elemento script no HTML"
  - "função que retorna uma função" em vez de "função de ordem superior"
- **Evite linguagem que invalide dificuldade**, como "fácil", "apenas", "obviamente" etc. Para referência, consulte [palavras a serem evitadas na escrita educacional] (https://css-tricks.com/Palavras-escrita-educacional/).


### Gramática

- **Evite abreviações** em exemplos de escrita e código (ex. `atributo` é melhor que `attr`, `mensagem` é melhor que `msg`), a menos que você esteja referenciando especificamente uma abreviatura em um API (por exemplo, `$attrs`). Os símbolos de abreviação incluídos nos teclados padrão (por exemplo, `@`, `#`, `&`) são aceitáveis.
- **Ao fazer referência a um exemplo diretamente a seguir, use dois pontos (`:`) para encerrar a frase**, em vez de um ponto final (`.`).
- **Use a vírgula de Oxford** (ex. "A, B, e C" em vez de "A, B e C"). 
![Por que a vírgula Oxford é importante](/images/oxford-comma.jpg)
  - Fonte: [The Serial (Oxford) Comma: When and Why To Use It](https://www.inkonhand.com/2015/10/the-serial-oxford-comma-when-and-why-to-use-it/)
- **Ao fazer referência ao nome de um projeto, use a mesma grafia usada pelo projeto.** Por exemplo, "webpack" e "npm" devem ser grafados em caixa baixa, assim como constam em sua documentação.
- **Para títulos use *title case*** - pelo menos por enquanto, pois é o que usamos no restante dos documentos. Há pesquisas sugerindo que apenas a primeira palavra do título em caixa alta é superior em relação à legibilidade e também reduz a sobrecarga cognitiva para os escritores da documentação, pois eles não precisam tentar se lembrar se devem capitalizar palavras como "e", "com" e "sobre".
- **Não use emojis (exceto nas discussões).** Os emojis são fofos e amigáveis, mas podem ser uma distração na documentação e alguns emoji até transmitem significados diferentes em diferentes culturas.

## Iteração & Comunicação

- **A excelência vem da iteração.** Os primeiros rascunhos são sempre ruins, mas escrevê-los é uma parte vital do processo. É extremamente difícil evitar a lenta progressão do ruim -> ok -> bom -> ótimo -> inspirador -> transcendente.
- **Espere apenas até que algo seja "bom" antes de publicar.** A comunidade ajudará você a empurrá-lo para o final da cadeia.
- **Tente não ficar na defensiva ao receber feedback.** Nossa escrita pode ser muito pessoal para nós, mas se ficarmos chateados com as pessoas que nos ajudarem a melhorar, elas pararão de dar feedback ou começarão a limitar o tipo de feedback que eles dão.
- **Revise o seu próprio trabalho antes de mostrá-lo a outras pessoas.** Se você mostrar a alguém trabalhos com muitos erros ortográficos/gramaticais, receberá feedback sobre error de ortografia/gramática em vez de notas mais valiosas sobre se a escrita está alcançando seus objetivos.
- **Quando você pedir feedback às pessoas, diga aos revisores:**
  - **o que está tentando fazer**
  - **os seus medos**
  - **o que está tentando atingir**
- **Quando alguém relata um problema, quase sempre há um problema**, mesmo que a solução que eles propuseram não esteja certa. Continue fazendo perguntas para saber mais.
- As pessoas precisam se sentir seguras ao fazer perguntas e contribuir/revisar o conteúdo. Veja como você pode fazer isso:
  - **Agradeça às pessoas por suas contribuições/revisões, mesmo se você estiver se sentindo mal-humorado.** Por exemplo:
    - "Ótima pergunta!"
    - "Obrigado pela explicação. 🙂"
    - "Isso foi realmente intencional, mas obrigado por contribuir. 😊"
  - **Ouça o que as pessoas estão dizendo e se coloque no lugar delas se você não tem certeza as compreende.** Isso pode ajudar a validar os sentimentos e as experiências das pessoas, além de ajudar a verificar se você está compreendendo corretamente.
  - **Use muitos emojis positivos e empáticos.** É sempre melhor parecer um pouco estranho do que mau ou impaciente.
  - **Explique as regras/limites de conduta de maneira gentil** Se alguém se comportar de uma maneira abusiva/inadequada, responda apenas com bondade e maturidade, mas também deixe claro que esse comportamento não é aceitável e o que acontecerá (de acordo com o Código de Conduta) se continuar se comportando mal.

### Dicas, Chamadas, Alertas e Destaques de Linha

Temos alguns estilos dedicados para denotar algo que vale a pena destacar de uma maneira específica. Eles estão reunidos [nesta página](https://vuejsbr-docs-next.netlify.app/guide/contributing/doc-style-guide.html#alerts). **Use com moderação.**

Há uma certa tentação de abusar desses estilos, pois é possível simplesmente adicionar uma mudança dentro de uma chamada. No entanto, isso interrompe o fluxo de leitura para o usuário e, portanto, deve ser usado apenas em circunstâncias especiais. Sempre que possível, devemos tentar criar uma narrativa e fluir dentro da página para respeitar a carga cognitiva aos leitores.

Sob nenhuma circunstância 2 alertas devem ser usados um ao lado do outro, é um sinal de que não podemos explicar o contexto bem o suficiente.

### Contribuindo

Agradecemos PRs pequenos e focados. Se você quiser fazer uma mudança extremamente grande, comunique-se com os membros da equipe antes de uma solicitação. Aqui está um [texto que detalha por que isso é tão crítico](https://www.netlify.com/blog/2020/03/31/how-to-scope-wow-prs/) para trabalharmos bem em equipe. Por favor, entenda que, embora sempre apreciemos contribuições, em última análise, precisamos priorizar o que funciona melhor para o projeto como um todo.

## Recursos

### Software

- [Grammarly](https://www.grammarly.com/): Desktop app and browser extension for checking spelling and grammar (though grammar checking doesn't catch everything and occasionally shows a false positive).
- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker): An extension for VS Code to help you check spelling within markdown and code examples.

### Livros

- [On Writing Well](https://www.amazon.com/Writing-Well-30th-Anniversary-Nonfiction-ebook/dp/B0090RVGW0) (see [popular quotes](https://www.goodreads.com/work/quotes/1139032-on-writing-well-the-classic-guide-to-writing-nonfiction))
- [Bird by Bird](https://www.amazon.com/Bird-Some-Instructions-Writing-Life/dp/0385480016) (see [popular quotes](https://www.goodreads.com/work/quotes/841198-bird-by-bird-some-instructions-on-writing-and-life))
- [Cognitive Load Theory](https://www.amazon.com/Cognitive-Explorations-Instructional-Performance-Technologies/dp/144198125X/)
