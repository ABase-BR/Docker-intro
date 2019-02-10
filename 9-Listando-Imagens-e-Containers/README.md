## Listando Imagens e Containers

### Listando imagens
Agora que já sabemos como criar as nossas imagem vamos ver como listar elas e ver mais informações sobre nossas imagens.

Antes de tudo vamos aprender a **listar as imagens** , podemos fazer isso facilmente usando
```sh
sudo docker images
```
Ao executar podemos ver as seguintes informações 
- REPOSITORY (é o respositorio da imagem , podemos ver o nome e até de onde foi baixado.
> Por padrão é usado o Dockerhub , porem se a imagem foi baixada de outro servidor é possivel ter o endereço na frente do nome

- TAG (Tag é usada para diferenciar uma imagem , podemos seguir as boas praticas e inserir a versão do projeto utilizado)
- IMAGE ID (é o ID unico da imagem e pode ser usado para identificar a maquina assim como o nome.
> ela tambem pode ser identificada pelos 5 primeiros caracteres do ID.

- CREATED (é quando a imagem foi criada)
- SIZE (é o tamanho que a imagem está ocupando)

### Listando containers
Podemos listar container usando a opção **ps**.
```sh
sudo docker ps
```

O resultado são os seguintes
- CONTAINER ID (É o numero unico do container)
- IMAGE (É a imagem usada pelo container)
- COMMAND (Como o container é volatil ele sempre vai precisar de um serviço rodando para manter o container funcionando.
- CREATED (Quando o container foi criado)
- STATUS (Quando o container foi ligado , mostra quando tempo está UP)
- PORTS (pois portas estão expostas)
- NAMES (É o nome dado ao container , por padrão ele sorteia e podemos tambem dar nomes a ele.
