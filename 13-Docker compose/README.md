## Multiplos container usando Docker compose

### O que é Docker compose
O Docker compose nos auxilia na 
- Orquestração 
- Criação 
- Administração 

Dessa forma podemos administra de forma facil um conjunto de containers a partir do uso de um simples arquivo de configuração.

### Beneficios
Como beneficio temos diversos ambientes isolados em um mesmo host , seja o ambiente de
- Desenvolvimento 
- Testes 
- Homologação.

### Tudo o que já vimos antes
Tudo o que já vimos antes podemos encontrar no uso do docker compose.

Podemos tambem usar volumes para auxiliar a manter os dados e alem disso ao modificar algo em algum container só é recriado o que foi mudado.

### Instalando o docker-compose
Podemos instalar o docker-compose usando o **pip**.
```sh
pip install docker-compose
```

### Conhecendo o arquivo docker-compose.yml

#### Heander do docker-compose.yml
Inicialmente o arquivo docker-compose.yml se inicia com a **versão** usada pelo compose.

> Temos diversas versões para o compose.

#### Services
Em seguida temos os **services** , neles declaramos os containers que compoem a pilha de aplicações.

> Podemos ter diversos services.

#### Config Options
Em cada service podemos encontrar dentro dele as configurações do container , ela tem o nome de **config options** e é resposavel por declarar as opções de cada container.

Podemos encontrar no config options
- Image  (Com o image informamos o nome e uma tag da imagem usada , usado com o o **build** podemos contruir uma imagem com o nome e tag informados.) 
- Ports  ( É responsavel por expor portas do serviço , por padrão funciona **HOST:CONTAINER**.)
- Network (É resposavel por informar qual a rede o container fara parte)
- Build (Recebe um caminho de um possivel Dockerfile)
- Volumes (Auxilia oferecendo um recurso de bind , dessa forma ajudando na persistencia de dados e named volumes.)

#### Footer 
Já o **footer** podemos encontrar as declarações de configurações personalizadas que usamos anteriormente no **Config Options**.


### Criando o primeiro docker-compose.yml
Primeiro vamos criar um arquivo Dockerfile , com esse arquivo vamos inserir as configurações necessarias para a criação de um projeto e veja o codigo para entender melhor.
```sh
FROM python:3.4-alpine
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

Em seguida podemos criar nosso arquivo docker-compose.yml , com ele vamos criar nosso serviço. 

```sh
version: '3'
services:
  web:
    build: .
    ports:
     - "5000:5000"
  redis:
    image: "redis:alpine"
```

Agora vamos ver a aplicação que vamos usar , inicialmente vamos usar um codigo Python que usa o framework chamado **flask**.
```sh
from flask import Flask
from redis import Redis

app = Flask(__name__)
redis = Redis(host='redis', port=6379)

@app.route('/')
def hello():
    count = redis.incr('hits')
    return 'Hello World! I have been seen {} times.\n'.format(count)

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True)
```

Para esse projeto funcionar será necessario o uso de algumas bibliotecas que serão instaladas usando o arquivo **requirements.txt** e nele temos as bibliotecas necessario para o projeto funcionar.
```sh
flask
redis
```

### Entendendo comandos basicos do Docker-compose.
Assim como o client docker , podemos realizar comando usando o docker-compose e podemos ver como eles são bem parecidos.

#### Como funciona os comandos
Basicamente o uso dos comandos funciona , primeiro o docker-compose , segundo a opção que vamos usar , o terceiro é o comando e por fim o quarto argumento.

Podemos usar como exemplo o uso do **ps** que é uma opção para verificar os container em funcionamento.
```sh
sudo docker-compose ps
```

Ou então usar a opção **up** e usar como comando o **-d** que é para ele funcionar em background.
```sh
sudo docker-compose up -d
```

#### O comando UP
O comando UP é usado para subir um novo serviço , podemos ver como usar ele da seguinte forma
```sh
sudo docker-compose up -h
```

Alem disso temos a opção de subir um serviço em background usando o **-d** ou até forçar para ele ser recriado usando **--force-recreate**.

Abaixo podemos ver como ele funciona em background.
```sh
sudo docker-compose up -d
```

Podemos tambem forçar para ele recriar o serviço usando
```sh
sudo docker-compose up -d --force-recreate
```

#### Down
O comando down é resposavel por parar um container e apagar , dessa forma ao usar ele podemos remover e assim não usando recursos do host.

Podemos apagar todas as imagens usadas no serviço usando
```sh
sudo docker-compose down --rmi all
```

Ou podemos apagar elas de forma local
```sh
sudo docker-compose down --rmi local
```

Tambem podemos apagar volumes usando
```sh
sudo docker-compose down -v
```

#### ps
Podemos usar o comando **ps** para listar containers e podemos usar ele 
```sh
sudo docker-compose ps 
```


#### logs
Caso queira ver o log do container podemos usar o **logs** , assim podemos ver informações de saida com mais precisão.
```sh
sudo docker-compose logs -f
```

Caso queira passar um serviço especifico para podemos usar
```sh
sudo docker-compose logs -f SERVICE_NAME
```

#### pull 
Podemos obter imagens usando o comando pull e é bem semelhante ao docker.
```sh
sudo docker-compose pull nginx
```


#### images
Podemos usar o imagem para listar imagens usadas pelo container criado.
```sh
sudo docker-compose images
```

#### top
Podemos ver os processos em funcionamento usando o top.
```sh
sudo docker-compose top
```

Ou podemos passar o nome do serviço que queremos analisar usando
```sh
sudo docker-compose top SERVICE_NAME
```

#### stop
O stop é resposavel por parar o funcionamento do container , podemos usar da seguinte forma
```sh
sudo docker-compose stop 
```

Ou podemos passar o nome do serviço que queremos parar.
```sh
sudo docker-compose stop SERVICE_NAME
```

#### start
Depois de parar o container é possivel iniciar ele usando start ,  podemos usar ele da seguinte forma
```sh
sudo docker-compose start 
```

Podemos tambem iniciar passando o nome do serviço
```sh
sudo docker-compose start SERVICE_NAME
```

#### exec (tty)
Podemos executar comando em nosso container em funcionamento usando o **exec** , dessa forma podemos interagir diretamente com o container
```sh
sudo docker-compose exec SERVICE_NAME sh
sudo docker-compose exec SERVICE_NAME ps
```
