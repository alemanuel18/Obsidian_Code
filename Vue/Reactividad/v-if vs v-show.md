A **renderização condicional no Vue** permite mostrar ou ocultar elementos da interface segundo uma condição lógica, algo essencial para construir aplicações web dinâmicas. Si trabalhas com Vue e precisas controlar quando um bloco aparece, esta é a base que vais usar todos os dias.

## Como funciona a renderização condicional no Vue?

Quando construis uma interface, nem tudo deve aparecer ao mesmo tempo. O Vue resolve isto com diretivas que avaliam uma expressão e decidem se o elemento se mostra ou não.

No exemplo prático de um jogo de adivinhar números, queremos dar pistas ao jogador: dizer-lhe se o número que procura é maior, menor ou se já ganhou. Para isso, encostamos as diretivas diretamente nas tags do componente _GameCounter_.

> **¿Qué é a renderização condicional no Vue?** É a capacidade de mostrar ou ocultar elementos do DOM consoante uma condição lógica, usando diretivas como `v-if`, `v-show` e `v-else-if`.

## Qual é a diferença entre v-if e v-show no Vue?

Aqui está o ponto que confunde quem começa. Ambas as diretivas servem para condicionar a visibilidade, mas funcionam de forma muito diferente por baixo.

A diretiva `v-show` mantém sempre o elemento no DOM. Quando a condição é `false`, o Vue limita-se a aplicar `display: none` via CSS, ou seja, o elemento continua compilado e ativo, apenas não se vê.

A diretiva `v-if`, em contrapartida, decide se o elemento existe ou não. Se a condição for `false`, o Vue nem sequer renderiza essa tag no DOM. Se inspecionares o código, vais ver que o elemento simplesmente não está lá.

- Usa `v-show` quando o elemento alterna a sua visibilidade frequentemente ou quando a acessibilidade importa.
- Usa `v-if` quando o componente é complexo e a lógica de negócio exige que seja totalmente removido.
- Combina `v-if` com `v-else` para mostrar um conteúdo por defeito quando a condição não se cumpre.

Cada caso pede uma escolha consciente, e isso vai definir tanto o desempenho como a manutenção do teu código.

## Como usar v-else-if para criar lógica tipo switch?

Voltando ao jogo, queremos três mensagens possíveis: _Procurar número maior_, _Procurar número menor_ e _Ganhaste_. Aqui entra o `v-else-if`, uma diretiva que funciona como um switch encadeado.

A lógica fica assim: se o contador for menor que `numberToGuess`, mostra-se _Procurar número maior_. Se essa condição falhar e o contador for maior que `numberToGuess`, então `v-else-if` toma conta e mostra _Procurar número menor_. Para a mensagem final de vitória, usa-se um `v-show` que aparece exatamente quando o jogador acerta.

```html
<p v-if="counter < numberToGuess">Procurar número maior</p> 
<p v-else-if="counter > numberToGuess">Procurar número menor</p> 
<p v-show="counter === numberToGuess">Ganhaste</p>
```

> **Quando devo usar v-else-if?** Quando tens várias condições mutuamente exclusivas e queres avaliar uma a seguir à outra, evitando escrever vários `v-if` separados.

## Por que escolher v-show em vez de v-if por acessibilidade?

Leitores de ecrã e tecnologias assistivas dependem do DOM real para funcionar. Se ocultas conteúdo com `v-if`, esse conteúdo desaparece por completo, o que pode quebrar a navegação para utilizadores com necessidades especiais.

Com `v-show`, o elemento permanece no DOM com `display: none`, o que mantém referências e estados intactos. Por isso, sempre que a decisão for apenas estética ou de alternância simples, `v-show` costuma ser a escolha mais segura.

## ¿Quando faz sentido usar v-if mesmo assim?

Imagina um componente pesado, com chamadas a APIs, formulários complexos ou lógica de negócio que não deve correr até que o utilizador a ative. Aí, `v-if` brilha: o Vue não compila nem renderiza nada até a condição ser verdadeira, poupando recursos.

A decisão entre uma e outra resume-se a isto: queres ocultar visualmente ou queres remover por completo? Essa pergunta guia toda a tua escolha.

## ¿Que conceitos chave aparecem nesta aula?

Ao longo da explicação, há ideias técnicas que vale a pena fixar para dominares a renderização condicional no Vue.

- _Diretiva_ `v-if`: avalia uma condição e renderiza o elemento no DOM apenas se for verdadeira .
- _Diretiva_ `v-show`: alterna a visibilidade aplicando `display: none`, mantendo o elemento no DOM .
- _Diretiva_ `v-else-if`: encadeia condições adicionais quando a anterior falha, semelhante a um switch .
- _Diretiva_ `v-else`: define o conteúdo por defeito quando nenhuma condição anterior se cumpre .
- _DOM_: estrutura onde o Vue decide compilar ou não o elemento, dependendo da diretiva escolhida .
- _Componente_ `GameCounter`: exemplo prático onde se aplica a lógica de adivinhar um número .

Agora tens o desafio na mão: pega num projeto teu e experimenta combinar `v-if`, `v-else-if`, `v-else` e `v-show` em casos reais. Conta nos comentários que cenário escolheste e qual diretiva resolveu melhor o teu problema.