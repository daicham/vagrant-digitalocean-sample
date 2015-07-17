# -*- mode: ruby -*-
# vi: set ft=ruby :

Dotenv.load

# change default provider to digital_ocean
ENV['VAGRANT_DEFAULT_PROVIDER'] = "digital_ocean"

# set droplet image name
# if you want to know available image names, please type below.
#   vagrant digitalocean-list images <TOKEN>
IMAGE_NAME = 'centos-7-0-x64'
#IMAGE_NAME = 'coreos-stable'

Vagrant.configure(2) do |config|
  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = '~/.ssh/id_rsa'
    override.vm.box = 'digital_ocean'
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = ENV['PERSONAL_TOKEN']
    provider.image = IMAGE_NAME
    provider.region = 'sgp1'
    provider.size = '512mb' 
    provider.user_data = File.open(File.dirname(__FILE__)+"/cloud-config.#{IMAGE_NAME}.yml").read
  end

  # Settings for running under proxy
  config.ssh.username = 'core' if IMAGE_NAME == 'coreos-stable'
  config.ssh.port = 443
  config.ssh.proxy_command = "\"C:\\Program Files\\git\\bin\\connect.exe\" -H #{ENV['PROXY_HOST']} %h %p"
end
