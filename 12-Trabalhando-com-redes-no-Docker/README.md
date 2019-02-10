## Trabalhando com rede no Docker
A comunicação é uma parte importante para os nossos containers , pois ela é usada para de maneira segura , tranferir dados de um container para o outro.

### Linking - Linkando containers
O container usando linking tem acesso aos dados do container de destino e o linking permite conexões entre containers atraves dos nomes.

- Simples
- Porem seu uso é considerado absoleto e possivelmente as proximas versões nao vão suportar mais.
- Ele é muito usado para disponibilizar microserviços.

Vamos criar um container de destino
```sh
sudo docker run -d --name database -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=teste -e MYSQL_USER=user -e MYSQL_PASSWORD=pass mysql:5.5
```

Podemos agora criar a conexão
```sh
sudo docker run -d -p 8080:80 --name php --link database:db -v /home/user/site:/var/www/html php:5.6-apache
```


### User-defined networks - usando docker network
Esse metodo é o sucesso do linking , temos a possibilidade de criar diversas redes proprias e ainda permitir a comunicação entre containers atraves do uso de nomes.

- É um metodo seguro , a rede isolada para comunicar dos containers.
- Acaba sendo um pouco complexo pois precisamos criar nossas redes bridges.

#### ajuda
```sh
sudo docker network -h
```

#### Criando nova rede
Primeiro vamos criar a rede
```sh
sudo docker network create redeA
```

Em seguida podemos criar duas maquinas para se comunicar com a redeA.
```sh
sudo docker run -itd --name ubuntu --network=redeA ubuntu
sudo docker run -itd --name ubuntu2 --network=redeA ubuntu
```

#### Desconectando 
Vamos desconectar as duas maquinas que criamos.

```sh
sudo docker network disconnect redeA ubuntu
sudo docker network disconnect redeA ubuntu2
```

Depois de desconectar as duas maquinas podemos usar 
```sh
sudo docker network rm redeA
```

Podemos checar se for removida usado
```sh 
sudo docker network ls
```

### Rede Host
O conceito de host no docker é bem interessante , pois ele funciona de forma isolada e com o uso do host é possivel configurar o container para que ele faça parte da rede assim podendo realizar testes de reconhecimento como se fosse uma maquina da rede.
