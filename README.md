
<h1 align="center">Cap-Ansible</h1>

<b>

Cap-Ansible is a playbook for the easy deployment of Ruby on Rails API along with React application. More Precisely, It is a set of steps and commands we followed to manually set up a server, now being automated with the help of Ansible. 
<br>
Below is the detailed information about this ansible-playbook. 
<br>
Information about specific roles is further mentioned in the respective role directory and also linked below. 
</b>

## What does it exactly do?
 
  *Process mentioned here is chronological. It describes the only procedure of the provision inside of VPS. Tasks are performed by respective roles as mentioned.*

[common]() 
* Install required/useful packages 

[postgresql]() 
* Install postgres and required packages
* Create postgres users
* Create databases
* Allow peer connection 

[ruby]() 
* Detect rvm installer
* Install rvm installer
* Install rvm
* Configure rvm
* Detect if rubies are installed
* Install rubies
* Select default ruby
* Install bundler if not installed 

[nodejs]()
* Add Node source repositories
* Install Nodejs and npm 

[user]() 
* Allow deployment group to have passwordless sudo
* Create a new user with sudo privileges
* Add local key to authorized key for remote user 

[git-ssh]() 
* Ensure git is installed
* Create the release and current folders {TODO}
* Clone git repositories

[deploy_react]() 
* Install dependencies *(npm install)*
* Build react app 

[deploy_rails]() {TODO} 

[nginx]() 
* Install nginx
* Create and symlink configuration for react app
* Set nginx user

## Requirements
* Python 2 (version 2.7) or Python 3 (versions 3.5 and higher) on remote node *Ansible needs these to run!*
* Local user should be ssh-authenticated with remote node. remote user with local user's public key should be set as `ansible_ssh_user`

## Getting Started
Here are the steps that you need to follow in order to get up and running with Ansible Rails.

### 1. Installation
    $ git clone git@bitbucket.org:codysseynepal/cap-ansible.git
    $ cd cap-ansible
    $ git checkout master

### 2. Configuration
Change `inventory.ini.sample` to `inventory.ini`

    $ mv inventory.ini.sample inventory.ini

Replace `<ip_address>` with target machine ip_address.

Replace `<your_ssh_user>` with the remote user by which SSH connection can be established

Replace `<your_deploy_user>` with the remote user you want to perform deploy with. `Make sure you give the same deploy user through-out the variable files.`

Open app-vars.yml and change the following variables. Additionally, please review the app-vars.yml and see if there is anything else that you would like to modify (e.g.: install some other packages, change ruby, node or postgresql versions etc.)
All the variables in `app-vars.yml` are described in [wiki here]()You can adjust them accordingly.

Here is list of required variables. Make sure that they are not empty and are correct.


      rails_app_name: APP_NAME (repo name)
      react_app_name: APP_NAME (repo name)

      # Users and Group
      deploy_user: REMOTE_DEPLOY_USER 

      # postgresql
      postgresql_version: "9.6"

      # Ruby
      rvm_rubies:
        - 'ruby-2.6.0'

      rvm_default_ruby_version: 'ruby-2.6.0' 
      rvm_bundler_version: '1.10.6' # bundler version 

      # Nodejs
      nodejs_version: "12.16.0" 

      # Deploy React
      deploy_branch_react: master

### Deploy

Before deploy, Check:

    $ ssh-add -l

If,    
 
    Could not open a connection to your authentication agent.
Do:
 
    $ eval `ssh-agent`
    $ ssh-add

Now check,
    
    $ ssh-add -l

It should log something like:

    4096 SHA256:7whqRh1YTgyvfP2ViedHfero5t4/kj327j4g5kdfuj/ user@gmail.com (RSA)              │

Now, We're ready to go.


To run the playbook:
    
    cap-ansible$ ansible-playbook -i inventory env_setup. 



### TODO's:
1. Add wiki:
  - Application Variables: Description and options 
      <!-- All the variables can be found in `app-vars.yml`.
      Here is the list, details and options that can be passed. -->
  - Architecture and control flow
  - SSH connections and users
2. Add specific README for all the roles
3. Task for maintaining releases
4. Task for bundle and deploy rails app 
5. Storing sensetive information 
  - Configure ansible-vault
6. Ansible Tower for automated playbook trigger


Please create issues if something problematic is found. Thank You!
