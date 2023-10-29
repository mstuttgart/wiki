---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Shell Script

Embora muita das veze utilizados juntos, os termos `shell` e `bash` não são a mesma coisa.

O termo `shell` refere-se a um programa que fornece uma interface de linha de comando para interagir com o Sistema Operacional. O termo `Bash (Bourne-Again Shell)`é um dos Unix/Linux _shells_ mais comuns e utilizados.

```mermaid
flowchart LR
User --> Shell --> Kernel --> Hardware
```

Todo script bash possui a extensão `.sh` e possui a`shebang (#!)` na primeira linha do script.

```bash
#!/bin/bash
```

_shebang_ indica qual _shell_ sera utilizado para executar o script.

## Variáveis

As variáveis não devem possuir espaço entre o nome da variável, o simbolo de atribuição e o seu valor.

```bash
#!/bin/bash

# errado
NAME ="Maria"
NAME= "Maria"

# correto
NAME="Maria"

# sempre usar aspas duplas
echo "$NAME"
```

Também é possível realizar a expansão da variável:

```bash
#!/bin/bash

echo "${NAME}"  # Maria

# tamanho do conteudo da variavel
echo "${#NAME}"   # 5
```

É sempre uma boa ideia usar aspas "aspas" ao redor das variáveis para manter os espaços em branco e evitar problemas com variáveis vazias. Todas as variáveis são consideradas globais. Variáveis locais são precedidas por `local`.

É possível armazenar o valor de um comando dentro de uma variável, inserindo o comando entre `$(...)`.

```bash
#!/bin/bash

DATA=$(date)
echo "Data de Hoje: $DATA"

# o comando 'unset' apaga o conteudo da variavel
unset DATA
```

O Bash tambem possui variáveis nativas. São elas:

* `$?`: valor retornado pelo ultimo comando executado
* `$$`: o `PID` do script
* `$0`: o nome do script
* `$1`, `$2` ... `$9`: argumentos que foram passados para o script, na sua execução
* `$@`: todos os argumentos fornecidos ao script
* `$#`: numero de argumentos fornecidas ao script

## Expressões Aritméticas

Podemos utilizar a expressão `$((...))` para realizar operações matemáticas:

```bash
#!/bin/bash

echo $((1 + 1))   # => 2
```

## Estrutura de controle

### `TEST`

O comando `test` do shell permite vários tipos de testes muito uteis com valores numéricos, strings e arquivos. Temos os seguintes operadores para o `test`:

#### Números

* `-ne`: not equal (diferente)
* `-lt`: less than (menor que)
* `-gt`: greater than (maior que)
* `-le`: less than or equal to (menor ou igual que)
* `-ge`: greater than or equal to (maior ou igual que)
* `-eq`: equal (igual a)

#### Strings

* `==`: string é igual
* `!=`: string é diferente
* `-n`: string é não nula
* `-z`: string nula ou vazia

#### Arquivos

* `-d`: é um diretório
* `-f`: é um arquivo comum
* `-r`: o arquivo tem permissão de leitura
* `-w`: o arquivo tem permissão de escrita
* `-s`: o tamanho do arquivo é maior que zero (arquivo não vazio)

Ainda existem outros operadores para arquivos, porém esses são os mais usados.

### IF

Aqui podemos utilizar `if` como em outras linguagens. O `if` possui a seguinte estrutura:

```bash
#!/bin/bash

if test "$NAME" == "Maria"; then
    # codigo ...
elif test "$NAME" != "João"; then
    # codigo ...
else
    # codigo ...
fi
```

Tambem podemos usar a seguinte notação:

```bash
#!/bin/bash

if [ "$NAME" == "Maria" ]; then
    # codigo ...
elif [ "$NAME" != "João" ]; then
    # codigo ... 
else
    # codigo ....
fi
```

Tambem temos operadores logicos que podem ser usados em duas ou mais condições:

* `&&`: operador _AND_
* `||`: operador _OR_

```bash
#!/bin/bash

if [ "$NAME" == "Maria" ] ||  [ "$NAME" == "João" ]; then
    # codigo ...
else
    # codigo ....
fi
```

## Arrays

A criação de um array segue a seguinte sintaxe:

```bash
alunos=("joao" "maria" "jose" "ana")
```

Conseguimos acessar cada item do array através de indices, como em outras linguagens:

```bash
#!/bin/bash

# primeiro item do array: joao
echo "${alunos[0]}"

# todos os items do array: joao maria jose ana
echo "${alunos[@]}"

# numero de items no array: 4
echo "${#alunos[@]}"
```

O comando `seq` ou `{inicio .. fim}` pode ser muito util se desejamos gerar uma sequência numérica:

```bash
#!/bin/bash

echo "$(seq 5)"  # 0 1 2 3 4

echo {1..5}   # 0 1 2 3 4
```

## Shell Loops

### FOR

A seguir, temos um exemplo de uso do `for`:

```bash
#!/bin/bash

for aluno in "${alunos[@]}"; do
    echo "$aluno"
done

# =>
# joao 
# maria 
# jose 
# ana
```

Também podemos utilizar uma notação alternativa para o `for`:

```bash
# numero de alunos
len=${#alunos[@]}

for ((i=0; i < len; i++)); do
    echo "$alunos[i]"
done

# =>
# joao 
# maria 
# jose 
# ana

```

### WHILE

Exemplo de uso do `while`:

```bash
#!/bin/bash

count = 0

while test "$count" -lt 10 ; do
    echo "$count"
    $(( count += 1 ))
done

# ou, utilizando outra notação

while [ "$count" -lt 10 ]; do
    echo "$count"
    $(( count += 1 ))
done
```

Se desejamos sair do `while`, sem concluir sua condição, podemos usar o comando `brake`.

```bash
#!/bin/bash

while; do
    if test -f /tmp/lock; then
    echo "Aguardando liberação do lock..."
    sleep 1
    else
    break
    fi
done

```

## Redirecionando outputs

O bash nos permite redirecionarmos a saída de um comando para um arquivo em disco ao invés da tela do terminal. Isso é feito através do operador `>`.

O uso do `>` cria (caso não exista) ou sobrescreve o conteúdo do arquivo.

#### Exemplo:

<pre class="language-bash"><code class="lang-bash"><strong>$ echo "Hello World!" > hello.log
</strong><strong>$ cat hello.log
</strong><strong>Hello World!  
</strong></code></pre>

Nesse exemplo, o arquivo `hello.log` será criado (ou sobrescrito, caso exista) com a saída da execução do comandos do script `hello_world.sh`.

O uso do `>>` anexa a saída do comando para o fim do arquivo.

#### Exemplo:

```bash
$ echo "Bye World!" > hello.log
$ cat hello.log
Hello World!
Bye World!
```

&#x20;Aqui a saída dos comandos presentes no script serão anexadas ao final do arquivo `hello.log`.

### Redirecionamento I/O  (entrada/saída)

O redirecionamento de entrada/saída nos permite redirecionar a entrada ou saída de um comando para diretamente para um arquivo de texto. Porem ser redirecionadas a `stdin` (entrada padrão), `stdout` (saída padrão) e `stderr`(saída exclusiva para erros de execução do script).

```bash
# Utiliza o arquivo stdin.log como entrada para o script
$ bash hello_world.sh < stdin.log

# redireciona a saída do script para o arquivo stdout.log
$ bash hello_world.sh > stdout.log

# rediciona a saída de erros do scritp para o arquivo stderr.log. Nesse caso, a 
# saída padrão ainda será exibida 
$ bash hello_world.sh 2> stderr.log

# redireciona a saida padrão e a saida de erros para o arquivo stdout_err.log
$ bash hello_world.sh 2>&1 stdout_err.log

# equivalente ao comando acima
$ bash hello_world.sh 2> stderr.log > stdout.log
```

Caso o objetivo seja "esconder" a saída padrão e/ou de erros do script, podemos redirecioná-las para uma saída "nula"

```bash
$ bash hello_world 2>&1 /dev/null
```

## Referências

* [https://learnxinyminutes.com/docs/bash/](https://learnxinyminutes.com/docs/bash/)
* [https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/#introduction](https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/#introduction)
* [https://www.learnshell.org/](https://www.learnshell.org/)
* [https://learning.lpi.org/en/learning-materials/010-160/3/](https://learning.lpi.org/en/learning-materials/010-160/3/)
