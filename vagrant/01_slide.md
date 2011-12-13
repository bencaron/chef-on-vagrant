!SLIDE
# Mais Vagrant, c'est quoi? #

![vagrant](vagrant_chilling.png)

!SLIDE
# De la bouche du cheval:
_Vagrant is a tool for building and distributing virtualized development environments_


!SLIDE bullets incremental
# Vagrant:

* basé sur VirtualBox
* scripter vos VM en Ruby
* facile de partager ses recettes 
* multiplateformes: Linux, OS X, Windows

!SLIDE
# Installation facile

    $ gem install vagrant

!SLIDE commandline incremental
# Session typique:

    $ mkdir monprojet ; cd monprojet
    $ vagrant init
    $ vagrant up
    $ vagrant ssh

!SLIDE incremental
# OK, j'ai triché!
# Manque une étape

!SLIDE
# Les VM n'apparaissent pas par magie.

!SLIDE
# Les VM sont généré à partir d'un template de base

!SLIDE commandline incremental
# L'étape manquante

    $ vagrant box add base http://files.vagrantup.com/lucid32.box
    $ vagrant init
    ...

!SLIDE bullets incremental
# base box

* plusieurs plateforme de base disponibles pré-canné:
 http://www.vagrantbox.es/

* DIY
 * création à la main
 * installation de la configuration requises à la main
 * ...

!SLIDE
# à la main?!?

!SLIDE
# Veewee!

Permet de batir automatiquement ses propres basebox à partir d'une image ISO (ou autre)

https://github.com/jedi4ever/veewee

Va même downloader l'ISO si vous ne l'avez pas sous la main!


!SLIDE smaller
# Contenu du Vagrantfile

    @@@ ruby
    Vagrant::Config.run do |config|
        config.vm.box = "base"
        config.vm.forward_port "http", 80, 8080
        config.vm.share_folder "v-data", 
                     "/vagrant_data", "../data"
    end

!SLIDE
# Port-forwarding facile!

    @@@ ruby
    config.vm.forward_port "http", 80, 8080

!SLIDE
# Travailler en semi-local

Répertoire local exposé par NFS dans la VM:

    @@@ ruby
    config.vm.share_folder "v-data", 
                 "/vagrant_data", "../data"


!SLIDE
# Provisionning!

!SLIDE
# Avec Puppet
    @@@ruby
    config.vm.provision :puppet do |puppet|
        puppet.manifests_path = "manifests"
        puppet.manifest_file  = "base.pp"
    end

!SLIDE smaller
# Avec Chef, mode solo

    @@@ ruby
    config.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "cookbooks"
        chef.add_recipe "mysql"
    end

!SLIDE smaller
# Avec Chef, mode client
    @@@ ruby
    config.vm.provision :chef_client do |chef|
     chef.chef_server_url = "http://mychefserver:4000"
     chef.validation_key_path = "../validation.pem"
     chef.environment = "dev"
     chef.add_role "mytestrole"
    end


!SLIDE
# Mais!

Je ne connais pas Chef!


