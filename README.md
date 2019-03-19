# VmDOCKERCore

How Start API In Ubuntu With Vagrant  and Docker.
Steps

1.- Download Vagrant And VirtualBox
      
      https://www.vagrantup.com/
      https://www.virtualbox.org/

2.- Make a new directory
     Open CMD in directory do you like make a new folder for VM. Run next command 
      
          MKDIR nameFolder
    
       go to nameFolder.
       and run this command 

         vagrant init vagrantImage  in this time i do a VM with Ubuntu/xenial64
         example : "vagrant init Ubuntu/xenial64"

    This command created a new file at directory nameFolder. File name "VagrantFfle"
     In this file is where i configure the VM that will created.

3.- Configure Vagrantfile
      In file can configure some options.
      First option configured is the GUI for haven't troubles when create VM.

          config.vm.provider "virtualbox" do |vb|
             vb.gui = true

      This text come commented, comment line is with #, you have delete # for to  uncomment.
      next configuration is memory and CPU's with next command line
      
          "vb.memory = 2048"  /this line define 2GB ram for this VM.
          "vb.cpus = 1"  /Numbers of pcs that VM will use
          "end" / This line indicate the end of configuration VM virtualbox

      With this first configuration Vagrant will download Image Ubuntu/xenial64
      for start download image run  vagrant up. Allways in directory where is Vagrantfile.

      Before run, there to configure tools/software in VM. This action names VM provisioning
      For provisioning need this command line 

              config.vm.provision "shell", inline: "yourcommand"

In this case needed a Viewer desktop then go to donwoad a desktop viewer xfce4 in                   virtualbox

        config.vm.provision "shell", inline: "sudo apt-get install -y xfce4 virtualbox-guest-dkms       virtualbox-guest-x11"

      Next needed  Net Core 2.2.1
      
           config.vm.provision "shell", inline: " echo --------Installing .net COre--------------"
        config.vm.provision "shell", inline: "wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb" 
          config.vm.provision "shell", inline: "sudo dpkg -i packages-microsoft-prod.deb"
          config.vm.provision "shell", inline: "yes | sudo apt-get install apt-transport-https"
          config.vm.provision "shell", inline: "yes | sudo apt-get update"  
          config.vm.provision "shell", inline: "yes | sudo apt-get install dotnet-sdk-2.2"

       This command lines was provider by microsoft official site

       To install Visual Studio Code

         config.vm.provision "shell", inline: "sudo curl    https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg"   
           config.vm.provision "shell", inline: "yes | sudo apt install snapd"
           config.vm.provision "shell", inline: "yes | sudo snap install vscode --classic"

        Installing DOCKER
            config.vm.provision "shell", inline: "yes | sudo apt-get install  curl  apt-transport-https ca certificates software-properties-common"
            config.vm.provision "shell", inline: "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -"
            config.vm.provision "shell", inline: "sudo apt-key fingerprint 0EBFCD88"
config.vm.provision "shell", inline: "sudo add-apt-repository 'deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable'"
           config.vm.provision "shell", inline: "sudo apt-get update" 
           config.vm.provision "shell", inline: "sudo apt-get install docker-ce"

      Thats Command line was provider by microsoft official

       Now i'm going to install chromium 
             config.vm.provision "shell", inline: "sudo apt-get install chromium-browser"
     
       And now start vagrant 
             vagrant up

      When you VM its started open in VM  new Terminal 
      Check if dotnet , visual studio code and docker installed
        For check dotnet write  in terminal 
          dotnet --version
        Check Docker
           docker --version 
       For check visual studio code 
          This  check is easy just search program in ubuntu.

  4.- Configure DOCKER SQL SERVER UBUNTU

       Now configure sql server for ubuntu in docker
       for make this write in terminal VM; Needed Pull the image sql server ubuntu. 
    
         sudo docker pull microsoft/mssql-server-linux

      With this was created docker image with sql server ubuntu. 
      for run sql server ubuntu write next lines

       docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=yourStrong(!)Password' -p 1433:1433 -d microsoft/mssql-server-linux:latest
      Line configure sql server , password and ports communications and accept EULA 
      
       This line created a container; For saw containers write 
           docker ps 
    
       If container is runnig must appear in list. If not running you can check with next comman line 
            docker ps -a     /this show all containers
        
        for running a container write this
            docker start <container id | container name>

         To connect data base in docker must write 
         docker exec -it <container_id|container_name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <your_password>

          Now can create Database
          Create with transact-SQL 
          CREATE DATABSE XenialDocker
 
          Late create a Table
          CREATE TABLE XenialDocker.dbo.Person (
               Id int IDENTITY (1,1) NOT NULL,
               Name varchar(50) NOT NULL,
             Email varchar(50) NOT NULL
           ) 

         And last insert data in database
     
          INSERT INTO namedatabse.dbo.nametable (columns) values (values columns);
         Don't forget write GO in next line transact-SQL

 




5. Create new WebApi in Ubuntu
   
   To create a new WebAPi in ubuntu write 
        dotnet new webapi  /Web api create in diretory you are

    for run new webapi write 
        dotnet run / This run webApi and you can get access by url with Browser

     with yor configuration access normally must be 
       localhost:5000/api/yourcontroller


      To Install a nuget/package in our project, just type this command in directory where is your project.
       dotnet add package 'name nuget/package'

    And now you get your api in ubuntu with c# and Docker
    
 

Final END
