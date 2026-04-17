Vagrant.configure("2") do |config|
  config.vm.box = "madebian12"
  # Colle ton lien GitHub entre les guillemets ci-dessous
config.vm.box_url = "https://github.com/charliewalker-art/boxe-image-debian/releases/download/v1.0.0/package.box"

  
  config.vm.hostname = "debian12"
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
     vb.cpus = 1
    vb.name = "debian12"
   
  end

  config.vm.network "private_network", ip: "192.168.44.44"

# ── Provisioning Shell ─────────────────────────────────────────────────────
  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    # On installe seulement les outils nécessaires (Ansible est requis pour la suite)
    apt-get install -y ansible python3-debian 

  
    # Changer le mot de passe root
    echo "root:debian" | chpasswd

    # Création de l'utilisateur debian (si n'existe pas déjà)
    if ! id "debian" &>/dev/null; then
      useradd -m -s /bin/bash debian
      echo "debian:1234" | chpasswd
    fi

    # Ajout de debian au groupe sudo
    usermod -aG sudo debian
  SHELL

  
end