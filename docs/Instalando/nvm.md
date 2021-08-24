
*24 de julho de 2021 365Tech*

# **O que é nvm ?**
O NVM (Node Version Manager) é um script de shell usado para instalar e gerenciar Node.js em um sistema baseado em Linux. Os usuários do macOS tambem podem instalar o NVM usando o homebrew.

Nvm é uma forma muito pratica de escolher a versão especifica do node que deseja excutar sem precisar remover e instalar a versão desejada.

# **Step 1 –Remover Node Existente **
```sh
brew uninstall --ignore-dependencies node 
brew uninstall --force node 
```

# **Step 2 – Instalando NVM no macOS**
```sh
brew update 
brew install nvm 
```

Criar um diretorio NVM na "home".
```sh
mkdir ~/.nvm 
```

Configure variaveis de ambientes necessarias.
```sh
vim ~/.bash_profile 
```

Adicione as linhas em  ~/.bash_profile ( ou ~/.zshrc em macOS Catalina ou  superior)
```sh
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
```
*ESC + :wq para salvar o arquivo e fechar*

Em seguida, Carregue a variáveis no ambiente shell atual. No próximo login, ele será carregado automaticamente.
```sh
source ~/.bash_profile
```

Pronto. O NVM foi instalado em seu sistema macOS. Vá para próxima etapa para aprender instalar as versões do Node.js com a ajuda do nvm.

# **Step 3 - Instale Node.js com NVM**
Verifique quais versões do Node estão disponíveis para instalação. Para ver as versões disponíveis, digite:
```sh
nvm ls-remote 
```

Agora, você pode instalar qualquer versão listada na saída acima. Você também pode usar nomes de alias para a versão mais recente do node, lts para a versão LTS mais recente, etc.

```sh
nvm install node     ## Instalando a versão mais recente 
nvm install 14       ## Instalando o Node.js versão 14.X 
```
Depois de instalar, você pode verificar o que está instalado com:

```sh
nvm ls 
nvm list node.js macos
```

Se você instalou várias versões em seu sistema, pode definir qualquer versão como a versão padrão a qualquer momento. Para definir o node 14.X como versão padrão, basta usar:

```sh
nvm use 14 
```

Da mesma forma, você pode instalar outras versões como Node 12.X ou Node 15 e alternar entre eles.



