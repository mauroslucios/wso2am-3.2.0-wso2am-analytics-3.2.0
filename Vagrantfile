Vagrant.configure("2") do |config|
  #config.vm.box = "bento/ubuntu-20.10"
  #config.vm.box = "centos/7"
  config.vm.box = "bento/centos-7"
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "4096"
  end
  $script = <<-SCRIPT
  sudo iptables -I INPUT -p tcp --dport 9443 -j ACCEPT
  sudo iptables -I INPUT -p tcp --dport 9643 -j ACCEPT
  SCRIPT

  config.vm.define "wso2" do |wso2|
    wso2.vm.network "public_network", ip: "192.168.0.51"
    wso2.vm.network "forwarded_port", guest: 8089, host: 8089
    wso2.vm.synced_folder "./data", "/data"
    wso2.vm.synced_folder ".", "/vagrant", disabled:true

    wso2.vm.provision "shell", inline: "yum update -y && yum install -y git && yum install -y wget && yum install -y curl && \
    yum install -y nano"
    wso2.vm.provision "shell", inline: "yum install -y  java-11-openjdk-devel"
    wso2.vm.provision "shell", inline: "echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.11.0.9-1.el7_9.x86_64' >> /etc/profile"
    wso2.vm.provision "shell", inline: "echo 'export PATH=${JAVA_HOME}/bin:${PATH}' >> /etc/profile"
    wso2.vm.provision "shell", inline: "source /etc/profile"
    wso2.vm.provision "shell", inline: "cp -R /data /home/vagrant"
    wso2.vm.provision "shell", inline: "chown -R vagrant:vagrant /home/vagrant/data"

    wso2.vm.provision "shell", inline: "mkdir /opt/wso2"
    wso2.vm.provision "shell", inline: "chown -R vagrant:vagrant /opt/wso2"

    wso2.vm.provision "shell", inline: "cp -R /data/wso2am-3.2.0 /opt/wso2"
    wso2.vm.provision "shell", inline: "chown -R vagrant:vagrant /opt/wso2/wso2am-3.2.0"
    wso2.vm.provision "shell", inline: "chmod +x /opt/wso2/wso2am-3.2.0/bin/wso2server.sh"

    wso2.vm.provision "shell", inline: "cp -R /data/wso2am-analytics-3.2.0 /opt/wso2"
    wso2.vm.provision "shell", inline: "chown -R vagrant:vagrant /opt/wso2/wso2am-analytics-3.2.0"
    wso2.vm.provision "shell", inline: "chmod +x /opt/wso2/wso2am-analytics-3.2.0/bin/worker.sh"
    wso2.vm.provision "shell", inline: "chmod +x /opt/wso2/wso2am-analytics-3.2.0/bin/dashboard.sh"

    wso2.vm.provision "shell", inline: $script

    wso2.vm.provision "shell", inline: "cp -R /data/wso2ApimWso2Server.service /etc/systemd/system/"
    wso2.vm.provision "shell", inline: "chmod +x /etc/systemd/system/wso2ApimWso2Server.service"
    wso2.vm.provision "shell", inline: "systemctl enable wso2ApimWso2Server.service"
    wso2.vm.provision "shell", inline: "systemctl daemon-reload"
    wso2.vm.provision "shell", inline: "service wso2ApimWso2Server start"

    wso2.vm.provision "shell", inline: "cp -R /data/wso2ApimDashboard.service /etc/systemd/system/"
    wso2.vm.provision "shell", inline: "chmod +x /etc/systemd/system/wso2ApimDashboard.service"
    wso2.vm.provision "shell", inline: "systemctl enable wso2ApimDashboard.service"
    wso2.vm.provision "shell", inline: "systemctl daemon-reload"
    wso2.vm.provision "shell", inline: "service wso2ApimDashboard start"

    wso2.vm.provision "shell", inline: "cp -R /data/wso2ApimWorker.service /etc/systemd/system/"
    wso2.vm.provision "shell", inline: "chmod +x /etc/systemd/system/wso2ApimWorker.service"
    wso2.vm.provision "shell", inline: "systemctl enable wso2ApimWorker.service"
    wso2.vm.provision "shell", inline: "systemctl daemon-reload"
    wso2.vm.provision "shell", inline: "service wso2ApimWorker start"
    #wso2.vm.provision "shell", inline: "cd /home/vagrant/data && dpkg -i wso2am-linux-installer-x64-3.2.0.deb"

  end
end
