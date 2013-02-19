begin
  load File.dirname(__FILE__) + "/Vagrantfile.local"
rescue LoadError
  raise 'Vagrantfile.local missing. Create it by copying Vagrantfile.local.dist and editing the variables in it.'
end

hostname = "symfony.local"
app_path = "/home/vagrant/symfony"


def Kernel.is_windows
  processor, platform, *rest = RUBY_PLATFORM.split("-")
  platform == "mingw32"
end

Vagrant::Config.run do |config|
  config.vm.box       = "precise32"
  config.vm.box_url   = "http://files.vagrantup.com/precise32.box"
  # config.vm.host_name = "vagrant"

  config.vm.forward_port 80, 8080
  config.vm.forward_port 22, 2222

  # Dedicated IP to avoid conflicts (and no port fowarding!)
  config.vm.network :hostonly, "33.33.33.10"
  config.vm.network :bridged

  # Mount the src folder as NFS for caching & speed
  config.vm.share_folder("v-root", app_path, ".", :nfs => !Kernel.is_windows)

  # Provision with chef
  config.vm.provision :chef_solo do |chef|
    # This path will be expanded relative to the project directory
    chef.cookbooks_path = "app/cookbooks"
    chef.add_recipe("apt")
    chef.add_recipe("ruby::1.9.1")
    chef.add_recipe("git")
    chef.add_recipe("php")
    chef.add_recipe("composer")
    chef.add_recipe("mysql::server")
    chef.add_recipe("mysql::ruby")
    chef.add_recipe("apache2")
    chef.add_recipe("apache2::mod_php5")
    chef.add_recipe("phpmyadmin")
    chef.add_recipe("zsh")
    chef.add_recipe("oh-my-zsh")
    chef.add_recipe("custom")
    chef.json = {
      :hostname => hostname,
      :mysql => {
        :server_debian_password => 'debian',
        :server_root_password => 'root',
        :server_repl_password => 'repl'
      },
      :webapp => {
        :path => app_path,
        :hostname => hostname,
        :database => {
          :user => "symfony",
          :name => "symfony",
          :password => "password"
        }
      },
      :oh_my_zsh => {
        :users => [{
          :login => 'vagrant',
          :theme => 'steeef',
          :plugins => %w(autojump composer debian git git-flow symfony2)
        }]
      },
      :php => { :directives => {
        'date.timezone' => 'Europe/Stockholm',
        'short_open_tag' => 0
      }},
      :git => {
        :name => @git_name,
        :email => @git_email
      }
    }
  end
end
