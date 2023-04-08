# Ansible

-- Instalação do Ansible no Amazon Linux 2 sudo yum update sudo amazon-linux-extras list | grep ansible2 sudo amazon-linux-extras enable ansible2 sudo yum install -y ansible

-- Subindo a chave SSH para maquina com Ansible

scp -i ansible.pem ansible.pem ec2-user@44.201.218.54:/home/ec2-user/

-- Na maquina com Ansible mkdir ansible-files cd ansible-files mkdir lab_inventory cd lab_inventory vim hosts

dentro de arquivo hosts:

[web] node1 ansible_host=<ip interno da maquina 1> node2 ansible_host=<ip interno da maquina 2> node3 ansible_host=<ip interno da maquina 3>

cd .. vim web.yaml

dentro do arquivo web.yaml:

name: Apache server instalado hosts: web become: yes module_defaults: ansible.builtin.package: use: dnf

tasks:

name: Ultima versao do apache server instalado ansible.builtin.dnf: name: httpd state: latest
name: Apache started e enable ansible.builtin.service: name: httpd enabled: true state: started
name: Copiar web.html ansible.builtin.copy: src: ~/ansible-files/web.html dest: /var/www/html/index.html
vim web.html

dentro do arquivo web.html:

Apache is running fine
ansible-playbook web.yaml -i lab_inventory/hosts --private-key

Exercicio:

Reproduzir este workshop da Red Hat no Amazon Linux: https://github.com/ansible/workshops/blob/devel/exercises/ansible_rhel/1.7-role/README.pt-br.md

Subir os arquivos para um repositório no github e enviar o link do repositório para o meu e-mail: william.loliveira@hotmail.com
