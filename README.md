# Ansible Playbook

Run


```bash
# ansible-playbook -i {FILE} -l {ALIAS} playbook.yml

$ ansible-playbook -i hosts -l digital-ocean playbook.yml
```

### Host file

The host file works with ```./ssh/config``` file

-----

# Ansible Resipes
## Run in localhost


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
    - name      : Install Git
      apt       :
        pkg     : git
        state   : latest
```

#### Create File

```yml
    - name      : Create File
      file      :
        path    : "~/thisfile.txt"
        state   : touch
        mode    : 0644
```

#### Create Folder

```yml
    - name      : Create Folder
      file      :
        path    : "~/Documents/custom/folder"
        state   : directory
        recurse : yes
```

#### Remove Folders

```yml
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
    - name   : Make File Executable
      file:
        path: /usr/bin/file
        mode: "u+rwx,g+rx,o+rx"
```

#### Apt Get Update

```yml
---
    - name   : Apt Get Update
      apt:
        update_cache: yes
```

#### Download

```yml
    - name   : Download
      get_url:
        url  : https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
        dest : /usr/bin/wp
```

#### Git Clone

```yml
    - name      : Clone Oh-My-ZSH
      git       :
        repo    : https://github.com/robbyrussell/oh-my-zsh.git
        dest    : "~/.oh-my-zsh"
```

#### Get output in variable

```yaml
    - name: Get username
      local_action: command whoami
      register: var_whoami

    - debug: var=var_whoami
```
