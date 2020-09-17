# centos7-CIS Ansible Role

This role can be used in an Ansible playbook to harden Centos 7 images to CIS 2.2.0 standards.

## Set Up

1. Make sure vagrant and virtualbox are installed.
```
brew cask install vagrant virtualbox
```

2. Create project folder and change into it before initializing the vagrant project with a Debiam9 base image. This should genertate a `Vagrantfile` and a `.vagrant` directory. You can then test whether the Vagrant project was created by running vagrant up to start the machine.

```
# Create project folder
mkdir -p ~/MyProjects/centos7-test-box
cd ~/MyProjects/centos7-test-box

# Initialize vagrant 
vagrant init centos/7

# Check if VM image was created
vagrant up
vagrant ssh -c "ip a"
vagrant destroy
```
3. Make sure ansible is installed.
```
brew install ansible
```
4. Create an ansible playbook, containing the yaml below.
```
- name: Harden Server
  hosts: all
  become: yes

  roles:
  - centos7-CIS
```
5. Create a `roles` folder within the the project and change into it. Clone this repo into the folder.
```
mkdir roles
cd roles
git clone https://github.com/broadinstitute/dsp-appsec-centos7-hardening-role.git
```
6. Open your Vangrant file and look for the `config.vm.box = "centos/7"` line. Edit the Vagrantfile so it looks like the yaml below.
```
...
  config.vm.box = "centos/7"
  
  # Add the following code
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "[YOUR-ANSIBLE-PLAYBOOK].yml"
  end
...
```
7. To run the role, run `vagrant up`. The ansible playbook will automatically run when VM boots. While the VM is running, you can run `vagrant provision` to re-run the playbook.

Role Name
=========

This role can be used in an ansible playbook to harden a Debian 9 image according to CIS 1.01 standards.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
