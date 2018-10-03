# Ansible Docker sample

Primeiramente gostaria de deixar claro que este é um projeto para exemplificar a utilização de Docker e Ansible para provisionamento de ambientes.
Gostaria de agradecer o pessoal do Passei Direto pela oportunidade de criação. Qualquer alteração será bem vinda!
Abaixo segue uma explicação de como utiliza-los

## Getting Started

O objetivo é demonstrar como utilizar Ansible e Docker. 
Aqui utilizei o Docker-Compose para facilidar a criação e a necessidade de escala dos containers que pode ser realizado com poucos comandos.

### Prerequisites

Para o projeto foi utilizado:

- CentOS Linux release 7.5.1804 (Core)
- ansible 2.6.4

### Installing

Para iniciar precisamos configurar algumas coisas antes.
Ja com o ansible instalado vamos fazer o seguinte:

```
$ git clone https://github.com/victorarthae/ansible-docker-sample &&
cd ansible-docker-sample/ &&
chmod +x *.sh &&
```

### Setting up ansible
No caso o meu ambiente não tem saída para internet, então eu utilizei um proxy para conseguir baixar as coisas.
Caso você não precise utilizar o proxy basta retirar as roles de "setproxy" e "unsetproxy" do [automated-orchestration.yml](https://github.com/victorarthae/ansible-docker-sample/blob/master/automated-orchestration.yml)

Outro ponto, eu utilizei uma vm que tinha criado para realizar o projeto mas ele pode ser executado na mesma maquina que esta rodando o Ansible (a nivel de conhecimento).
Para alterar o ip do host que irá receber os containers va até o [hosts](https://github.com/victorarthae/ansible-docker-sample/blob/master/inventories/prod/hosts)

Caso tenha duvida sobre como criar uma VM-kvm via ansible eu deixei algumas partes para consulta [neste repositorio](https://github.com/victorarthae/infra-scripts).
O Ansible utiliza ssh para realizar seus comandos, então certifique-se de seu host ter as chaves criadas e vinculadas ao authorized_hosts, se tiver duvida em como fazer isso dê uma lida [neste artigo da DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)

### Starting automation

Depois de ter configurado chave de acesso, proxy (caso preciso) e qual host irá receber os containers, está na hora de começar a automação.
Para isso usaremos o comando dentro da pasta do projeto:

```
$ ansible-playbook -i inventories/prod/hosts automated-orchestration.yml
```

Após rodar este comando o Ansible começará a provisionar tudo necessario para as aplicações.

### Testing

Existem três scripts para testar a aplicação:

Testando a criação de uma anotação
*Primeiro parametro é o IP do host onde estão os containers*
*Segudo parametro é a mensagem da anotação*
```
$ ./cria_anotacao.sh 192.168.100.191 "teste asdasd"
OK
```

Testando a listagem das anotações
*Primeiro parametro é o IP do host onde estão os containers*
```
$ ./listar_anotacoes.sh 192.168.100.191
[{"Id":1,"Text":"`teste asdasd` = ''","CreateDate":"2018-10-03T18:39:21.000Z"}]
```

Testando a listagem das anotações 
*Primeiro parametro é o IP do host onde estão os containers*
*Segudo parametro é o ID da anotação*
```
$ ./deleta_anotacao.sh 192.168.100.191 1
[{"Id":1,"Text":"`teste asdasd` = ''","CreateDate":"2018-10-03T18:39:21.000Z"}]
```

### Final consideration

Espero que seja útil este projeto e caso tenha duvidas pode enviar para victorragarcia@gmail.com


