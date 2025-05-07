

### ✅ **Passo a passo para instalar o Docker no Ubuntu 22.04**

#### 1. **Atualize os pacotes existentes**

```bash
sudo apt update
sudo apt upgrade -y
```

#### 2. **Instale pacotes necessários para usar repositórios HTTPS**

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

#### 3. **Adicione a chave GPG oficial do Docker**

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

#### 4. **Adicione o repositório do Docker**

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### 5. **Atualize os pacotes com o novo repositório**

```bash
sudo apt update
```

#### 6. **Instale o Docker Engine, CLI e containerd**

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### 7. **Verifique se o Docker está funcionando**

```bash
sudo docker run hello-world
```

---

### 🔧 (Opcional) Rodar Docker sem `sudo`

Para não precisar digitar `sudo` toda vez:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

