# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|

  config.vm.box = "opscode-ubuntu"
  
  config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.2.0.box"
  
  config.vm.forward_port 3000, 3000 # Rails
  config.vm.forward_port 4567, 4567 # Sinatra
  config.vm.forward_port 8080, 8080 # Rack
  
  config.vm.share_folder "app", "/home/vagrant/app", "app/", :create => true
  
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks", "vendor"]
    chef.add_recipe "apt"
    chef.add_recipe "ruby_build"
    chef.add_recipe "rbenv::user_install"
    chef.add_recipe "rbenv::vagrant"
    chef.add_recipe "git"
    chef.add_recipe "nodejs::npm"
    chef.add_recipe "redisio::install"
    chef.add_recipe "redisio::enable"
    chef.add_recipe "postgresql::server"
    chef.add_recipe "postgis"
    chef.add_recipe "imagemagick"
    chef.add_recipe "vim"
    chef.add_recipe "rails-lastmile"

    chef.json = {
      'rvm' => {
        'default_ruby' => 'ruby-1.9.3-p194',
        'gem_package' => {
          'rvm_string' => 'ruby-1.9.3-p194'
        }
      },
      'rbenv' => {
        'user_installs' => [
          { 'user' => 'vagrant' }
        ]
      },
      'postgresql' => {
        'password' => {
          'postgres' => 'postgres'
        }
      }
    }
  end

end
