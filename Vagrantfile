VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.network 'forwarded_port', guest: 80,  host: 8080
  config.vm.network 'forwarded_port', guest: 443, host: 8443
  
  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize [ 'modifyvm', :id, '--memory', '512' ]
    vb.customize [ 'modifyvm', :id, '--nictype1', 'virtio' ]
    vb.customize [ 'modifyvm', :id, '--natdnshostresolver1', 'on' ]
    vb.customize [ 'modifyvm', :id, '--natdnsproxy1', 'on' ]
  end
      
  config.vm.define 'ubuntu' do |ubuntu|
    ubuntu.vm.box      = 'ubuntu/trusty64'
    ubuntu.vm.hostname = 'ubuntu'
    
    ubuntu.vm.provision 'shell', inline: 'apt-get update'
    ubuntu.vm.provision 'shell', inline: 'apt-get install -y -qq  python-pip'
    ubuntu.vm.provision 'shell', inline: 'pip install ansible jinja2'
    ubuntu.vm.provision 'shell', inline: 'ln -sf /vagrant /ansible-role-elasticsearch'

    ubuntu.vm.provision 'ansible' do |ansible| 
      ansible.playbook = 'tests/test_vagrant.yml'
    end
    
  end

end
  
# vi:ts=2:sw=2:et:ft=ruby:
