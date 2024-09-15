## ZSH \- Configuracoes Iniciais
### Passo 1 \- Tornar o ZSH o interpretador padrão
```warp-runnable-command
# Atualizar a lista de pacotes e instalar o zsh
sudo apt update
sudo apt install -y zsh wget git curl

# Tornar o zsh o shell padrão do seu usuário
chsh -s $(which zsh)

# Fechar o terminal para aplicar as mudanças
echo "O terminal será fechado para aplicar as mudanças. Por favor, abra um novo terminal."
sleep 2
exit
```
### Passo 2 \- Instalar o oh\-my\-zsh
```warp-runnable-command
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```
### Passo 3 \- Configurar o history e outras necessidades básicas
```warp-runnable-command
# Adiciona as configurações diretamente no .zshrc
cat << 'EOF' >> ~/.zshrc

# Configurar o histórico com timestamps
HISTSIZE=1000000
SAVEHIST=1000000
# Configuração de formato de timestamp do oh-my-zsh
HIST_STAMPS="dd/mm/yyyy"


setopt EXTENDED_HISTORY       # gravar timestamp do comando no HISTFILE
setopt HIST_EXPIRE_DUPS_FIRST # excluir duplicatas primeiro quando o tamanho do HISTFILE exceder o HISTSIZE
setopt HIST_IGNORE_DUPS       # ignorar comandos duplicados na lista de histórico
setopt HIST_IGNORE_SPACE      # ignorar comandos que começam com espaço
setopt HIST_VERIFY            # mostrar comando com expansão de histórico para o usuário antes de executá-lo
setopt INC_APPEND_HISTORY     # adicionar comandos ao HISTFILE na ordem de execução
setopt SHARE_HISTORY          # compartilhar dados do histórico de comandos
EOF
```
## WARP \- Best Terminal \=\)
Use este link para a inscrição\: [https\:\/\/app\.warp\.dev\/referral\/R5KZKY](https://app.warp.dev/referral/R5KZKY)
```warp-runnable-command
sudo apt-get install wget gpg curl
wget -qO- https://releases.warp.dev/linux/keys/warp.asc | gpg --dearmor > warpdotdev.gpg
sudo install -D -o root -g root -m 644 warpdotdev.gpg /etc/apt/keyrings/warpdotdev.gpg
sudo sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/warpdotdev.gpg] https://releases.warp.dev/linux/deb stable main" > /etc/apt/sources.list.d/warpdotdev.list'
rm warpdotdev.gpg
sudo apt update && sudo apt install warp-terminal
```
## Flatpak \/ Pacotes
### Passo 1
```warp-runnable-command
sudo apt install flatpak plasma-discover-backend-flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
### Passo 2
```warp-runnable-command
# Adiciona as linhas ao ~/.profile apenas se elas não existirem
if ! grep -Fxq 'export XDG_DATA_DIRS="$XDG_DATA_DIRS:/var/lib/flatpak/exports/share:/home/$USER/.local/share/flatpak/exports/share"' ~/.profile; then
    echo -e "\n# Adicionando Flatpak ao XDG_DATA_DIRS\nexport XDG_DATA_DIRS=\"$XDG_DATA_DIRS:/var/lib/flatpak/exports/share:/home/$USER/.local/share/flatpak/exports/share\"" >> ~/.profile
fi

# Recarrega as configurações do ambiente
source ~/.profile
```
### Passo 3
```warp-runnable-command

flatpak install com.getpostman.Postman
flatpak install com.github.flxzt.rnote
flatpak install com.github.tchx84.Flatseal
flatpak install com.slack.Slack
flatpak install dev.geopjr.Calligraphy
flatpak install io.missioncenter.MissionCenter
flatpak install org.gimp.GIMP
flatpak install org.gnome.Platform//46
flatpak install org.gtk.Gtk3theme.Breeze//3.22
flatpak install org.mozilla.firefox
flatpak install flathub md.obsidian.Obsidian
flatpak install flathub com.microsoft.Edge
flatpak install flathub com.ktechpit.whatsie
flatpak install flathub net.devolutions.RDM
flatpak install flathub io.podman_desktop.PodmanDesktop
flatpak install com.discordapp.Discord
```
### Passo 4
```warp-runnable-command
sudo apt remove snapd
```
### Passo 5
```warp-runnable-command
sudo apt install vim gdebi timeshift ca-certificates curl gnupg kleopatra gh network-manager-openvpn network-manager-fortisslvpn gcr gnome-keyring gnome-keyring-pkcs11 libpam-gnome-keyring libpam-gnome-keyring openfortivpn sshpass wget apt-transport-https software-properties-common scdaemon ksnip default-jre caffeine peek pulseaudio xserver-xorg-input-synaptics solaar htop
```
# CLI
## Azure
```warp-runnable-command
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# Instalar o Bicep CLI
az bicep install

# Verificar a instalação do Bicep
az bicep version
```
## Kubectl
```warp-runnable-command
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```
## Helm
```warp-runnable-command
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```
## Hashicorp
```warp-runnable-command
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install terraform 
```
## Github
```warp-runnable-command
gh auth login
```
Instalar extensão do Copilot para Github
```warp-runnable-command
gh extension install github/gh-copilot
```
## Powershell
```warp-runnable-command
# Atualize a lista de pacotes
sudo apt update

# Baixe e instale a dependência libicu72
wget -O libicu72_amd64.deb http://mirrors.kernel.org/ubuntu/pool/main/i/icu/libicu72_72.1-3ubuntu3_amd64.deb
sudo dpkg -i libicu72_amd64.deb

# Obtenha a URL do pacote .deb mais recente do PowerShell para amd64
LATEST_PWSH_DEB_URL=$(curl -s https://api.github.com/repos/PowerShell/PowerShell/releases/latest | grep browser_download_url | grep 'powershell_.*deb_amd64.deb' | cut -d '"' -f 4)

# Baixe o pacote .deb mais recente do PowerShell
wget -O powershell_latest_amd64.deb $LATEST_PWSH_DEB_URL

# Instale o PowerShell
sudo dpkg -i powershell_latest_amd64.deb
```
# **Coisas de Dev**
## Docker
```warp-runnable-command
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```
## Ngrok
```warp-runnable-command
curl -s https://ngrok-agent.s3.amazonaws.com/ngrok.asc \
	| sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null \
	&& echo "deb https://ngrok-agent.s3.amazonaws.com buster main" \
	| sudo tee /etc/apt/sources.list.d/ngrok.list \
	&& sudo apt update \
	&& sudo apt install ngrok
```
## Miniconda
```warp-runnable-command
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
-O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```
## Atlassian SDK
```warp-runnable-command
# Adicionar o repositório Atlassian SDK
echo "deb https://packages.atlassian.com/debian/atlassian-sdk-deb/ stable contrib" | sudo tee -a /etc/apt/sources.list

# Baixar e adicionar a chave pública utilizando gpg
curl -sS https://packages.atlassian.com/api/gpg/key/public | gpg --dearmour | sudo tee /etc/apt/trusted.gpg.d/atlassian-sdk.gpg > /dev/null

# Atualizar os repositórios e instalar o Atlassian SDK
sudo apt-get update
sudo apt-get install atlassian-plugin-sdk
```
## NodeJS
### Passo 1 \- Instalar o gerenciador de versões
```warp-runnable-command
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
### Passo 2 \- Instalar a versão do NodeJS \(instala global o pnpm\)
```warp-runnable-command
# download and install Node.js (you may need to restart the terminal)
nvm install 20
nvm use 20
node -v
npm install -g pnpm
```
## Dotnet Auto Complete \(\.zshrc\)
```warp-runnable-command
echo "" >> ~/.zshrc && echo "# zsh parameter completion for the dotnet CLI

_dotnet_zsh_complete()
{
  local completions=(\"\$(dotnet complete \"\$words\")\")

  # If the completion list is empty, just continue with filename selection
  if [ -z \"\$completions\" ]
  then
    _arguments '*::arguments: _normal'
    return
  fi

  # This is not a variable assignment, don't remove spaces!
  _values = \"\${(ps:\n:)completions}\"
}

compdef _dotnet_zsh_complete dotnet" >> ~/.zshrc && source ~/.zshrc
```
## GO
### Instalação rapida e simples
```warp-runnable-command
curl -s https://go.dev/VERSION?m=text | head -n 1 | xargs -I {} zsh -c '\
wget https://dl.google.com/go/{}.linux-amd64.tar.gz && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf {}.linux-amd64.tar.gz && \
if ! grep -q "/usr/local/go/bin" ~/.zshrc; then echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.zshrc; fi && \
if ! grep -q "\$HOME/go/bin" ~/.zshrc; then echo "export PATH=\$PATH:\$HOME/go/bin" >> ~/.zshrc; fi && \
source ~/.zshrc && \
go version'
```
### Instalação por script shell \- \(criar um script shell com este conteúdo\, chmod \+x e executar\)
```yaml
#!/bin/zsh

# Obter a última versão do Go
LATEST_GO_VERSION=$(curl -s https://go.dev/VERSION?m=text | head -n 1)

# Definir a URL do arquivo tar.gz do Go
LATEST_GO_URL="https://dl.google.com/go/${LATEST_GO_VERSION}.linux-amd64.tar.gz"

# Definir o nome do arquivo
GO_TAR_FILE=$(basename $LATEST_GO_URL)

# Baixar o arquivo tar.gz do Go
wget $LATEST_GO_URL

# Remover qualquer instalação anterior do Go
sudo rm -rf /usr/local/go

# Extrair o arquivo tar.gz para /usr/local
sudo tar -C /usr/local -xzf $GO_TAR_FILE

# Adicionar Go ao PATH no ~/.zshrc
if ! grep -q '/usr/local/go/bin' ~/.zshrc; then
  echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.zshrc
fi

# Adicionar $HOME/go/bin ao PATH no ~/.zshrc
if ! grep -q '$HOME/go/bin' ~/.zshrc; then
  echo "export PATH=\$PATH:\$HOME/go/bin" >> ~/.zshrc
fi

# Aplicar as mudanças no PATH
source ~/.zshrc

# Verificar a instalação do Go
go version
```
## Telemetry generator for OpenTelemetry
Este binário para GO simula métricas do OpenTelmetry para fins de testes\/debugs\. Para mais informações acesse\: [https\:\/\/github\.com\/open\-telemetry\/opentelemetry\-collector\-contrib\/tree\/main\/cmd\/telemetrygen](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/cmd/telemetrygen)
```warp-runnable-command
go install github.com/open-telemetry/opentelemetry-collector-contrib/cmd/telemetrygen@latest
```
### Traces
```warp-runnable-command
telemetrygen traces --otlp-insecure --duration 5s
```
### Logs
```warp-runnable-command
telemetrygen logs --duration 5s --otlp-insecure
```
### Metrics
```warp-runnable-command
telemetrygen metrics --duration 5s --otlp-insecure
```
# AnyDesk
```warp-runnable-command
# Adicionar a chave do repositório aos provedores de software confiáveis
wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | gpg --dearmor | sudo tee /usr/share/keyrings/anydesk-archive-keyring.gpg

# Adicionar o repositório
echo "deb [signed-by=/usr/share/keyrings/anydesk-archive-keyring.gpg] http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list

# Atualizar o cache do apt
sudo apt update

# Instalar o AnyDesk
sudo apt install anydesk

# Desativar o AnyDesk inicio automático
sudo systemctl disable anydesk.service

# Parar o AnyDesk
sudo systemctl stop anydesk.service

# Ligar o AnyDesk
sudo systemctl start anydesk.service
```
## NerdFonts
```warp-runnable-command
git clone --depth 1 --branch master https://github.com/ryanoasis/nerd-fonts.git ~/Downloads/nerd-fonts && cd ~/Downloads/nerd-fonts && ./install.sh
```
## Forticlient VPN
```warp-runnable-command
# Baixe libappindicator1 e sobrescreva o arquivo existente
wget -O libappindicator1_amd64.deb http://mirrors.kernel.org/ubuntu/pool/universe/liba/libappindicator/libappindicator1_12.10.1+20.10.20200706.1-0ubuntu1_amd64.deb 

# Baixe a dependência necessária para libappindicator1 e sobrescreva o arquivo existente
wget -O libdbusmenu-gtk4_amd64.deb http://mirrors.kernel.org/ubuntu/pool/universe/libd/libdbusmenu/libdbusmenu-gtk4_16.04.1+18.10.20180917-0ubuntu8_amd64.deb

# Baixe o FortiClient com nome dinâmico e sobrescreva se já existir
wget --content-disposition -O forticlient_vpn_amd64.deb https://links.fortinet.com/forticlient/deb/vpnagent

# Instale os pacotes
sudo apt install -y ./libappindicator1_amd64.deb ./libdbusmenu-gtk4_amd64.deb ./forticlient_vpn_amd64.deb
```
## OpenVPN
```warp-runnable-command
# Instalar pacotes necessários
apt install -y apt-transport-https curl

# Criar o diretório de keyrings, se não existir
mkdir -p /etc/apt/keyrings

# Baixar a chave de assinatura do OpenVPN Inc
curl -sSfL https://packages.openvpn.net/packages-repo.gpg >/etc/apt/keyrings/openvpn.asc

# Obter automaticamente o nome da distribuição
DISTRO=$(lsb_release -cs)

# Configurar o repositório APT do OpenVPN 3 baseado na distribuição detectada e apenas para a arquitetura amd64
echo "deb [signed-by=/etc/apt/keyrings/openvpn.asc arch=amd64] https://packages.openvpn.net/openvpn3/debian $DISTRO main" | tee /etc/apt/sources.list.d/openvpn3.list

# Atualizar os pacotes e instalar o OpenVPN 3
apt update
apt install -y openvpn3
```
## OpenShift Local
```warp-runnable-command
sudo apt install qemu-kvm libvirt-daemon libvirt-daemon-system network-manager virtiofsd
```
```warp-runnable-command
wget https://developers.redhat.com/content-gateway/rest/mirror/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz
```
```warp-runnable-command
# Defina variáveis para facilitar a reutilização
DOWNLOAD_DIR=~/Downloads
BIN_DIR=~/bin
CRC_TAR=crc-linux-amd64.tar.xz
CRC_ARCHIVE="$DOWNLOAD_DIR/$CRC_TAR"
LINK_PATH=/usr/bin/crc

# Navegue para o diretório de Downloads
cd "$DOWNLOAD_DIR" || exit

# Remova quaisquer diretórios existentes que correspondam a 'crc-linux-*'
rm -rf crc-linux-*-amd64

# Extraia o tarball
tar xvf "$CRC_ARCHIVE"

# Encontre o diretório extraído dinamicamente
CRC_EXTRACT_DIR=$(find . -maxdepth 1 -type d -name 'crc-linux-*-amd64' | head -n 1)

# Verifique se o diretório foi encontrado
if [ -z "$CRC_EXTRACT_DIR" ]; then
    echo "Erro: Diretório extraído não encontrado."
    exit 1
fi

# Crie o diretório bin se não existir
mkdir -p "$BIN_DIR"

# Copie o binário crc para ~/bin, substituindo se já existir
cp -f "$CRC_EXTRACT_DIR/crc" "$BIN_DIR/crc"

# Determine o arquivo de configuração do shell
if [ -n "$ZSH_VERSION" ]; then
    SHELL_RC=~/.zshrc
elif [ -n "$BASH_VERSION" ]; then
    SHELL_RC=~/.bashrc
else
    SHELL_RC=~/.profile
fi

# Adicione ~/bin ao PATH apenas se não estiver presente
if ! grep -Fxq 'export PATH=$PATH:$HOME/bin' "$SHELL_RC"; then
    echo 'export PATH=$PATH:$HOME/bin' >> "$SHELL_RC"
    export PATH=$PATH:$HOME/bin
fi

# Crie o link simbólico apenas se ele não existir ou estiver incorreto
if [ -L "$LINK_PATH" ]; then
    CURRENT_TARGET=$(readlink "$LINK_PATH")
    if [ "$CURRENT_TARGET" != "$BIN_DIR/crc" ]; then
        sudo ln -sf "$BIN_DIR/crc" "$LINK_PATH"
    fi
elif [ -e "$LINK_PATH" ]; then
    echo "Arquivo $LINK_PATH já existe e não é um link simbólico. Pulando criação do link."
else
    sudo ln -s "$BIN_DIR/crc" "$LINK_PATH"
fi
```
```warp-runnable-command
crc config set consent-telemetry no
```
```warp-runnable-command
crc setup
```
```warp-runnable-command
crc start --log-level debug
```
### Acessando o ambiente 
```warp-runnable-command
# Configure o ambiente para o comando oc
eval $(crc oc-env)

# Faça login no cluster OpenShift
oc login -u developer https://api.crc.testing:6443
```
### Erro
A mensagem de erro indica que o CRC está tentando usar um novo bundle \(`crc_libvirt_4.16.7_amd64`\)\, mas a máquina virtual existente ainda está configurada para o bundle antigo \(`crc_libvirt_4.15.14_amd64`\)\. Para corrigir esse problema\, você precisará excluir o cluster existente e iniciar um novo com o novo bundle\.
```text
DEBU Bundle 'crc_libvirt_4.16.7_amd64' was requested, but the existing VM is using 'crc_libvirt_4.15.14_amd64'
DEBU Making call to close driver server
DEBU (crc) Calling .Close
DEBU Successfully made call to close driver server
DEBU Making call to close connection to plugin binary
Bundle 'crc_libvirt_4.16.7_amd64' was requested, but the existing VM is using 'crc_libvirt_4.15.14_amd64'. Please delete your existing cluster and start again
```
Execute o seguinte comando para excluir o cluster existente\:
```warp-runnable-command
crc delete
```
Após excluir o cluster antigo\, inicie o CRC novamente com o novo bundle\:
```warp-runnable-command
crc start --log-level debug
```
