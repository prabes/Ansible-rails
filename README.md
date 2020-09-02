
# Cap-Ansible

## Contents  _Till Now_

There are3 roles created:

  * Commom
  * Postgresql
  * Ruby

#### Common
  * Install all common packages:
    * git-core  
    * curl
    * tmux
    * htop

#### Postgresql
  * Install postgresql
  * Enable postgresql service
  * Create a postgres user

#### Ruby
  * Install RVM
  * Source RVM scripts
  * Install ruby
  * Set default ruby-version

## Dependencies
  * [rvm1-ansible](https://github.com/rvm/rvm1-ansible) An ansible role to install and manage ruby versions using rvm.

## Running Scripts
  * Clone the repo and checkout to master branch
  * Change `<target_machine_ip>` to your target machine ip
  * Change `<target_machine_user>` to your target machine user by which you like to run the tasks.
  * Run `$ ansible-galaxy install rvm.ruby` 

  To start the tasks, Run:
  >    $ ansible-playbook -i inventoy.ini env_setup.yml

  