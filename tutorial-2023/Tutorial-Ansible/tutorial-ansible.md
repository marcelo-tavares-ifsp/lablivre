# Ansible 
Tutorial do Ansible

----

## Como utilizar

Para utilizar o Ansible é necessário estar na biblioteca /etc/Ansible/

~~~
sudo su
cd /etc/Ansible
~~~~

Após isso crie um arquivo .txt com o nome que você preferir neste caso será chamado de hosts

----

## Configuração dos alvos do processo (inventário)

Cada arquivo que contém as máquinas onde o script (playbook) será aumtomatizado, ou seja, executado é chamado de inventário, não existe limites em relaço a quantas máquinas podem compor um inventário. Para a criação do arquivo .txt que será utilizado como inventário para a execução coloque inicialmente no terminal:

~~~
nano hosts
~~~

Em seguida para que o código .yaml funcione é preciso passar como parâmetro um arquivo Hosts, que contenha o conjunto de ip das máquinas, que deverá ser escrito desta maneira:

~~~
[lab14]
10.100.14.30 
10.100.14.33
10.100.14.37	
10.100.14.43	
10.100.14.82	
10.100.14.45	
10.100.14.46	
10.100.14.49	
10.100.14.62	
10.100.14.69	
10.100.14.70	
10.100.14.72	
10.100.14.73	
10.100.14.75	
10.100.14.76	
10.100.14.77	
10.100.14.78	
10.100.14.80	
10.100.14.90	
10.100.14.59	
~~~

Observe que é necessário e possível a criação de mais de um conjunto desses ips, ou seja, pode se criar diversas divisões para que na linha de comando do Ansible, seja possível a escolha de determinados conjuntos de ips.

----

## Comandos do Ansible

Para utilizar o ansible é necessário utilizar apropriadamente sua sintaxe, cada .yaml é chamado de playbook, o mesmo tem que ser invocado dessa maneira, ou seja ansible-playbook, logo abaixo segue um exemplo de utilização deste comando:

ansible-playbook -i lab14 playbook.yaml 

ou 

ansible-playbook -i lab14 .yaml 

----

## Utilizando o Ansible para para gerenciamento o veyon-master

### Ativando o Veyon-master

~~~ Este arquivo é em .yaml
- name: configuração do veyon
  hosts: lab14
  become: yes
  tasks:
  - name: ativando veyon multiseat
    ansible.builtin.shell: |
      veyon-cli config set Service/MultiSession true
      systemctl restart veyon.service
~~~

----

### Desativando o Veyon-master

~~~Este código é em .yaml
- name: configuração do veyon
  hosts: lab14
  become: yes
  tasks:
  - name: desativando veyon multiseat
    ansible.builtin.shell: |
      veyon-cli config set Service/MultiSession false
      systemctl restart veyon.service
~~~

----

## Criando logs no Ansible

A utilização de logs é essencial uma vez que o resultado do script pode ter sido executado de maneira incorreta, ou seja, tenha passado para as máquinas mas não ter tido o resultado esperado, ou até mesmo nem sequer rodado no "alvo"; portanto o log é uma maneira eficaz de manter o contole sobre a distribuiço dos scripts, e sobre o resultado que estes trazem, ainda mais se utilizado em um ambiente com diversas máquinas.

----

## Utilizando o Ansible para mandar emails

O Ansible pode vir com uma configuraço que não possui a biblioteca necessária para que o envio de emails seja "efetivado", ou seja, pode no vir configurado da maneira ideal, o que tem que se fazer é instalar a biblioteca community.general.mail 6.5.0.

Caso a biblioteca não tenha sido instalada:
~~~
ansible-galaxy collection install community.general
~~~

ou 

Caso apenas seja necessário atualiza-la:
ansible-galaxy collection install community.general --update

----

### Utilizando o Ansible para mandar emails de logs



----
