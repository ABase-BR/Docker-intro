## Como a infraestrutura de servidores é projetada

### Antigamente sem o uso da plataforma de containers
Uma infraestrutura sem o uso de containers deixa todo o projeto mais pesado e lento.

Em toda maquina virtual tem um sistema operacional instalado , deixando o projeto muito mais lento , pesado e até aumentando o custo

Diferente do Docker a virtualização precisa de um sistema operacional e podemos ver a imagem abaixo para entender melhor.

PARAVIRTUALIZACAO-1.png
VIRTUALIZACAO-1.png

> A virtualização também pode virar um processo rápido e seguro com o uso de Vagrant.

### Como funciona com o uso de containers
Já com o uso de containers podemos ver que só é necessário obter os binários e as bibliotecas.

CONTAINERS-1.png

O Docker usa um modelo de isolamento utilizado é o virtualização a nível de sistema operacional , esse método de virtualização onde o kernel do sistema operacional permite o processamento de múltiplos processos e esses processos são executados isoladamente no mesmo host.

Esses processos isolados em execução são denominados no Docker de container.

O docker usa uma funcionalidade do kernel denominada de namespaces , ele é responsável por criar ambientes isolados entre os containers e os processos em execução não terão acesso aos recursos de outra.

Para evitar exaustão dos recursos o Docker usa a funcionalidade de cgroups do kernel e ele é responsável por criar limites do uso de hardware a disposição.

 