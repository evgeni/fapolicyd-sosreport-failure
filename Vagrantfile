Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "quadlet" do |override|
    override.vm.box = "centos/stream9"
    override.vm.hostname = "quadlet.example.com"

    override.vm.provider "libvirt" do |libvirt, provider|
      libvirt.memory = 10240
      libvirt.cpus = 4
    end
  end
end
