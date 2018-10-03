# Ansible Docker sample

Primeiramente gostaria de deixar claro que este é um projeto para exemplificar a utilização de Docker e Ansible para provisionamento de ambientes.
Gostaria de agradecer o pessoal do Passei Direto pela oportunidade de criação. Qualquer alteração será bem vinda!
Abaixo segue uma explicação de como utiliza-los

*First of all I would like to make it clear that this is a project to exemplify the use of Docker and Ansible for environment provisioning.*
*I would like to thank the Passei Direto staff for the creative opportunity. Any change will be welcome!*
*Below is an explanation of how to use them!*

## Getting Started

O objetivo é demonstrar como utilizar Ansible e Docker. 
Aqui utilizei o Docker-Compose para facilidar a criação e a necessidade de escala dos containers que pode ser realizado com poucos comandos.

*The goal is to demonstrate how to use Ansible and Docker.*
*Here I used Docker-Compose to facilitate the creation and the need to scale containers that can be accomplished with few commands.*

### Prerequisites

Para o projeto foi utilizado:

*For the project was used:*

- CentOS Linux release 7.5.1804 (Core)
- ansible 2.6.4

### Installing

Para iniciar precisamos configurar algumas coisas antes.
Ja com o ansible instalado vamos fazer o seguinte:

*To start we need to configure some things before.*
*Already with ansible installed we will do the following:*

```
git clone https://github.com/victorarthae/ansible-docker-sample &&
cd ansible-docker-sample/ &&
chmod +x *.sh &&
```


## Setting up ansible
No caso o meu ambiente não tem saída para internet, então eu utilizei um proxy para conseguir baixar as coisas.
Caso você não precise utilizar o proxy basta retirar as roles de "setproxy" e "unsetproxy" do [automated-orchestration.yml](https://github.com/victorarthae/ansible-docker-sample/blob/master/automated-orchestration.yml)

Outro ponto, eu utilizei uma vm que tinha criado para realizar o projeto mas ele pode ser executado na mesma maquina que esta rodando o Ansible (a nivel de conhecimento).
Para alterar o ip do host que irá receber os containers va até o [hosts](https://github.com/victorarthae/ansible-docker-sample/blob/master/inventories/prod/hosts)

Caso tenha duvida sobre como criar uma VM-kvm via ansible eu deixei algumas partes para consulta [neste repositorio](https://github.com/victorarthae/infra-scripts).
O Ansible utiliza ssh para realizar seus comandos, então certifique-se de seu host ter as chaves criadas e vinculadas ao authorized_hosts, se tiver duvida em como fazer isso dê uma lida [neste artigo da DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)

*In case my environment has no internet connection, then I used a proxy to get things down.
*If you do not need to use the proxy, simply remove the "setproxy" and "unsetproxy" roles from [automated-orchestration.yml](https://github.com/victorarthae/ansible-docker-sample/blob/master/automated-orchestration.yml)
*Another point, I used a vm that had been created to carry out the project but it can be executed on the same machine that is running the Ansible (knowledge level).*

*To change the host ip that will receive the containers, go to [hosts](https://github.com/victorarthae/ansible-docker-sample/blob/master/inventories/prod/hosts)*

*If you have doubts about how to create an VM-kvm via ansible I left some parts for consultation [in this repository](https://github.com/victorarthae/infra-scripts).*
*Ansible uses ssh to perform its commands, so make sure your host has the keys created and linked to authorized_hosts, if you have any questions on how to do this, read this [DigitalOcean article](https://www.digitalocean.with/community/tutorials/how-to-set-up-ssh-keys-2)*

### Starting automation

Depois de ter configurado chave de acesso, proxy (caso preciso) e qual host irá receber os containers, esta na hora de começar a automação.
Para isso usaremos o comando dentro da pasta do projeto:

*Once you have configured access key, proxy (if necessary) and which host will receive the containers, it is time to start automation.*
*For this we will use the command inside the project folder:*

```
ansible-playbook -i inventories/prod/hosts automated-orchestration.yml
```
