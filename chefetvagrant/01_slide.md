!SLIDE 
# Vagrant aime Chef

    @@@ruby
    config.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "cookbooks"
        chef.add_recipe "mysql"
        chef.add_role "monapp"
        chef.json = { 
            :mysql_password => "foo"
            }
    end

!SLIDE commandline
# Provisionning intégré

    $ vagrant provision

Mais... Gotcha!

*vagrant provision* 
!=
*vagrant ssh + chef-solo*

!SLIDE bullets incremental
# Allez cuisiner!

Les ingrédients:

* VirtualBox 
* Vagrant
* Chef

!SLIDE
# Questions?
