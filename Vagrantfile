# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.ssh.username = "root"
  config.ssh.password = "freenas"
  config.ssh.shell = "sh"
  config.ssh.sudo_command = "%c"

  config.vm.box = "freenas/11.1u6x64"
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  config.vm.guest = :freebsd

  config.vm.hostname = "freenas.local"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network", bridge: [
    "en0: Wi-Fi (AirPort)",
    "wlx503eaa4f3a9f",
  ], :mac => "080027F33A55"

  config.vm.provider "virtualbox" do |vb|
    # Don't display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "1024"

    # Add SATA Controller
    vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata']

    # Create disk
    file_to_disk = 'disk-ada1-tank.vdi'
    unless File.exist?(file_to_disk)
      # 100 * 1024 = 100 GB
      vb.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
    end

    # Attach disk
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]

  end

  # Disable the default /vagrant share
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "/userdata/data/freenas", "/tank/freenas"

end
