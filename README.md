# Jayson's Mac Ansible Playbook

[![Build Status](https://travis-ci.org/jayson/jayson-mac-ansible.svg?branch=master)](https://travis-ci.org/jayson/jayson-mac-ansible)

This playbook installs all my homebrew apps and configurations for me instead
of manually configuring every new laptop I get.

*See Also*
  - Forked from [mac-dev-playbook](https://github.com/geerlingguy/mac-dev-playbook) by [Jeff Geerling](http://www.jeffgeerling.com/)

## Installation

  1. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  2. [Install Ansible](http://docs.ansible.com/intro_installation.html).
  3. Clone this repository to your local drive.
  4. Run `$ ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
  5. Run `ansible-playbook main.yml -i inventory -K` inside this directory. Enter your account password when prompted.

> Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

### Running a specific set of tagged tasks

You can filter which part of the provisioning process to run by specifying a set of tags using `ansible-playbook`'s `--tags` flag. The tags available are `dotfiles`, `homebrew`, `mas`, `extra-packages` and `osx`.

    ansible-playbook main.yml -i inventory -K --tags "dotfiles,homebrew"

## Overriding Defaults

Not everyone's development environment and preferred software configuration is the same.

You can override any of the defaults configured in `default.config.yml` by creating a `config.yml` file and setting the overrides in that file. For example, you can customize the installed packages and apps with something like:

    homebrew_installed_packages:
      - cowsay
      - git
      - go

    mas_installed_apps:
      - { id: 443987910, name: "1Password" }
      - { id: 498486288, name: "Quick Resizer" }
      - { id: 557168941, name: "Tweetbot" }
      - { id: 497799835, name: "Xcode" }

    composer_packages:
      - name: hirak/prestissimo
      - name: drush/drush
        version: '^8.1'

    gem_packages:
      - name: bundler
        state: latest

    npm_packages:
      - name: webpack

    pip_packages:
      - name: mkdocs

Any variable can be overridden in `config.yml`; see the supporting roles' documentation for a complete list of available variables.

## Included Applications / Configuration (Default)

Applications (installed with Homebrew Cask):

  - [Docker](https://www.docker.com/)
  - [Alfred](https://www.alfredapp.com/)
  - [Google Chrome](https://www.google.com/chrome/)
  - [Homebrew](http://brew.sh/)
  - [Slack](https://slack.com/)
  - [Vagrant](https://www.vagrantup.com/)
  - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Packages (installed with Homebrew):

  - cfssl
  - ctags
  - fzf
  - git
  - kubernetes-cli
  - mas
  - node
  - rbenv
  - readline
  - ruby
  - the_silver_searcher
  - vim
  - watch
  - wget

My [dotfiles](https://github.com/jayson/dotfiles) are also installed into the current user's home directory. You can disable dotfiles management by setting `configure_dotfiles: no` in your configuration.

## Future additions

### Configuration to be added:

  - I need to finish dotfiles setup and vim configuration

## Testing the Playbook

  You can follow the instructions here to create a [Mac OS X VirtualBox VM](https://github.com/geerlingguy/mac-osx-virtualbox-vm) for testing your playbook changes

This project is [continuously tested on Travis CI's macOS infrastructure](https://travis-ci.org/jayson/jayson-mac-ansible).

## Author

  [Jayon Paul](http://www.jaysonmpaul.com/), 2017 (originally forked from [mac-dev-playbook](https://github.com/geerlingguy/mac-dev-playbook) by [Jeff Geerling](http://www.jeffgeerling.com/))
