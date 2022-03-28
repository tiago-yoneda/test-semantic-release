# lib-request

### Mudanças
A partir de agora a lib-request vai ser distribuida como um pacote, igual ao que fazemos com a lib-app-components. Para fazer essa transição vai ser necessário:
- desinstalar a lib-request com o `yarn remove lib-request`
- utilizar `yarn add @meliuz/lib-request`

Um ponto de atenção é que vamos precisar alterar a versão do pacote no `package.json` manualmente caso seja feito um novo release. Ou remover/adicionar novamente via yarn.

O release tem o formato v.{major}.{minor}.{patch} 

## Grandes mudanças no repositório
Implementamos o uso do [semantic-release](https://github.com/semantic-release/semantic-release), com isso podemos versionar e publicar o pacote automaticamente, mas para isso precisamos seguir regras de commit para que o fluxo automático seja corretamente implementado.

- O commit deve ter ser composto por até 3 blocos e eles devem ser separados por uma linha: `header`, `body` e `footer(opcional)`.
Para ficar mais claro o responsável pelo commit, por favor utilize o `comando git commit -s`, pois ele gera automaticamente uma signature como footer.

### Header - Máximo de 50 caractéres
```
<tipo>(<escopo>): <breve descrição>
  │       │             │
  │       │             └─⫸ Escrever no modo imperativo sem ponto final
  │       │
  │       └─⫸ É opcional mas se for utilizar, matenha o kebab-case
  │
  └─⫸ Mais sobre os tipos abaixo
```
#### Sobre o `tipo`
O que vai fazer com que a versão seja corretamente criada vai ser o tipo do commit que vai ser feito.

Atualmente estão implementados quatro tipos de commit
- *fix* ou *chore*: Implementam um incremento do tipo patch 
- *feat*: Implementa o tipo minor
- *perf*: Implementa o tipo major

Atenção para o tipo `perf` que necessita de um cuidado especial:
- Esse tipo de commit necessita de um footer com o seguinte texto `BREAKING CHANGE: <mensagem>`. Caso não tenha a versão vai ser incrementada como um patch em vez de um major.


exemplo:
```
perf: Implementa grande mudança no componente x

texto explicando o que foi feito

Signed-off-by: Tiago Yoneda <tiago.yoneda@meliuz.com.br>
BREAKING CHANGE: Explica o que porque é uma mudança grande
```

### Body - Máximo de 72 caractéres por linha

### Footer
- Assinatura do responsável pelo commit
- `BREAKING CHANGE:` caso seja um tipo `perf`

## Sobre o release automático
Uma nova versão desse pacote vai ser criado toda vez que um PR for mergeado na main.
E a versão vai ser modificada e incrementada de acordo com os commits que forem realizados nesse PR. Sendo que o maior incremento sobrepõe os menores.
ex: 
Dada a versão v2.1.7, se tivermos 4 fix e 1 feat o resultado vai ser a versão v2.2.0

