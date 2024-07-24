# Single Responsability Principle (SRP)

_Princípio da Responsábilidade Única, em pt-BR._

Este postulado define o seguinte:

> Uma classe deve ter um, e somente um, motivo para mudar.

Dizemos que a classe deve ser coesa. Em outras palavras, ela deve ter uma _única_ responsabilidade.

Por que uma classe ter mais de uma responsibilidade é um problema?

Porque cada resposabilidade é algo passível de sofrer mudanças, e quanto mais responsabilidades nossa classe tiver, mais acoplada ela será, ou seja, mais impacto ela irá causar nas classes que dependem dela quando houver uma alteração em uma das responsabilidades e mais dificil será extendê-la, caso seja necessário.

A título de exemplo, vamos analisar a seguinte classe:

```python
class Server: 

	def create_connection(self):
	    pass

	def check_connection(self):
	    pass

	def close_connection(self):
	    pass

	def send_package(self):
	    pass

	def receive_package(self):
	    pass
	
```

Analisando a classe acima, percebemos claramente que ela possui duas responsabilidades: uma relacionada a conexões (criar, destruir e checar) e outra relacionado ao gerenciamento de pacotes de dados (envio e recebimento). Desse modo, todas as classes que herdarem dela, também receberão esses dois comportamentos não relacionados. Usando o `Single Responsability Principle` podemos separar a classe em duas outras classes, cada uma tratando adequadamente de sua própria responsabilidade:

```python
class ConnectionManager:
	"""Gerencia apenas a conexao"""

	def create_connection(self):
	    pass

	def check_connection(self):
	    pass

	def close_connection(self):
	    pass	
```

e

```python
class PackageManager:
	"""Gerencia apenas o envio e recebimento de pacotes de dados"""

	def send_package(self):
	    pass

	def receive_package(self):
	    pass	
```

O `Single Responsability Principle` é um dos princípios mais dificieis de serem aplicados, porque a definição da resposabilidade da classe pode variar de desenvolvedor para desenvolvedor, onde o mesmo define se algo esta ou não dentro do escopo da classe. Então, de modo a tornar mais fácil a aplicação deste princípio, devemos sempre ter em mente o domínio do problema que estamos tentando resolver e a arquitetura que iremos utilizar no design do software.
