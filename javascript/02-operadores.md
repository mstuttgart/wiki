
# Operadores [^operators]

Existem diferentes tipos de operadores em Javascripts e esses são separados nas seguintes categorias:

- Operadores Aritméticos
- Operadores de Atribuição
- Operadores de Comparação
- Operadores Lógicos
- Operadores Condicionais
- Operadores de Tipo

## Operadores Aritméticos

São utilizados para executar operações aritméticas de números.

| Operador | Descrição                                                          |
| -------- | ------------------------------------------------------------------ |
| +        | Adição                                                             |
| -        | Subtração                                                          |
| *        | Multiplicação                                                      |
| **       | Exponenciação ([ES2016](https://www.w3schools.com/js/js_2016.asp)) |
| /        | Divisão                                                            |
| %        | Modulo (resto da divisão)                                          |
| ++       | incremento                                                         |
| --       | Decremento                                                         |         |                                                                    |

## Operadores de Atribuição

São utilizados para atribuir valores as variáveis.

Exemplo:

```javascript
x += y    // x = x + y
x++       // x = x + 1

x -= y    // x = x - y
x--       // x = x - 1

x *= y    // x = x * y
x /= y    // x = x / y

x %= y    // x = x % y
x **= y   // x = x ** y
```

### Atribuição Via Desestruturação

No Javascript, uma **atribuição via desestruturação** (do inglês, *destructuring assignment*), é uma expressão que permite extrair dados de *arrays* ou *objects* em variáveis distintas.

Exemplo com *object*:

```javascript
const pessoa = {
    nome: 'Maria',
    idade: '20'
}

// destructuring padrao
var {nome, idade} = pessoa

console.log(nome)    // 'Maria'
console.log(idade)   // 20

// pessoa nao possui o atributo 'curso', entao 'curso' recebe um valor padrao
var {nome, idade, curso='Enfermagem'} = pessoa

console.log(nome)    // 'Maria'
console.log(idade)   // 20
console.log(curso)   // 'Enfermagem'

// destructuring ignorando valores (no caso, a propriedade 'idade')
var {nome, , curso='Enfermagem'} = pessoa

console.log(nome)    // 'Maria'
console.log(curso)   // 'Enfermagem'
```

Exemplo com *array*:

```javascript
var lista = ['x', 'y', 'z']

// destructuring padrao
var [a, b, c] = lista

console.log(a)    // 'x'
console.log(b)    // 'y'
console.log(c)    // 'y'

// Separando valores em particular
var [a, b, ...resto] = [1, 2, 3, 4, 5]

console.log(a)      // 1
console.log(b)      // 2
console.log(resto)  // [3, 4, 5]

// Trocando variáveis
var [a, b] = [b, a]
```

## Operadores de Comparação

São utilizados em comparação de valores, de modo a determinar a igualdade ou diferença entre eles, sempre retornando `true` ou `false` como resultado.

| Operador | Descrição                    |
| -------- | ---------------------------- |
| ==       | igual a                      |
| ===      | igual ao valor e ao tipo     |
| !=       | diferente de                 |
| !==      | diferente de em valor e tipo |
| >        | maior que                    |
| <        | menor que                    |
| >=       | maior ou igual a             |
| <=       | menor ou igual a             |
| ?        | operador ternário            |

### Comparando tipos diferentes

Quando compara uma *string* com um número, o Javascript converte essa *string* em um valor númerico. Uma *string* vazia é convertida para `0`. Uma string não numérica é convertida para `Nan`, que sempre é considerado `false`.

Exemplo:

```javascript
console.log('1' == 1)     // true (compara apenas o valor)
console.log('1' === 1)    // false (compara valor e tipo)

console.log('1' != 1)     // false (compara apenas o valor)
console.log('1' !== 1)    // true (compara valor e tipo)

console.log('' == 0)      // true (string vazia convertida para 0)
```

É recomendável fazer uso do operador `===` de modo a comparar não apenas a igualdade de valor mas também se os valores são do mesmo tipo.

### Operador Ternário

É um operador especial que atribui que retorna um valor baseado em uma dada condição ser `true` ou `false`.

```javascript
let resultado = (nota >= 7) ? 'Aprovado' : 'Reprovado'
```

No código acima, se a condição `nota >= 7` for `true`, a variável `resultado` receberá a *string* `'Aprovado'`. Por outro lado, se a condição for `false`, `resultado` receberá a *string* `'Reprovado'`.

### Operadores Lógicos

São utilizados para executar operações lógicas entre variáveis ou valores.

| Operador | Descrição |
| -------- | --------- |
| &&       | and       |
| \|\|     | or        |
| !        | not       |

Exemplo:

```javascript
// operacoes com and
undefined && 'texto'   // undefined
null      && 'texto'   // null
NaN       && 'texto'   // Nan
0         && 'texto'   // 0
false     && 'texto'   // false
''        && 'texto'   // ''

// operacoes com or
undefined || 'texto'   // 'texto'
null      || 'texto'   // 'texto'
NaN       || 'texto'   // 'texto'
0         || 'texto'   // 'texto'
false     || 'texto'   // 'texto'
''        || 'texto'   // 'texto'

// operacoes com not
!(undefined && 'texto')   // false
!(null      && 'texto')   // false
!(NaN       && 'texto')   // false
!(0         && 'texto')   // false
!(false     && 'texto')   // false
!(''        && 'texto')   // false
```

### Operador de Coalescência Nula [^coales] (??)

O operador de **Coalescência Nula** `??` (do inglês, *Nullish Coalescing*) é um operador lógico que retorna o seu operando do lado direito quando o seu operador do lado esquerdo for *nullish* - `null` ou `undefined`. Ao contrário do operador OR `||`, o operando  esquerdo  é retornado se houver um valor *falsy* que não seja `null` ou `undefined`.

Exemplo:

```javascript
// operacoes com ??
undefined ?? 'texto'   // 'texto'
null      ?? 'texto'   // 'texto'

NaN       ?? 'texto'   // Nan
0         ?? 'texto'   // 0
false     ?? 'texto'   // false
''        ?? 'texto'   // ''
```

Os operadores lógicos seguem a seguinte ordem de precedência:

- `||` : operador `or` 
- `??`: operador `nullish coalescing`
- `?`: operador ternário

### Operador de Encadeamento Opcional (?.)

O operador de **Encadeamento Opcional** `?.` (do ingês, *Optional Chaining Operator*) retorna `undefined` se um objeto é *nullish* ao invés de disparar um erro. É utilizado para acessar propriedades de um objeto.

Exemplo:

```javascript
const pessoa = {nome: 'Maria'}

console.log(pessoa?.nome)    // 'Maria'
console.log(pessoa?.idade)   // undefined
```

## Operadores de Tipo

| Operador   | Descrição                                                     |
| ---------- | ------------------------------------------------------------- |
| typeof     | Retorna o tipo da variável                                    |
| instanceof | Retorma `true` se um objeto é uma instância de um tipo objeto |

Exemplo:

```javascript
const langs = ['Javascript', 'Python', 'Go', 'C']

console.log(langs instanceof Array)    // true
console.log(langs instanceof Object)   // true
console.log(langs instanceof Number)   // false
```

## Operadores de Manipulação de Bits

São operadores de *bits* utilizados para trabalhar com numeros de 32 bits. Qualquer valor númerico na operação é convertido em um número de 32 bits. O resultado é reconvertido para um `Number`.

| Operador | Descrição            |
| -------- | -------------------- |
| &        | AND                  |
| \|       | OR                   |
| ~        | NOT                  |
| ^        | XOR                  |
| <<       | left shift           |
| >>       | right shift          |
| >>>      | unsigned right shift |

## Referências

[^operators]: https://www.w3schools.com/js/js_operators.asp
[^coales]: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing