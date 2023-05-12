# Ansible 
Tutorial do Ansible

----

## Como utilizar

Para utilizar o Ansible é necessário estar na biblioteca /etc/Ansible/

sudo su
cd /etc/Ansible

Após isso crie um arquivo .txt com o nome que você preferir neste caso será chamado de hosts

----

## Configuração dos alvos do processo

Para a criação do arquivo .txt coloque:

nano hosts

Em seguida para que o código .yaml funcione é preciso passar como parâmetro um arquivo Hosts, que contenha o conjunto de ip das máquinas, que deverá ser escrito desta maneira:

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

Observe que é necessário e possível a criação de mais de um conjunto desses ips, ou seja, pode se criar diversas divisões para que na linha de comando do Ansible, seja possível a escolha de determinados conjuntos de ips.

----

## Ativando o Veyon-master

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

## Desativando o Veyon-master

- name: configuração do veyon
  hosts: lab14
  become: yes
  tasks:
  - name: desativando veyon multiseat
    ansible.builtin.shell: |
      veyon-cli config set Service/MultiSession false
      systemctl restart veyon.service

----

## Comandos do Ansible

Para utilizar o ansible é necessário utilizar apropriadamente sua sintaxe, cada .yaml é chamado de playbook, o mesmo tem que ser invocado dessa maneira, ou seja ansible-playbook, logo abaixo segue um exemplo de utilização deste comando:

ansible-playbook -i lab14 ativando-veyon.yaml 

ou 

ansible-playbook -i lab14 desativando-veyon.yaml 

---

## Instalação via linha de comando | 32bits e 64bits | 
Para instalar é preciso usar um terminal como root (administrador), então, abra o terminal e com a VM limpa, entre como root através do comando: 
```sh
    su -
```
---

## Utilização básica

----

