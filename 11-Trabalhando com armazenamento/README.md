## Trabalhando com armazenamento
Um volume é basicamente um diretorio do container que é mapeado para persistir seus dados (já que o containers é volatil) independente da vida util do container.

### Como funciona
O volume permite manter os dados , mesmo que o container seja deletado , é mapeado em um diretorio do host , em outro container ou até outro volume.

Um volume é criado quando um container é criado.

### Temos tres tipos de volumes

#### Host directoty as a data volume - Volume entre host e container
- Volume é salvo no Host.
- Não é escalavel.

Podemos ver um exemplo de uso , vamos compartilhar um arquivo que está em nosso host no diretorio **/home/user/site**.
```sh
sudo docker run -d --name server_web -v /home/user/site:/usr/local/apache2/htdocs -p 80:80 httpd
```


#### Data-only Container - Container como volume
- O volume é portavel e não é atrelado ao host.
- Volatil caso container seja removido ou falhar.

----------------41-1.png

Iniciamente vamos usar o docker create , ele é resposavel por criar nosso container e deixar ele em stand by.

inicialmente vamos criar o nosso volume usando o docker create , da seguinte forma
```sh
sudo docker create -v "/usr/local/apache2/htdocs" --name datasite ubuntu:14.04
```


Podemos ver se ele vai estar disponivel
```sh
docker ps
```

Em seguida podemos fazer ele funcionar usando o volume de outra maquina , que por recomendação use um sistema operacional.
```sh
docker run --name web_volumes -d --volumes-from datasite -p 9092:80 httpd
```

E agora , como podemos obter os arquivos do volume ?

Podemos usar
- entrar no container
- docker cp

usando o docker cp
```sh
sudo docker cp /home/ricardo/site/index.html datasite:/usr/local/apache2/htdocs
```

Parando o container
```sh
sudo docker stop web_volumes
```

removendo container
```sh
sudo docker rm web_volumes
```

Criando novamente o container e podemos ver que ainda vai se mantido os dados.
```sh
docker run --name web_volumes -d --volumes-from datasite -p 9092:80 httpd
```


#### Shared-store Volume - Docker Volume
- Ele tem um problema , maior overhead de disco.
- Porem ele tem uma maior segurança dos dados.
- Compativel com plugin local , NFS , CIFS e Cluster.


Podemos usar o shared-storage volume para criar volumes , dessa forma não precisamos criar um container apenas para isso e o unico problema é o possivel overhead devida a segunda camada de comunicação.

> Esse é o metodo mais importante para mapiar volumes.

Vamos criar o volume
```sh
sudo docker volume create --name data
```

Em seguida vamos listar os volumes
```sh
sudo docker volume ls
```

Depois vamos iniciar um container
```sh
sudo docker run -it --name cont_volume -v "data:/tmp" ubuntu:14.04
```