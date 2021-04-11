# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: <<-SHELL
#GERAL
    echo "127.0.0.1 localhost
    192.168.122.10 appdocker
    192.168.122.11 webapp
    192.168.122.14 ansible
    192.168.122.15 mysql" > /etc/hosts
    mkdir /root/.ssh/
    echo "-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAwtKcLOQ5016KlWHs2/oppDyj7v8nE5/bbDMKdDLNMYTtdE2L
MOp2szLKXJm1SQH2IhSN4ksJIUU6HE6YpcOqVEDCDLu6JWWmOFAJnF0q/4xWX7hD
mXxbb42++qn9ROYhGSgt7PQXIvD1TdjW7rKn1zT3i81LPkmeLK/zKikAOfV1H2b8
XuNYK0+15aD/cFTrKbI2BMkBRDbfKcAvUcigeH5pMJT0vUhE2Xa3AWKsj/bLIqgg
5dM1EvWrA6I5GkcEOHNF2CrtAPf07yUAwkBpLgvAfUfSu3UJaK4qOFJTGwjM8ulh
BBAbAmUCztwbsb/Ji1QZPVb4XMl5OvuSa7i6iQIDAQABAoIBADsmqthOaugsGjOE
yd94MtB0wOk9euXQcVSGorPpALf6PgZDzPELHwMFdr9qw8no2Iw8ZV/BnIIHfL8/
dcVOhRaTmtc24CuekzshwelBuF5ig48IaS3evfw+sy90ETusC3yR4G/DJIstUa1T
Gt7aS29h248Mw72jqGy090VjsXfm8Q1ZyVYWBb1A4PbGGt/Y9CjA1w2b18FAlbI1
5yNwkKRCaeA3ATPaKsUMSsUweurZYVXFOMqNPf632CFq4URfEqOpD6YGg1xf15uS
iZeH147r8lGvdwO8IPwJMxFpfYlb0X8JRn2zlzPkXs9HRCFONI8TTmhPB5pEXAh1
VVrWmWkCgYEA4INdyz1TuwJAFlQeY+HQR+Ppxd01gxGjCSd5PAMtK8yryzOSyuJA
GUryfBdrJVgS+S4RllVS83Z6aJwQSBRPDNM2XQrgsakaKMgU6yushnHyNSFV/4zq
fPEQFcafkND/gOBc4ycytsf72J0UUD/lJ0bJwj6vj494q8z0sLm0TTsCgYEA3iVG
hr2T4zXKP8aHS5WscaQMoNuoUVV9il/kfEHSmMLxB5tfclrsmp9vG2zy0Wj7NRvY
xCdjdL1eOUD10kImS5q2Fi2Fzrhk/VUer0eq0u0MBP7TepLg14yCRqNNB/vzSTSO
OMMHlD/R4cP7/DlK4A7DjAghWc9MJCjEPXn5qwsCgYBsjTehV9KPHeRsp1lWQ81X
pQvXvj/sUm+4slw8tvB1N+1sP1BfRgtl70XU1+HXWYE695pLTI/h5UwEHkkFAMTD
1692Rxci7zcVtr/egOxWyOsp4ydYewK5TDjRvopSE6sl3dUrgz1TANh1AGXc8zfR
yLkucO6jg+P9dQhuFivmFwKBgBdF7HedUOsS7Zd04yPGEITvXOtVV/L9c+OVXEiw
VLHwanQTkRJX+EXSwj8rUN0jlH3h5vnV7pOCa2awKZDXoU92a/Ey37vikaIA0vAm
H/1tHD9Bu0IyNSAf9l4UKbPWb4yR1vyXYinj7ccrUzD/h5qlsVLwXx4bm6yGINkX
+FI1AoGBAIsXas3zGB+nmK+O27w8MNECZ+582uyrisVRlXvj7OhVUlqCvaMJ1Ni4
1FRocKHz5bLKHIOgCCriCAWjYKZB3rdAbD+LTv9dh7G86ILCQeS5jz0hnEB8Chvf
8BYynX2Nc6k7Nv79YYGD+MZwRZK1IaNG0k/Vy+na8orNMMdm7x8w
-----END RSA PRIVATE KEY-----" >> /root/.ssh/id_rsa
    echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDC0pws5DnTXoqVYezb+imkPKPu/ycTn9tsMwp0Ms0xhO10TYsw6nazMspcmbVJAfYiFI3iSwkhRTocTpilw6pUQMIMu7olZaY4UAmcXSr/jFZfuEOZfFtvjb76qf1E5iEZKC3s9Bci8PVN2NbusqfXNPeLzUs+SZ4sr/MqKQA59XUfZvxe41grT7XloP9wVOspsjYEyQFENt8pwC9RyKB4fmkwlPS9SETZdrcBYqyP9ssiqCDl0zUS9asDojkaRwQ4c0XYKu0A9/TvJQDCQGkuC8B9R9K7dQlorio4UlMbCMzy6WEEEBsCZQLO3Buxv8mLVBk9VvhcyXk6+5JruLqJ" >> /root/.ssh/authorized_keys
    chmod 600 /root/.ssh/id_rsa
  SHELL

#APP
  config.vm.define "appdocker" do |appdocker|
    appdocker.vm.hostname = "app"
    appdocker.vm.box = "centos/8"
    appdocker.vm.box_check_update = false
    appdocker.vm.network "private_network", ip: "192.168.122.10", dns: "8.8.8.8"

  appdocker.vm.provision "shell", inline: <<-SHELL
    yum update -y && yum install curl 
    curl -fsSL https://get.docker.com | bash && systemctl enable --now docker
  SHELL

    config.vm.provider "libvirt" do |appdocker|
      appdocker.memory = "1024"
    end
  end

#WEBAPP
  config.vm.define "webapp" do |webapp|
    webapp.vm.hostname = "webapp"
    webapp.vm.box = "centos/8"
    webapp.vm.box_check_update = false
    webapp.vm.network "private_network", ip: "192.168.122.11", dns: "8.8.8.8"

  webapp.vm.provision "shell", inline: <<-SHELL
    yum update -y && yum install curl  
    curl -fsSL https://get.docker.com | bash && systemctl enable --now docker
  SHELL

    config.vm.provider "libvirt" do |webapp|
      webapp.memory = "1024"
    end
  end

#ANSIBLE
  config.vm.define "ansible" do |ansible|
    ansible.vm.hostname = "ansible"
    ansible.vm.box = "centos/8"
    ansible.vm.box_check_update = false
    ansible.vm.network "private_network", ip: "192.168.122.14", dns: "8.8.8.8"

  ansible.vm.provision "shell", inline: <<-SHELL
    yum update -y && yum install curl
    curl -fsSL https://get.docker.com | bash && systemctl enable --now docker
  SHELL

    config.vm.provider "libvirt" do |ansible|
      ansible.memory = "1024"
    end
  end

#DATABASE
  config.vm.define "mysql" do |mysql|
    mysql.vm.hostname = "mysql"
    mysql.vm.box = "centos/8"
    mysql.vm.box_check_update = false
    mysql.vm.network "private_network", ip: "192.168.122.15", dns: "8.8.8.8"

  mysql.vm.provision "shell", inline: <<-SHELL
    yum update -y && yum install curl
    dnf -y install mysql-server && systemctl enable --now mysqld
  SHELL

    config.vm.provider "libvirt" do |mysql|
      mysql.memory = "3064"
    end
  end
end
