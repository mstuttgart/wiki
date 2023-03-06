# Fundamentos

Javascript é uma linguagem de auto nível que segue o padrão ECMAScript. Ela é fracamente tipada e possui tipagem dinâmica, Orientação Objetos baseada em Protótipos e funções como cidadão de primeira classe. Suporta os paradigmas de programação imperativo, funcional e orientada a eventos.

## Características

### Fracamente Tipada

Uma linguagem **fracamente tipada** aceita que valores de tipos diferentes sejam atribuídos a uma mesma variável.

```javascript
var a = 'exemplo'

a = 10 // não causa erro
```

Em linguagens **fortemente tipadas** (como C, C++ e Java), ocorreria um erro no codigo acima. Pois um variável que foi declarada com *string*, seria permitido receber apenas valores do tipo *string*.

### Tipagem Dinâmica

Uma linguagem pode possuir tipagem *Estática* ou *Dinâmica*.

Na **Tipagem Estática**, quando o tipo da valores que a variável irá receber é determinado na declaração da variável (como ocorre no C, C++ e Java).

Na **Tipagem Dinâmica**, o tipo de valor da variável é determinado somente no momento que um valor é atribuído a ela.

Podemos usar o comando *typeof* para determinar o tipo do valor contido na variável.

> typeof value

Exemplo:

```javascript
var a = 'exemplo'
typeof a    // string

a = 10
typeof a    // number
```

## Number [^number]

Em Javascript, o tipo **Number** é uma função e representa tanto números inteiros (Integer) como números de ponto flutuante (Float). Ele apresenta várias operações muito úteis, como no exemplo a seguir.

Exemplo:

```javascript
// Exemplo de Numbers
typeof -5    // number
typeof 10    // number
typeof 2.5   // number

// Determinar se um numero é ou não inteiro
Number.isInteger(2.6)   // true
Number.isInteger(15)    // false

// Delimitar o numero de casas decimais
(3.1415).toFixed(2)    // '3.14' 

// Converter valor numerico para string
(3.1415).toString()    // '3.1415'

// Converter valor numerico para string, mas para base binária (2)
(7).toString(2)    // '111'
```

### Números especiais

Javascript possui alguns valores de números especiais que normalmente não encontramos em outra linguagem: `NaN` e `Infinity`.

#### NaN

O valor `Nan` (do inglês, *Not a Number*) é produzido quando o resultado de uma operação retorna um valor que não é um *Number*.

Exemplo:

```javascript
var Number('hello')   // NaN -> o número não pode ser parseado
var Number('12a')     

var Math.sqrt(-4)  // NaN -> operação falhou raiz de numero negativo)

var NaN + 4   // NaN
```

**Importante**:

> `NaN` é o único valor que não ígual a  si mesmo. 

```javascript
NaN === NaN   // false

typeof NaN  // Number
```

Essa peculiaridade vem da regra [IEEE](https://en.wikipedia.org/wiki/IEEE_754) utilizada para operações com ponto flutuante. Isso ocorre devido a natureza dos valores que o `NaN` pode representar.

```javascript
var raizA = Math.sqrt(-4)   // NaN
var raizB = Math.sqrt(-25)  // NaN

raizA === raizB  // false
```

Para realizar a verificação se um determinado valor é `NaN`, ddevemos utilizar a função `isNaN`:

```javascript
isNaN('12a')  // true
isNan(4)      // false
```

#### Infinity

É considerado o maior "número" da linguagem, assim como `-Infinty` é considerado o menor, com exceção do `NaN`. De modo a verificar se um *Number* assume um dos valores `Infinity`, utilizamos a função `isFinite`.

```javascript
isFinite(1000)      // true
isFinite(Infinity)  // false
isFinite(NaN)       // false
```

### Operações aritméticas

O Javascript apresenta alguma excentricidades em relação ao *Number* que devem ser observadas.

#### Divisão por zero

Diferente de outras linguagens, o Javascript não irá acusar erro ou disparar uma exceção quando ocorrer uma divisão por zero. Ao invés disso, a linguagem possui o tipo **Infinity**, um tipo especial para representar valores infinitos.

```javascript
a = 5/8   // Infinity
```

#### Operações com tipos diferentes

Por ser fracamente tipada, o Javascript permite alguns tipos de operações envolvendo valores de tipos diferentes.

```javascript
a = '10' / 2    // 5
b = '10' * 2    // 10

c = '10,2' * 2    // Nan (indefinido, por causa da virgula, o JS nao sabe que é um número)
```

#### Chamando funções diretamente

Quando desejado podemos chamar as funções diretamente pelo Number, sem precisar guardar o valor em uma variável primeiro.

```javascript
10.toString()    // Uncaught SyntaxError: Invalid or unexpected token

(10).toString()    // '10'
```

#### Operações com números de ponto flutuante

Em operações com números de ponto flutuante, o Javascript sempre irá retornar o número máximo de casas decimais, seguindo o padrão IEEE [^IEEE].

```javascript
var soma = 0.1 + 0.7    //0.7999999999999999
```

### Math [^math]

O objeto **Math** nos permite executar tarefas matemáticas, como raiz quadrada, elevar um número a determinada potência, seno e cosseno de um determinado angulo e determinar o máximo e mínimo de um determinado conjunto de valores, entre outras funções. 

**Math** não é um construtor, então todos os metodos do objeto podem ser chamados sem criá-lo (semelhante a funções estática de outras linguagens).

```javascript
Math.PI    // valor PI

Math.sqrt(4)    // raiz quadrada de 4.

Math.pow(2, 3)    // 2^3

Math.max(2, 1, 5, 4)    // 5 -> maior valor de um conjunto de valores

Math.floor(3.1415)    // 3 -> arredondamento para o inteiro anterior
Math.ceil(3.1415)     // 4 -> arredondamento para o inteiro superior
```

## String [^string]

Em Javascript, uma *string* pode ser representada tanto por aspas duplas quanto por aspas simples. A *string*  é tratada como uma lista, isso nos permite realizar buscas e cortes na mesma, conforme a necessidade.

Exemplos:

```javascript
text = 'Javascript'

// Retorna o caracter de uma determinada posicao
text.charAt(0)    // 'J'
text.charAt(20)    // '' . string vazia quando o indice nao existir na string

// Retorna o indice de um determinado caracter
text.indexOf('c')    // 5 
text.indexOf('a')    // 1 retorna a primeira ocorrencia do caracter 'a'

// Retorna substring a partir de um intervalor de indices
text.substring(1)    // 'avascript' . Do indice 1 até o final da string
text.substring(0, 3)    // 'Java'. Do indice 0 ao 3

// Separa uma string a partir de um caracter delimitador
'Javascript, Python, Go'.split(',')    // ['Javascript', 'Python', 'Go']

// Busca dentro da string (pode ser utilizado Regex)
'Javascript, Python, Go'.search('Python')    // 12. Indice da primeira ocorrencia que coincide coma busca
```

### Interpolação e Concatenação de strings

O Javascript, assim como outras linguagens, também apresenta recursos para *interpolação* e *concatenação* de strings. **Interpolação de Strings** seria utilizar uma string como *template*,  onde essa string possui variaveis nas partes de texto que valores reais durante o processo de interpolação.

Exemplo  *concatenação*:

```javascript
text = 'Javascript'
 
// Concatenacao utilizando a funcao 'cocat'
text.cocat(' é ', ' nota', ' 10!')    // 'Javascript é nota 10!'

// Concatenacao usando operador +
text = text + ' é ' + ' nota ' + ' 10!'
```

Exemplo *interpolação*:

```javascript
var nota = 10

// Transformamos a string em uma template string, onde a chave #{nota} recebe
// o valor da variavel 'nota'
text = `Javascript é nota ${nota}!`    // 'Javascript é nota 10!'
```

O Javascript tentará executar tudo o que esta dentro da chave `${}`. Desde a execução de funções até operações aritméticas.

```javascript
text = `2 + 3 = ${2 + 3}`    // '2 + 3 = 5'
```

## Boolean [^boolean]

Em Javascript, os valores booleanos são representados por *true* e *false*. Como ocorre em algumas linguagens, alguns valores também podem representar *true* ou *false* quando utilizados em determinados contextos. 

Os valores a seguir são considerados *true*:

- `true`,
- `1`: ou qualquer inteiro diferente de zero,
- `' '`: string com pelo menos um caracter (mesmo que seja espaço) ,
- `Infinity`: palavra reservada,
- `[]`: array vazio,
- `{}`: objeto literal.

Os valores a seguir são considerados *false*:

- `false`,
- `0`: valor inteiro,
- `null`: palavra reservada,
- `undefined`: palavra reservada,
- `NaN`: palavra reservada (*Not a Number*).

## Declaração de variáveis

**let** e **const** são substitutos para **var**, introduzidos no [ECMAScript6](https://www.w3schools.com/js/js_es6.asp) e proveem escopo de block para o Javascript. Antes do ES6 (2015), o JavaScript possuia apernas *escopo global* e *escopo de função*.

### var[^var]

As variáveis definidas com *var* possuem as seguintes propriedades:

- Devem ser declaradas antes do uso
- Podem ser redeclaradas
- Possuem escopo global ou de função

ECMAScript6 (ES6 / JavaScript 2015) encoraja a declaração de varáveis com **let**, de modo a evitar alguns possíveis problemas. O primeiro diz respeito ao escopo.

Exemplo:

```javascript
var n = 5

{
    var n = 10
}

console.log(n)    // 10

```

No exemplo acima, vericamos que o valor impresso nas duas situações foi `10`. Isso ocorre porque *var* permite a redeclaração de variáveis e redeclar uma variável dentro de um block iŕa redeclará-la fora do bloco. Sendo assim, o Javascript intepretou que as duas variáveis `n` eram na verdade, a mesma variável. Por isso o valor impresso foi o valor da última atribuição.

Outro inconveniente de `var` é o fato dele permitir o acesso externo de variáveis declaras dentro do bloco `{}`.

Exemplo:

```javascript

{
    var nome = 'Maria' 
}

console.log(nome)    // 'Maria'

```

Essa liberdade de acesso independente do escopo pode atrapalhar a legibilidade de código e causar erros de inconsistência no estado das variáveis (valor armazenado pela mesma), algo muito importante em linguagens de paradigma funcional.

### let [^let]

As variáveis definidas com *let* possuem as seguintes propriedades:

- Devem ser declaradas antes do uso
- Não podem ser redeclaradas
- Possuem escopo de bloco `{}`

O uso de *let* resolve os incoveniêntes apresentado pelo uso do *var*. 

Exemplo:

```javascript
let n = 5

{
    let n = 10
}

console.log(n)    // 5 (o valor foi mantido)
```

O *let* não permite a redeclaração de variáveis em um mesmo escopo de bloco `{}`. Sendo assim, o Javascript entende que, salvo terem o mesmo nome, as varáveis `n` são variáveis diferentes.

```javascript
{
    let nome = 'Maria'
    let nome = 'Pedro' // SyntaxError: Identifier 'nome' has already been declared
}
```

O *let* também não permite o acesso fora do escopo de bloco onde ele foi declarado.

Exemplo:

```javascript

{
    let nome = 'Maria' 
}

console.log(nome)    // ReferenceError: nome is not defined

```

A tentativa de acesso resultará em um `ReferenceError` indicando que a variável `nome` não foi definida.

### const [^const]

As variáveis definidas com *const* possuem as seguintes propriedades:

- Devem ser declaradas e inicializas com um valor antes do uso
- Não podem ser redeclaradas
- Não podem sofrer reatribuição
- Possuem escopo de bloco `{}`

Exemplo:

```javascript
const PI = 3.1414   // Declaramos a constante PI e a inicializamos
PI = 3.14           // TypeError: Assignment to constant variable.

const PI = 3.14     // SyntaxError: Identifier 'PI' has already been declared
```

Sempre declaramos uma variável com *const* quando sabemos que a *referência* ao qual ela aponta não deve mudar. Recomenda-se o uso de *const* quando declaramos:

- Um novo *array*
- Um novo *object*
- Uma nova *Function*

O *const* não define um uma valor constante. Ela define um referência constante a uma valor. Sendo assim, não podemos reatribuir outro *object* a uma constante, mas podemos alterar os valores do mesmo.

Exemplo:

```javascript
const pessoa = {nome: 'Maria'}

pessoa.nome = 'Joao'       // conseguimos alterar o atributo do object

pessoa = {nome: 'Pedro'}  // TypeError: Assignment to constant variable.

```

### Hoisting [^hoisting]

**Hoisting** é um comportamento padrão do Javascript de mover todas as declaração para o topo do escopo atual (para o topo do *script* ou da função). Isso permite que variáveis possam ser utilizadas antes de serem declaradas.

```javascript
n = 10

.
. // codigo qualquer
.

var n
```

É a mesma coisa que:

```javascript
n = 10
var n

.
.  // codigo qualquer
.
```

O Javascript somente executa o *hoisting* para declarações, não inicializações:

```javascript
var a = 10
var b = 2

console.log(a + b)  // 12
```

É diferente de:

```javascript
var a = 10

console.log(a + b)  // b is undefined

var b = 2
```

O Javascript irá indicar que `b` esta `undefined`. Isso ocorre porque somente a declaração `var b`, e não atribuição `= 2`, sofreu *hoisting* para o topo do *script*. Em outras palavras, ocorre o comportamento semelhante ao seguinte código:

```javascript
var a = 10    // inicializa 'a'
var b         // declara 'b'

console.log(a + b)  // 'b' is undefined

b = 2   // somente aqui atriuimos um valor a 'b'
```

#### Comportamento para o *let* e *const*

Variáveis declaradas com *let* e *const* sofrem *hoisting* para o topo do bloco, mas não são inicializadas. Isso significa que o bloco sabe da existência das variáveis, mas não pode usá-las até que as mesmas sejam declaradas.

Exemplo:

```javascript
{
    nome = 'Maria'
    let nome   // ReferenceError: Cannot access 'nome' before
}

{
    PI = 3.14
    const PI  // SyntaxError: Missing initializer in const declaration
}
```

#### Boas práticas

O funcionamento do *hoisting* pode causar erros dificeis de depurar caso não saibamos do seu funcionamento e resultar em estados inesperados nas variáveis. De modo a evitar o surgimento de bugs e melhorar a legibilidade do código, é uma boa prática *sempre* declarar as variáveis no inicio de cada escopo e evitar usar variaveis que ainda não foram declaradas (o uso de *let* e *const* evita isso).

### Null e Undefined

São valores denominados ***nullish***.

**Undefined** é utilizado pelo Javascript quando temos uma variável que não foi inicializada com nenhum valor. 

```javascript
var n
console.log(n)    // sera retornado o tipo undefined
```

**Null** é utilizado quando queremos evitar que uma variável fique como *undefined* mas não desejamos atribui nenhum valor a ela.

```javascript
var n = null
console.log(n)    // sera retornado null
```

O Javascript utiliza *cópia por referência* para atribuição de valores. O mesmo não ocorre para tipos primitivos, onde é utilizada a *cópia por valor*.

```Javascript
// Object simples
var a = {nome: 'João'}

// Na atribuicao de objetos, ocorre a copia por referencia.
var b = a

/* 
Como as variáveis 'a' e 'b' apontam para o mesmo endereco de memoria, se alterarmos uma propriedade de 'b', o conteúdo de 'a' tambem sera alterado
*/
b.nome = 'Pedro'

console.log(b.nome)    // 'Pedro'
console.log(a.nome)    // 'Pedro'
```

O **null** também é util quando desejamos reinicializar o valor de um objeto.

```javascript
var a = {nome: 'João'}

a = null
console.log(a)    // null
```
