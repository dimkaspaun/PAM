# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = 'centos/8'
#  config.vm.box_url = 'https://cloud.centos.org/centos/8/vagrant/x86_64/images/CentOS-8-Vagrant-8.4.2105-20210603.0.x86_64.vagrant-virtualbox.box'
  config.vm.box_download_checksum = 'dfe4a34e59eb3056a6fe67625454c3607cbc52ae941aeba0498c29ee7cb9ac22'
  config.vm.box_download_checksum_type = 'sha256'

  config.vm.synced_folder ".", "/vagrant"
  
  config.vm.define "PAM" do |box|
  

    box.vm.host_name = "PAM"

    box.vm.provider "virtualbox" do |vb|
      vb.cpus = 2      
      vb.memory = 1024
    end
 
    box.vm.provision "shell", inline: <<-SHELL
      for pkg in epel-release pam_script; do yum install -y $pkg; done
      sed -i 's/^PasswordAuthentication.*/PasswordAuthentication yes/' /etc/ssh/sshd_config
      systemctl restart sshd
      groupadd admin
      useradd -G admin test_admin
      echo "test_admin" | passwd --stdin test_admin
      sed -i '/pam_nologin\.so$/a account    required     pam_exec.so \/usr\/local\/bin\/pam_script\.sh' /etc/pam.d/sshd
      cp /vagrant/pam_script.sh /usr/local/bin/
      chmod +x /usr/local/bin/pam_script.sh

    SHELL
  end  
end
