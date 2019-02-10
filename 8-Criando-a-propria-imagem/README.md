## Criando a propria imagem
- Revisando imagem e container

Como já vimos anteriormente podemos pesquisar por imagens oficiais no dockerhub.
```sh
https://hub.docker.com/_/php
```

Alem disso podemos tambem usar imagens não oficiais , vamos ver jaja que qualquer um pode criar uma conta e subir a sua imagem personalizada.
```sh
https://hub.docker.com/u/greenmind/
```

Tem todos os projetos temos um **nome** da imagem , o nome podemos colocar o nome do projeto e um exemplo foi o **DB do VidaFacil**.
```sh
https://hub.docker.com/r/greenmind/db_vidafacil/
```

Já as TAGS podemos entender como versão de uma imagem , vou usar como exemplo o repositorio do **Debian** e podemos ver nas tags diversas versões do Debian para uso.
```sh
https://hub.docker.com/_/debian?tab=tags
```

### Criando imagem usando commit
Vamos imaginar ue temos uma imagem em funcionamento , pela imagem ser volaril assim que ela for desligada tudo será apagado e assim todas as modificações serão apagadas.

Podemos usar o commit , criar uma imagem apartir de um container modificado e assim salvar o container com as modificações.

Isso ainda é usado , porem não é uma boa pratica.

No terminal 1 - Vamos criar um container e realizar algumas modificações.
- Vamos usar o Debian
- Vamos instalar o NGINX nele

```sh
sudo docker container run -it --name container_criado debian:9.7 bash
apt-get update
apt-get install nginx -y
exit
```

Depois de sair do terminal - Vamos realizar o commit para criar uma imagem do container , só que antes é preciso parar o container que está em funcionamento e podemos fazer isso da usando o
```sh
sudo docker container stop container_criado 
```

Depois podemos realizar o commit para criar a imagem codificada , precisamos passar o nome do container e o nome que queremos da imagem.
```sh
sudo docker commit container_criado "greenmind/debian:nginx" 
```

> Podemos ver usando o comando **docker images** a imagem criada.

### Criando imagem com Dockerfile
Antes de criar um Dockerfile é necessario entender algumas instruções , depois de aprender mais sobre essas instruções estaremos prontos e vamos começar a criar o nosso arquivo Dockerfile.

## Entendo instruções
As instruções são passos seguidos pelo Docker , essas instruções são passadas atraves do arquivo Dockerfile e agora vamos entender um pouco sobre eles.

### FROM
A instrução FROM é resposavel por passar o nome da imagem e da tag que vamos usar no arquivo Dockerfile.

Vamos imagem que queremos uma imagem do Debian , podemos passar a seguinte instrução e seguido da TAG e um exemplo seria usar a versão **8** que é o Debian Jessie.
```sh
FROM debian:8
```

> Lembrando que se você passar o nome de uma imagem apenas , será usado a versão latest e isso acontece por padrão.


### MAINTAINER
O maintainer é a instrução resposavel por passar o resposavel por criar a imagem e pode ser usado caso alguem queria relatar algum problema/melhorar imagem.

```sh
MAINTAINER greenmind.sec@gmail.com
```

> Essa instrução não é obrigatoria.

### WORKDIR
O Workdir é um comando que é usado no arquivo Dockerfile , essa instrução nos auxilia na troca de diretorios e podemos usar da seguinte forma.

```sh
WORKDIR /root
```

Dessa forma estamos enviando uma instrução ao docker que desejamos ir para o diretorio **/root**.

> Essa opção pode nos ajudar , dessa forma não precisamos passar comandos como o **cd** e assim seguimos boas praticas.

### COPY
O copy é uma instrução usada para copiar algo para dentro da imagem , por exemplo..

Temos um projeto no github , esse projeto tem os codigos fontes em sua raiz e tambem o arquivo Dockerfile.

Podemos copiar tudo para um diretorio expecifico , vou dar como exemplo a copia dos arquivos locais para o diretorio /application.

```sh
COPY . /application
```

> Dessa forma será **copiado todos os arquivos do diretorio** corrente para o diretorio da imagem **/application**.


### RUN
O comando run é resposavel por passar algum comando como instrução , podemos usar como exemplo uma imagem e queremos atualizar o repositorio dela ou até instalar algo.

Podemos usar o **RUN** para isso e ele funciona da seguinte forma
```sh
RUN apt-get update
```

> Sempre que usar a imagem para instalar algo eu recomendo usar o update.

Outro exemplo é a instalação de algum programa e nunca se esqueça de passar o **-y** para que a instalação seja aceita. 
Porque senão tera um erro.
```sh
RUN apt-get install nano -y
```

> Não esqueça de passar o argumento -y , caso não passe a ordem será parada.


### EXPOSE
A instrução EXPOSE é usada para expor uma determinada porta da nossa imagem , vamos imaginar um servidor web , eles costumam funcionar por padrão na porta 80 e devemos passar a porta que queremos usar para o arquivo Dockerfile.

Vamos dar um exemplo e expor a porta **80** local.
```sh
EXPOSE 80
```

### ENTRYPOINT
O entrypoint é um argumento para ser usado caso queira usar sempre um comando ao iniciar o container e veja o exemplo para entender melhor.

Vamos imaginar que temos uma aplicação , queremos executar ela toda vez que o container for iniciado e para isso podemos usar o **ENTRYPOINT**.

> Vou usar como exemplo o NMAP , esse projeto é considerado o melhor portscan do mundo e pode nos auxliar no reconhecimento de aplicações.

Na instrução a baixo é chamado o nmap assim que o container for iniciado.
```sh
ENTRYPOINT ["nmap"]
```

### CMD
A instrução CMD eu vejo ela como um complemento do ENTRYPOINT , vamos imaginar o complemento anterior , onde passamos um programa para o ENTRYPOINT e agora vamos passar o CMD logo a baixo.

Vamos imaginar que eu executei o container , nada foi passado e o que vai acontecer?
Basicamente se nada for passado ele vai executar o CMD , nesse caso ele só está retornando a versão do projeto e em outros casos poderia ser algum comando ou até alerta.

```sh
ENTRYPOINT ["nmap"]
CMD ["--version"]
```

### Entendo a ordem das instruções
As instruções que o nosso arquivo Dockerfile tem , vou usar como exemplo o uso de uma imagem Debian , um servidor NGINX ,vamos expor a porta 80 e por fim realizar o comando para iniciar o NGINX toda vez que iniciar o container.

Nosso arquivo Dockerfile
```sh
FROM debian:9.7
RUN apt-get update
RUN apt-get install nginx -y
EXPOSE 80
EXTRYPOINT[""]
```
> Podemos criar a imagem acima usando o **docker build** , devemos passar um nome , uma tag e onde está o arquivo Dockerfile.
```sh
sudo docker build -t "greenmind/debian:nginx2
```

Agora se nós fossemos realizar uma modificação , nesse caso vamos inserir um comando acima do comando de instalação do NGINX e podemos ver que tudo a baixo será refeito.
```sh
FROM debian:9.7
RUN apt-get update
RUN apt-get install nano -y
RUN apt-get install nginx -y
EXPOSE 80
EXTRYPOINT[""]
```

> Podemos ver que os passos a baixo serão refeitos e uma outra observação é o uso do **-y** para aceitar a instalação.