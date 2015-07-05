# I Am DevOps
## (And So Can You!)

![](img/stephen-colbert.jpg)

---

# About Me

![right,filtered](img/Me.jpg)

### Software Engineer @ IBM
### Continuous Delivery, SmartCloud Notes
### [www.nerdaga.in](http://www.nerdaga.in)
### ![inline](img/Twitter.png) [ImDarinEgan](https://twitter.com/ImDarinEgan)

---

# TL;DR

![fit](img/sticky.png) 

## Vagrant
### omnibus, cachier, berkshelf
## Chef Development Kit (ChefDK)
### Berkshelf
## Packer

---

# Definition of DevOps

![right,filtered](img/chefconf-2015-logo.png)

Chef Style DevOps Kung Fu
[https://github.com/chef/devops-kungfu](https://github.com/chef/devops-kungfu)

> "A cultural and professional movement, focused on how we build and operate high velocity organizations, born from the experiences of the it's practitioners."
-- Adam Jacob - ChefConf 2015 Keynote

---

# Infrastructure Is Code, And All Code Goes Through The Same Workflow

![](img/application.jpg)

* Applications Are Code
* Infrastructure Is Code
* All Code Goes Through The Same Workflow

---

# Culture
# Process
# Tools

![left](img/hashicorp-logo.jpg)
![right,fit](img/opscode-logo.png)

---

![inline](img/hashicorp-logo.jpg)

# Hashicorp

## Vagrant
## Packer
## Consul
## Atlas

---

![inline](img/opscode-logo.png)

# Opscode

## Chef

---

# Vagrant

![fit](img/vagrant.png)

## Create and configure lightweight, reproducible, and portable development environments.

### [https://www.vagrantup.com](https://www.vagrantup.com)

> In a world with Vagrant, developers can check out any repository from version control, run vagrant up, and have a fully running development environment without any human interaction.
-- [The Tao of Vagrant](http://mitchellh.com/the-tao-of-vagrant)

---

# vagrant init

![fit](img/vagrant.png)

```bash
$> vagrant init chef/ubuntu-14.04
```

A Vagrantfile has been placed in this directory. You are now ready to vagrant up your first virtual environment! Please read the comments in the Vagrantfile as well as documentation on vagrantup.com for more information on using Vagrant.

```ruby
Vagrant.configure(2) do |config|
  config.vm.box = "chef/ubuntu-14.04"
end
```

---

# vagrant <up | status | ssh | destroy>

![fit](img/vagrant.png)

```bash
$> vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'chef/ubuntu-14.04'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'chef/ubuntu-14.04' is up to date...
==> default: Setting the name of the VM: chefubuntu-1404_default_1435402982259_46392
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 => 2222 (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /Users/darin/samples/chef.ubuntu-14.04
```

---

# Chef Development Kit (ChefDK)

![fit](img/opscode-logo.png)

> Chef Development Kit (ChefDK) brings Chef and the development tools developed by the Chef Community together and acts as the consistent interface to this awesomeness.
-- [https://downloads.chef.io/chef-dk](https://downloads.chef.io/chef-dk)

This awesomeness is composed of:
[Chef](https://github.com/chef/chef), [Berkshelf](http://berkshelf.com), [Test Kitchen](http://kitchen.ci), [ChefSpec](http://sethvargo.github.io/chefspec), [Foodcritic](http://www.foodcritic.io)

For even more awesomeness, check out:

[tailor](https://github.com/turboladen/tailor) and [RuboCop](https://github.com/bbatsov/rubocop)

---

# vagrant-omnibus

![fit](img/vagrant.png)

### A Vagrant plugin that ensures the desired version of Chef is installed via the platform-specific Omnibus packages.

### [https://github.com/chef/vagrant-omnibus](https://github.com/chef/vagrant-omnibus)

```bash
$> vagrant plugin install vagrant-omnibus
```

```ruby
if Vagrant.has_plugin?("vagrant-omnibus")
    config.omnibus.chef_version = :latest
end
```

---

# vagrant-cachier

![fit](img/vagrant.png)

### A Vagrant plugin that reduces the time for boxes to be provisioned by sharing a common package cache among similar instances, targeting multiple package managers and distros.

### [https://github.com/fgrehm/vagrant-cachier](https://github.com/fgrehm/vagrant-cachier)

```bash
$> vagrant plugin install vagrant-cachier
```

```ruby
if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
end
```

---

# Berkshelf

![right,fit](img/berks.jpg)

Manage a Cookbook or an Application's Cookbook dependencies.

[http://berkshelf.com](http://berkshelf.com)

The Berkshelf contains the installed cookbooks and their dependencies.

Dependencies are managed via the file `Berksfile`. 

For more, see [The Berkshelf Way](https://www.chef.io/blog/chefconf-talks/the-berkshelf-way-jamie-winsor)

Berkshelf is now included as part of the ChefDK. This is the fastest, easiest and recommended installation method.

---

# berks <cookbook | init | package | vendor>

![](img/berks.jpg)

```bash
$> berks cookbook NAME
.
├── recipes/
│   └── default.rb
├── .kitchen.yml
├── .rubocop.yml
├── .rubocop_todo.yml
├── .tailor
├── Berksfile
├── CHANGELOG.md
├── Gemfile
├── LICENSE
├── README.md
├── Thorfile
├── Vagrantfile
├── chefignore
└── metadata.rb
```

---

# vagrant-berkshelf

![fit](img/vagrant.png)

### A Vagrant plugin that adds Berkshelf integration to the Chef provisioners. Vagrant Berkshelf will automatically download and install cookbooks onto the Vagrant Virtual Machine.

### [https://github.com/berkshelf/vagrant-berkshelf](https://github.com/berkshelf/vagrant-berkshelf)

```bash
$> vagrant plugin install vagrant-berkshelf
```

```ruby
if Vagrant.has_plugin?("vagrant-berkshelf")
    config.berkshelf.enabled = true
end
```

---

# Tao of Vagrant - Create Target

![](img/berks.jpg)

```bash
Bringing machine 'default' up with 'virtualbox' provider...
    default: The Berkshelf shelf is at "/Users/darin/.berkshelf/vagrant-berkshelf/shelves/..."
==> default: Sharing cookbooks with VM
==> default: Importing base box 'chef/ubuntu-14.04'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'chef/ubuntu-14.04' is up to date...
==> default: Setting the name of the VM: berkscookbookfoo_default_1436020179873_34644
==> default: Updating Vagrants Berkshelf...
==> default: Resolving cookbook dependencies...
==> default: Fetching 'berks.cookbook.foo' from source at .
==> default: Using berks.cookbook.foo (0.1.0) from source at .
==> default: Vendoring berks.cookbook.foo (0.1.0) to
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 => 2222 (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Mounting shared folders...
    default: /vagrant => /Users/darin/i-am-devops-and-so-can-you/samples/berks.cookbook.foo
    default: /tmp/vagrant-cache => /Users/darin/i-am-devops-and-so-can-you/samples/berks.cookbook.foo/.vagrant/machines/default/cache
    default: /tmp/vagrant-chef/.../cookbooks => /Users/darin/.berkshelf/vagrant-berkshelf/shelves/...
```

---

# Tao of Vagrant - Install Provisioners

![](img/berks.jpg)

```bash
==> default: Installing Chef 12.4.0 Omnibus package...
==> default: Downloading Chef 12.4.0 for ubuntu...
==> default: downloading https://www.getchef.com/chef/metadata?v=12.4.0&prerelease=false&nightlies=false&p=ubuntu&pv=14.04&m=x86_64
==> default:   to file /tmp/install.sh.1636/metadata.txt
==> default: trying wget...
==> default: url    https://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/10.04/x86_64/chef_12.4.0-1_amd64.deb
==> default: md5    630a8752be2cb45c69b7880adb2340f1
==> default: sha256 2d66c27884658f851d43cec850b4951b4d540492be521ae16f6941be80e8b1e6
==> default: downloaded metadata file looks valid...
==> default: /tmp/vagrant-cache/vagrant_omnibus/chef_12.4.0-1_amd64.deb already exists, verifiying checksum...
==> default: Comparing checksum with sha256sum...
==> default: checksum compare succeeded, using existing file!
==> default: Installing Chef 12.4.0
==> default: installing with dpkg...
==> default: Selecting previously unselected package chef.
==> default: (Reading database ... 32400 files and directories currently installed.)
==> default: Preparing to unpack .../chef_12.4.0-1_amd64.deb ...
==> default: Unpacking chef (12.4.0-1) ...
==> default: Setting up chef (12.4.0-1) ...
==> default: Thank you for installing Chef!
```

---

# Tao of Vagrant - Provision Target

![](img/berks.jpg)

```bash
==> default: Running provisioner: chef_zero...
==> default: Detected Chef (latest) is already installed
Generating chef JSON and uploading...
==> default: Running chef-zero...
==> default: stdin: is not a tty
==> default: [2015-07-04T14:30:28+00:00] INFO: Started chef-zero at chefzero://localhost:8889 with repository at /tmp/vagrant-chef/...
==> default:   One version per cookbook
==> default: [2015-07-04T14:30:28+00:00] INFO: Forking chef instance to converge...
==> default: [2015-07-04T14:30:28+00:00] INFO: *** Chef 12.4.0 ***
==> default: [2015-07-04T14:30:28+00:00] INFO: Chef-client pid: 1785
==> default: [2015-07-04T14:30:32+00:00] INFO: Setting the run_list to ["recipe[berks.cookbook.foo::default]"] from CLI options
==> default: [2015-07-04T14:30:32+00:00] INFO: Run List is [recipe[berks.cookbook.foo::default]]
==> default: [2015-07-04T14:30:32+00:00] INFO: Run List expands to [berks.cookbook.foo::default]
==> default: [2015-07-04T14:30:32+00:00] INFO: Starting Chef Run for berks.cookbook.foo-berkshelf
==> default: [2015-07-04T14:30:32+00:00] INFO: Running start handlers
==> default: [2015-07-04T14:30:32+00:00] INFO: Start handlers complete.
==> default: [2015-07-04T14:30:32+00:00] INFO: berks.cookbook.foo Success
==> default: [2015-07-04T14:30:32+00:00] INFO: Chef Run complete in 0.060590805 seconds
==> default: [2015-07-04T14:30:32+00:00] INFO: Skipping removal of unused files from the cache
==> default: [2015-07-04T14:30:32+00:00] INFO: Running report handlers
==> default: [2015-07-04T14:30:32+00:00] INFO: Report handlers complete
```

---

# Vagrant Boxes

![fit](img/vagrant.png)

Boxes are the package format for Vagrant environments. A box can be used by anyone on any platform that Vagrant supports to bring up an identical working environment.

```bash
$> vagrant <init | box add> USER/BOX
```

_e.g._ `chef/ubuntu-14.04`

```ruby
Vagrant.configure(2) do |config|
  config.vm.box = "chef/ubuntu-14.04"
end
```

---

# Packer

![fit](img/packer.png)

### Packer is an open source tool for creating identical machine images for multiple platforms from a single source configuration.

### [https://packer.io](https://packer.io)

### Templates are JSON files that configure the various components of Packer in order to create one or more machine images.

```javascript
"builders": [],
"provisioners": [],
"post-processors": [{
  "output": "builds/{{user `box_basename`}}.{{.Provider}}.box",
  "type": "vagrant"}]
```

---

# Bento

![left,filtered,fit](img/packer.png)

## Modularized Packer definitions for building Vagrant baseboxes

> Bento is a project that encapsulates Packer templates for building Vagrant baseboxes. These boxes are used internally at Chef Software, Inc. for testing Hosted Chef, Chef Server and open source cookbooks via test-kitchen.
-- [http://chef.github.io/bento](http://chef.github.io/bento)

---

# Bento chef/ubuntu-14.04

![fit](img/packer.png)

```bash
$> packer build ubuntu-14.04-amd64.json 

/Users/darin/.vagrant.d/boxes/chef-VAGRANTSLASH-ubuntu-14.04
├── 1.0.0/
│   └── virtualbox/
│       ├── Vagrantfile
│       ├── box.ovf
│       ├── metadata.json
│       └── packer-ubuntu-14.04-amd64-disk1.vmdk
└── metadata_url
```

---

# Boxcutter

![left,filtered,fit](img/packer.png)

Community-driven templates and tools for creating cloud, virtual machines, containers and metal operating system environments

## Packer templates for Windows

> This repository contains templates for Windows that can create Vagrant boxes using Packer.
-- [https://github.com/boxcutter/windows](https://github.com/boxcutter/windows)

---

# Q & A

![right,fit](img/i-am-devops-and-so-can-you.jpg)

### ![inline](img/Twitter.png) [ImDarinEgan](https://twitter.com/ImDarinEgan)
