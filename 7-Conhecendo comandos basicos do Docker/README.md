## Conhecendo comandos basicos do Docker
### Executando comandos
Temos diversos comandos no Docker , aqui não vou conseguir falar sobre todos e para qualquer duvida eu recomendo fortemente o uso da ajuda.
```sh
sudo docker --help
```


### run
O comando **docker run** é usado para iniciar um novo container , podemos ver como usar essa opção
```sh
sudo docker run --help
```

> Primeiro devemos saber como obter uma imagem , ver as imagens e ai vou demostrar como inicar um container.

### pull
O comando **docker pull** é resposavel por obter uma imagem , essa imagem pode ser do DockerHub ou de outro servidor de imagens.

Podemos usar ele da seguinte forma
```sh
sudo docker pull debian
```
> Podemos querer escolher uma terminada tag , senão ele vai baixar a versão latest.

### images
O comando **docker images** é resposavel por listar as imagens que temos em nossa maquina , assim podemos ver qual imagem usar e até qual TAG.

Vamos usar apenas
```sh
sudo docker images
```

### Executando em background
Agora que já sabemos como obter uma imagem e como listar elas vamos executar um container em background.
```sh 
sudo docker run -d debian
```

Usamos o **-d** para ele iniciar em background.

### Acesso a shell e excluindo quando sair
Anteriormente vimos como criar um container em background , agora vou mostrar como criar e já ter acesso ao container.

Podemos usar a opção **-it** , essa opção é a **-i** de interative e a **-t** chama um programa unix para ter acesso usando TTY.

Tambem vamos usar o **-rm** , dessa forma ele vai ser removido assim que for usado.
```sh
sudo docker run -it --rm debian
```

### Listando containers
Podemos listar os container que estão em funcionamento usando o **ps** e ele nos ajuda muito para saber quais containers estão em funcionamento.
```sh
sudo docker ps
```

### Passando um nome ao container
Podemos passar um nome ao criar um container , dessa forma podemos passar comandos usando apenas o nome e não o ID.

Podemos criar um nome para ele da seguinte forma
```sh
sudo docker --name "web_server" httpd
```

### Passando uma porta ao container
Vamos imaginar que temos um servidor web em um container , para a porta ficar disponivel podemos usar o **-p80:80** e assim deixamos a porta 80 disponivel em nosso host.
```sh
sudo docker run --name "web_server" -p80:80 httpd
```

> Lembrasse que a primeira é a porta do host e a segunda é a porta do container **-p80:80**.

### Volumes
Vamos realizar mapeamento da seguinte forma.

Primeiro precisamos especificar qual origem do dado no host e segundo onde devemos montar dentro do container.

docker container run -it --rm -v "<host>:<container>" debian


### Portas
Podemos realizar o mapeamento de portas da seguinte forma.

Primeiro precisamos saber qual porta será mapeada no host e qual deve receber essa conexão dentro do container.

Depois de saber podemos realizar o uso da seguinte forma
```sh
docker container run -it --rm -p "<host>:<container>" debian
```

### Recursos (Ram e CPU)
Ao iniciar um container é possivel setar alguns limites na ultilização dos recursos.

Vou falar apenas de 
- RAM
- CPU

Podemos setar a quantidade de RAM que vai ser usada passando o **-m**.
```sh
docker container run -it --rm -m 512M debian
```
> O comando acima passamos para o container o uso de 512 MB.

Já para especificar o uso de CPU é ultilizado o uso de pesos para cada container , quanto menor o valor , menor sua prioridade e os pesos podem oscilar de 1 a 1024.
```sh
docker container run -it --rm -c 512 debian
```
> Caso não passe valor para ele , será usado o maior peso possivel e que nesse caso é 1024.
> Para entender melhor sobre vamos imaginer 3 containers , dois deles tem 512 e um 1024. Se os tres processos estiverem funcionando ao mesmo tempo. O primeiro tem 1024 e usará 50% do tempo de processamento e os outros dois processos com peso 512 usarão 25% do tempo de processamento, cada.


### Conhecendo o exec
Depois de criado tambem podemos ter acesso aos nossos containers , para isso vamos usar o exec.

Vamos supor que temos um container com o nome **web_server** e quero ter acesso a ele.

Podemos usar
```sh
sudo docker exec -it web_server
```

### Gerenciando containers
Depois que aprendemos a inserir nome em um container e subir ele para funcionar em background podemos realizar comandos como por exemplo
- stop
- start 

Podemos parar um container da seguinte maneira
```sh
sudo docker container stop meu_container
```

Podemos iniciar um container 
```sh
sudo docker container start meu_container
```