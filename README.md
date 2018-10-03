# Ansible Docker sample

Primeiramente gostaria de deixar claro que este ém projeto para exemplificar a utilizaç de Docker e Ansible para provisionamento de ambientes.
Gostaria de agradecer o pessoal do Passei Direto pela oportunidade de criaç. Qualquer alteraç seráem vinda!
Abaixo segue uma explicaç de como utiliza-los

## Getting Started

O objetivo éemonstrar como utilizar Ansible e Docker. 
Aqui utilizei o Docker-Compose para facilidar a criaç e a necessidade de escala dos containers que pode ser realizado com poucos comandos.

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
No caso o meu ambiente nãtem saí para internet, entãeu utilizei um proxy para conseguir baixar as coisas.
Caso vocêãprecise utilizar o proxy basta retirar as roles de "setproxy" e "unsetproxy" do [automated-orchestration.yml](https://github.com/victorarthae/ansible-docker-sample/blob/master/automated-orchestration.yml)

Outro ponto, eu utilizei uma vm que tinha criado para realizar o projeto mas ele pode ser executado na mesma maquina que esta rodando o Ansible (a nivel de conhecimento).
Para alterar o ip do host que iráeceber os containers va até [hosts](https://github.com/victorarthae/ansible-docker-sample/blob/master/inventories/prod/hosts)

Caso tenha duvida sobre como criar uma VM-kvm via ansible eu deixei algumas partes para consulta [neste repositorio](https://github.com/victorarthae/infra-scripts).
O Ansible utiliza ssh para realizar seus comandos, entãcertifique-se de seu host ter as chaves criadas e vinculadas ao authorized_hosts, se tiver duvida em como fazer isso dêma lida [neste artigo da DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)

### Starting automation

Depois de ter configurado chave de acesso, proxy (caso preciso) e qual host iráeceber os containers, estáa hora de começ a automaç.
Para isso usaremos o comando dentro da pasta do projeto:

```
$ ansible-playbook -i inventories/prod/hosts automated-orchestration.yml
```

Apóodar este comando o Ansible começá provisionar tudo necessario para as aplicaçs.

### Testing

Existem trêscripts para testar a aplicaç:

Testando a criaç de uma anotaç
*Primeiro parametro é IP do host onde estãos containers*
*Segudo parametro é mensagem da anotaç*
```
$ ./cria_anotacao.sh 192.168.100.191 "teste asdasd"
OK
```

Testando a listagem das anotaçs
*Primeiro parametro é IP do host onde estãos containers*
```
$ ./listar_anotacoes.sh 192.168.100.191
[{"Id":1,"Text":"`teste asdasd` = ''","CreateDate":"2018-10-03T18:39:21.000Z"}]
```

Testando a listagem das anotaçs 
*Primeiro parametro é IP do host onde estãos containers*
*Segudo parametro é ID da anotaç*
```
$ ./deleta_anotacao.sh 192.168.100.191 1
[{"Id":1,"Text":"`teste asdasd` = ''","CreateDate":"2018-10-03T18:39:21.000Z"}]
```

### Final consideration

Espero que seja úeste projeto e caso tenha duvidas pode enviar para victorragarcia@gmail.com



