Vagrant.configure("2") do |config|
  # Betriebssystem der VM
  config.vm.box = "bento/ubuntu-22.04"
  # Hostname der VM
  config.vm.hostname = "dyli-server"
  # privates Netzwerk mit statischer IP-Adresse: '192.168.50.7'
  config.vm.network "private_network", ip: "192.168.50.7"
  # VM lauscht auf Port 80 und leitet diesen auf Port 8080 weiter
  config.vm.network "forwarded_port", guest: 80, host: 8080
  # VM lauscht auf Port 80 und leitet diesen auf Port 8080 weiter
  config.vm.network "forwarded_port", guest: 3306, host: 8081

    config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     # vb.gui = true

    # Customize the amount of memory on the VM:
    # Einstellungen der VM (Arbeitsspeicher, Prozessorkerne, Name)
     vb.memory = "4096"
     vb.cpus = 2
     vb.name = "Dyli-Webseiten-Software"
  end
  config.vm.provision "shell", inline: <<-SHELL
  # Aktualisierung der Paketquellen
  sudo apt-get update -y
  # Aktualisierung des Systems und installierter Pakete
  sudo apt update && sudo apt upgrade -y
  # Installierung der Pakete 'apache2', 'nginx', 'php'
  sudo apt-get install wget curl gnupg2 nano apache2 libapache2-mod-php nginx php-fpm -y
  # Erstellen des Ordners 'dyli-Webseiten-Software' im Verzeichnis '/var/www/'
  sudo mkdir /var/www/dyli-Webseiten-Software

  # Kopieren der Datei 'favicon.ico' aus dem Verzeichnis '/vagrant/Assets/' in dem Ordner '/var/www/dyli-Webseiten-Software/Assets/'
  cp /vagrant/Assets/favicon.ico /var/www/dyli-Webseiten-Software/Assets/
  # Kopieren der Datei 'Bewerbungsfoto.jpeg' aus dem Verzeichnis '/vagrant/Assets/' in dem Ordner '/var/www/dyli-Webseiten-Software/Assets/'
  cp /vagrant/Assets/Bewerbungsfoto.jpeg /var/www/dyli-Webseiten-Software/Assets/
  # Kopieren der Datei 'Logo.png' aus dem Verzeichnis '/vagrant/Assets/' in dem Ordner '/var/www/dyli-Webseiten-Software/Assets/'
  cp /vagrant/Assets/Logo.png /var/www/dyli-Webseiten-Software/Assets/

  # Kopieren der Datei 'Logo.png' aus dem Verzeichnis '/vagrant/config/' in dem Ordner '/var/www/dyli-Webseiten-Software/config/'
  cp /vagrant/config/dyli-Webseiten-Software.conf /var/www/dyli-Webseiten-Software/config/
  # Kopieren der Datei 'proxy.conf' aus dem Verzeichnis '/vagrant/config/' in dem Ordner '/var/www/dyli-Webseiten-Software/config/'
  cp /vagrant/config/proxy.conf /var/www/dyli-Webseiten-Software/config/
  # Kopieren der Datei 'Portfolio.css' aus dem Verzeichnis '/vagrant/styles/' in dem Ordner '/var/www/dyli-Webseiten-Software/styles/'
  cp /vagrant/styles/Portfolio.css /var/www/dyli-Webseiten-Software/styles/
  # Kopieren der Datei 'Portfolio.html' aus dem Verzeichnis '/vagrant/html/' in dem Ordner '/var/www/dyli-Webseiten-Software/html/'
  cp /vagrant/html/Portfolio.html /var/www/dyli-Webseiten-Software/html/

  # Kopieren aller Ordner und Dateien aus dem Verzeichnis '/vagrant' in den Ordner 'dyli-Webseiten-Software'
  # sudo cp -r /vagrant/* /var/www/dyli-Webseiten-Software/
  # Ändernung der Berechtigungen des Ordners 'dyli-Webseiten-Software' im Verzeichnis '/var/www' 
  # auf Benutzer: vagrant und Benutzergruppe: vagrant
  sudo chown -R vagrant:vagrant /var/www/dyli-Webseiten-Software/
  # Änderung der RWX Berechtigungen für den Benutzer und die Benutzergruppe
  sudo chmod -R 755 /var/www/dyli-Webseiten-Software/
  SHELL
end