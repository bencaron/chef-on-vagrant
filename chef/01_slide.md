!SLIDE bullets incremental
# Chef, vu de 10 000 pieds

* Configuration Management
* Gestion de _recipes_ dans des _cookbooks_: vous êtes un chef

!SLIDE 
# Deux façons typique de l'utiliser

!SLIDE 
# chef-server: un serveur central

* votre inventaire de nodes, cookbooks, data bags
* gestion de clients, roles, environnements
* le tout indexé, recherchable

!SLIDE
# Disponible de deux façon:

* hébergé par Opscode
* roll-your-own

!SLIDE
# Puissant... mais complexe

* nécessite un serveur
* pas nécessaire pour se familiariser avec Chef

!SLIDE
# L'autre façon d'utiliser Chef: chef-solo

* exécution locale, détaché de cookbooks Chef

!SLIDE
# chef-solo

* Les cookbooks, juste les cookbooks
* pas de données indexés
* pas de data bag

!SLIDE
* Suffisant pour pleins d'usages
* Parfait pour travailler avec Vagrant!

!SLIDE
# Chef, crash-course

!SLIDE commandline
# Installation

Client seulement, rien de plus simple:

    $ gem install chef

!SLIDE
# unité de base: le cookbook

!SLIDE smaller commandline
# Contenu de base

    $ ls test-cookbook/
    attributes   files      metadata.rb  README.rdoc  resources
    definitions  libraries  providers    recipes      templates

!SLIDE small commandline
# minimum minimal minimaliste

    $ ls
    metadata.rb  README.rdoc  recipes/
    $ ls recipes/
    default.rb

!SLIDE smaller
# metadata.rb

    @@@ ruby
    maintainer       "Your name"
    maintainer_email "your.email@exemple.com"
    license          "Apache v2.0"
    description      "Installs/Configures a simple cookbook"
    long_description IO.read(File.join(File.dirname(__FILE__), 'README.rdoc'))
    version          "0.0.1"
    depends "apache2", "> 1.0"

!SLIDE bullets
# README.rdoc

* Votre documentation "longue"
* Info typique... et importante!

= DESCRIPTION:

= REQUIREMENTS:

= ATTRIBUTES:

= USAGE:

!SLIDE
# recipes/default.rb

C'est là que se passe les vrais affaires

!SLIDE
# mais par défaut...

    @@@ruby
    #
    # Cookbook Name:: simple-cookbook
    # Recipe:: default
    #
    # Copyright 2011, You
    #
    # Your License
    #

!SLIDE
# Cuisiner, je veux bien, mais...

!SLIDE bullets incremental
# Principe de base avec Chef

* convergence
* resources

!SLIDE bullets incremental
# Qu'est-ce qu'une resource?

* Quelque chose à gérer:
* process, packages, usagers
* Pleins de resources providers:
    http://wiki.opscode.com/display/chef/Resources
* Facile de faire les votre (comme LWRP)

!SLIDE bullets
# Quel genre de resource?

* un serveur web
* une base de données
* du code
* ...

!SLIDE smaller
# Premier jet: gérer des dépendances

    @@@ruby
    package "vim" do
        action :install
    end

!SLIDE smaller
# gérer des répertoires

    directory "/tmp/monapp" do
      owner "root"
      group "root"
      mode "0755"
      action :create
    end

!SLIDE
# Pleins de resources:

* File, Directory, Link
* User, Group
* Env, Cron, 
* Deploy, Subversion, Git

!SLIDE 
# Un exemple simple

Pratique avec Vagrant:

installer l'environnement nécessaire pour développer une application web


!SLIDE smaller
# un service web
    @@@ruby
    include_recipe "apache2"
    include_recipe "php::php5"
    
    apache_site "monserveur.conf" do
      enable :true
    end

!SLIDE
Good Artists Copy, Great Artists Steal

!SLIDE

Des tonnes de cookbooks!
Trouvez le bon:

http://community.opscode.com/


