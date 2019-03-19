# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.boot_timeout=60
    config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = 2048
     vb.cpus = 1
   end
   
   # Install viewer desktop
    config.vm.provision "shell", inline: " echo --------Installing viewer desktop - Upgrading--------------"
    config.vm.provision "shell", inline: " sudo apt-get -y update && sudo apt-get -y dist-upgrade"
    config.vm.provision "shell", inline: "sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-x11"

   # Installing .net core 2.2
    config.vm.provision "shell", inline: " echo --------Installing .net COre--------------"
    config.vm.provision "shell", inline: "wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb"
    config.vm.provision "shell", inline: "sudo dpkg -i packages-microsoft-prod.deb"
    config.vm.provision "shell", inline: "yes | sudo apt-get install apt-transport-https"
    config.vm.provision "shell", inline: " echo --------Installing .net COre --  UPDATE--------------"
    config.vm.provision "shell", inline: "yes | sudo apt-get update"  
    config.vm.provision "shell", inline: " echo --------Installing .net COre --  INSTALLING--------------"
    config.vm.provision "shell", inline: "yes | sudo apt-get install dotnet-sdk-2.2"

    config.vm.provision "shell", inline: "sudo curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg"   
    config.vm.provision "shell", inline: "yes | sudo apt install snapd"
    config.vm.provision "shell", inline: "yes | sudo snap install vscode --classic"
     
   # Installing Docker

    config.vm.provision "shell", inline: " sudo apt-get -y install  curl  apt-transport-https ca-certificates software-properties-common"
    config.vm.provision "shell", inline: "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -"
    config.vm.provision "shell", inline: "sudo apt-key fingerprint 0EBFCD88"
    config.vm.provision "shell", inline: "sudo add-apt-repository 'deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable'"
    config.vm.provision "shell", inline: "sudo apt-get -y update" 
    config.vm.provision "shell", inline: "sudo apt-get -y install docker-ce"


   # install chromium browser
    config.vm.provision "shell", inline: "sudo apt-get -y install chromium-browser"
    config.vm.provision "shell", inline: "echo hacer un vagrant reload cuando finalice todo para entrar modo grafico en VM escribir startx"

   # for install a docker linux sqlserver you have put this in virtual machine
   # sudo docker pull microsoft/mssql-server-linux

   # Con esto se creara un docker con el servicio sql server instalado luego para arrancar en sql server se ha de poner lo siguiente
   
   #sudo  docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=yourStrong(!)Password' -p 1433:1433 -d microsoft/mssql-server-linux:latest
   # es una linea de configuracion de sqll server para registrar un password y puertos .
   
   # luego para conectarse a la base de datos se ha de poner la siguiente linea
   # docker exec -it <container_id|container_name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <your_password>
   # y una vez dentro de SQL se pueden crear las bases de datos y las tablas.
   # vamos a proceder a instalar FLYWAY
   # config.vm.provision "shell", inline: "wget -qO- https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/5.2.4/flyway-commandline-5.2.4-linux-x64.tar.gz | tar xvz && sudo ln -s `pwd`/flyway-5.2.4/flyway /usr/local/bin"    
   # Ahora que tenemos flyway vamos a configurar la base de datos de docker
   # Creamos la database 


end



