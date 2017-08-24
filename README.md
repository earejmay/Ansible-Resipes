Ansible
=======

## Install

```bash
sudo apt-add-repository -y ppa:ansible/ansible && \
sudo apt-get update && \
sudo apt-get install -y ansible
```
--------------------------------------------------------------------------------


### CI
```bash
$
ansible-playbook bootstrap.yml
```
--------------------------------------------------------------------------------

### Run Local

```bash
touch playbook.yml && \
vim playbook.yml
```

```yml
---
- hosts: all
  tasks:
    - shell: echo "hello world"
```

```bash
$ ansible-playbook -i "localhost," -c local playbook.yml
```

--------------------------------------------------------------------------------

### Host file

```bash
# ansible-playbook -i {FILE} -l {ALIAS} playbook.yml

$ ansible-playbook -i hosts -l digital-ocean playbook.yml
```

The host file works with ```./ssh/config``` file

--------------------------------------------------------------------------------

## Disable Cow

In ```~/.bashrc``` add this line:

```bash
export ANSIBLE_NOCOWS=1
```

--------------------------------------------------------------------------------

# Ansible Resipes

#### Wordpress cli

[link](https://github.com/wp-cli/wp-cli)

```bash
  $
  wget -O ans http://git.io/vsgtz && \
  ansible-playbook -i "localhost," -c local ans && \
  rm ans
```

#### Locale Fix

```bash
  $
  wget -O ans http://git.io/vGK27 && \
  ansible-playbook -i "localhost," -c local ans && \
  rm ans
```

```yml
---
- hosts      : all
  become     : yes
  tasks      :

    - name      : Fix locale es_CO.UTF-8
      locale_gen:
        name    : es_CO.UTF-8
        state   : present

    - name      : Fix locale en_US.UTF-8
      locale_gen:
        name    : en_US.UTF-8
        state   : present
```
#### ZSH for ROOT

```bash
  $
  wget -O ans http://git.io/vGK6D && \
  ansible-playbook -i "localhost," -c local ans && \
  rm ans
```

-----

## Common Tasks

#### Install apt-get

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name      : Install Git
      apt       :
        pkg     : git
        state   : latest
```

#### Create File

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name      : Create File
      file      :
        path    : "~/thisfile.txt"
        state   : touch
        mode    : 0644
```

#### Create Folder

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name      : Create Folder
      file      :
        path    : "~/Documents/custom/folder"
        state   : directory
        recurse : yes
```

#### Remove Folders and Files

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name      : Remove Remove
      file      :
        state   : absent
        path    : "{{ item }}"
      with_items:
        - "~/.zshrc"
        - "~/.oh-my-zsh"
        - "~/.antigen"
        - "~/antigen.zshrc"
        - "~/.zshrc"
```

#### Make File Executable

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name   : Make File Executable
      file:
        path: /usr/bin/file
        mode: "u+rwx,g+rx,o+rx"
```

#### Apt Get Update

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name   : Apt Get Update
      apt:
        update_cache: yes
```

#### Download

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name   : Download
      get_url:
        url  : https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
        dest : /usr/bin/wp
```

#### Git Clone

```yml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name      : Clone Oh-My-ZSH
      git       :
        repo    : https://github.com/robbyrussell/oh-my-zsh.git
        dest    : "~/.oh-my-zsh"
```

#### Get output in variable

```yaml
---
- hosts      : 127.0.0.1
  become     : yes
  tasks      :

    - name: Get username
      local_action: command whoami
      register: var_whoami

    - debug: var=var_whoami
```
