## Subindo imagem para o Dockerhub

### Conhecendo o Dockerhub
O dockerhub basicamente é um repositorio publico de imagens , lá podemos encontrar imagens oficiais como por exemplo
- NGINX
- DEBIAN
- MYSQL

Quanto tambem imagens publicas de pessoas , tambem podemos pagar para ter repositorios privados e por padrão temos 1 gratuito. 
```sh
https://hub.docker.com/
```


### Criando conta no Dockerhub
Podemos baixar imagens sem ter conta , porem alguma é necessario ter uma conta e podemos criar uma conta em
```sh
https://hub.docker.com/signup
```

### Entendo sobre stars
Stars é uma forma de pontuar reputação de uma imagem , funciona semelhante ao github e quanto mais starts mais bem conceituada é uma imagem.

### Imagem oficial e não oficial
Como eu falei anteriormente é possivel obter imagens oficiais e subir as nossas proprias imagens para o Dockerhub.

Eu vou criar uma imagem que tem como função subir uma API em Node e subir ela para meu dockerhub.

### Subindo imagem para o Dockerhub
Primeiro precisamos ter uma imagem em nossa maquina , depois precisamos estar logados no Dockerhub e depois é só dar o comando **docker push**.
```sh
sudo docker push "greenmind/debian:nginx"
```

Depois disso nossa imagem vai ser inserida na sua pagina do Dockerhub e podera ser usada por qualquer pessoal se estiver publica.

### Obtendo imagem usando pull
Depois de subir nossa maquina para o Dockerhub podemos obter ela usando o comando **docker pull** e tambem precisamos estar logados no dockerhub.

Podemos obter a imagem usando
```sh
sudo docker pull greenmind/debian:nginx
```