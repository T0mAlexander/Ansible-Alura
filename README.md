# Guia básico de Ansible

## Requisitos mínimos

- [**Ansible**](https://developer.hashicorp.com/vagrant/downloads) instalado na máquina com versão mínima em 2.x.x
- [**Vagrant**](https://developer.hashicorp.com/vagrant/downloads) instalado na máquina com versão mínima em 2.x.x

## Instruções de uso

1. Instale o Ansible

  ```bash
  sudo dnf install -y dnf-plugins-core
  sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/fedora/hashicorp.repo
  sudo dnf install -y ansible vagrant
  ```

2. Crie um arquivo de configuração do Vagrant

  ```bash
  vagrant init <nome>
  ```

3. Inicializando uma máquina

  **3.1** - Configure o arquivo `Vagrantfile`

  ```js
  Vagrant.configure("2") do |config|

    config.vm.box = "tknerr/baseimage-ubuntu-22.04"

    config.vm.define "wordpress" do |m|
        m.vm.network "private_network", ip: "<ip-para-máquina>"
    end

  end
  ```

  **3.2** - Construa a máquina

  ```bash
  vagrant up --provider=<provedor>
  ```

  > **Aviso:** Escolha um dos [provedores de virtualização do Vagrant](https://developer.hashicorp.com/vagrant/docs/providers) antes de executar o comando acima
  >
  > **Sugestão:** para definir um provedor padrão, digite o comando abaixo:
  
  ```bash
  export VAGRANT_DEFAULT_PROVIDER=<provedor>
  ```

4. Crie um arquivo com informações do host

  4.1 - Crie o arquivo com o vim no formato `.yml`

  ```bash
  vim hosts.yml
  ```

  4.2 - Insira as seguintes informações

  ```vim
  all:
  hosts:
    <nome-do-host>:
      ansible_ssh_pass: vagrant
      ansible_ssh_user: vagrant
      ansible_ssh_private_key_file: .vagrant/machines/<host>/<provedor-vm>/private_key
      ansible_host: <ip-da-máquina>
  ```

  4.3

  ```bash
  ansible <nome-do-host> -i hosts.yml -m shell -a 'echo Hello, Ansible!'
  ```

5. Conecte-se a máquina virtual

  ```bash
  vagrant ssh
  ```

  >**Nota:** para sair da sessão, digite `exit` ou pressione **CTRL** + **D**
