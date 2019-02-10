## Conhecendo o conceito
### Conhecendo o Docker​ ​Engine
O docker engine é um **daemon** , ele é nos auxilia na construção , no envio e para executar nossos containers.

### Conhecendo o Docker Client
Já o Docker client é responsável por receber as entradas do usuário e as enviar para a engine.

Podemos ter um client e o engine na mesma maquina. Porem eles podem ser executados em hosts diferentes.

### Conhecendo o Docker Registry​​
O Docker registry é responsável por armazenar nossas imagens , ele pode ser usado de forma local ou criar o nosso próprio servidor de imagens.

Esse servidor pode ser privado ou publico , um exemplo de servidor publico é o Dockerhub onde podemos encontrar diversas imagens e até subir a nossa.


### Conhecendo o Dockerfile
O dockerfile é um arquivo que auxiliar na criação de uma imagem , basicamente é usado instruções e elas são aplicadas em uma determinada imagem para ue outra imagem seja criada baseada nas modificações.

Mais pra frente vamos aprender como criar nosso arquivo Dockerfile e como podemos subir nossa imagem para o dockerhub.

### Conhecendo o Docker compose
O docker compose é uma ferramenta para nos auxiliar na criação de múltiplos containers Docker , com elas podemos configurar todos os parâmetros necessários para executar um container a partir de um arquivo de definição.

Vamos imaginar que nesse arquivo de execução podemos selecionar definir determinados serviços , podemos setar portas abertas , variáveis de ambiente , volumes , configurar redes e muitas possibilidade que não conseguimos apenas com o Dockerfile.


 