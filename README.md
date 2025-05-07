# Implementação do Fedimintd

Este guia descreve os passos para implementar o Fedimintd.

## Pré-requisitos (PRECISAM ESTAR PRONTOS ANTES DE RODAR O SCRIPT)
Certificar que as portas 80, 443, 8173 e 8174 estão abertas. ** IMPORTANTE: Porta 8173 deve estar aberta para UDP também. **
Ter um nome de dominio, seudominio.com apontando para a maquina onde será instalado Fedimint
Executar o comando na conta ROOT. Use o comando `sudo su`


## Instalação
```bash
git clone https://github.com/jvxis/fedimint-docker
```
# Após a instalação, vá para o diretório e pare os serviços:
```bash
cd fedimint-docker
```
# Edite o arquivo .env e altere a variável `FM_DOMAIN` para o seu nome de domínio
```bash
nano .env
```
# Salve CTRL+X - YES
# Inicie os Serviços
```bash
docker compose up -d
```
# Verifique se tudo certo
Teste fedimintd
```bash
docker logs fedimint-docker-fedimintd-1
```
Não pode ter erro.

Resultado Esperado:
```bash
Starting fedimintd
2025-05-05T12:39:32.206336Z  INFO fedimintd::fedimintd: Starting fedimintd (version: 0.7.0 version_hash: b983d25d4c3cce1751c54e3ad0230fc507e3aeec)
2025-05-05T12:39:32.206484Z  WARN fm::core: FM_BITCOIN_RPC_KIND is obsolete, use FM_DEFAULT_BITCOIN_RPC_KIND instead
2025-05-05T12:39:32.206496Z  WARN fm::core: FM_BITCOIN_RPC_URL is obsolete, use FM_DEFAULT_BITCOIN_RPC_URL instead
2025-05-05T12:39:32.289114Z  INFO fm::consensus: Starting config gen
2025-05-05T12:39:32.290131Z  INFO fm::net::api: Starting http api on ws://172.20.0.11:8174
2025-05-05T12:39:32.290166Z  INFO fm::net::auth: Api available for public access
2025-05-05T12:39:32.291648Z  INFO fm::consensus: Setup UI running at http://172.20.0.11:8175 🚀
```
Teste Containers
```bash
docker ps
```
Resultado Esperado:
```bash
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                                                                                          NAMES
a9f1e597a5fa   traefik:v2.10               "/entrypoint.sh --pr…"   36 minutes ago   Up 36 minutes   80/tcp, 0.0.0.0:443->443/tcp                                                                   traefik
c966712450da   fedimint/fedimintd:v0.7.0   "/nix/store/i2n2xcgj…"   36 minutes ago   Up 36 minutes   0.0.0.0:8173->8173/tcp, 0.0.0.0:8173-8174->8173-8174/udp, 8174/tcp, 127.0.0.1:8175->8175/tcp   fedimint-docker-fedimintd-1
7a93fbe9f558   bitcoin/bitcoin:28.1        "/entrypoint.sh -pri…"   36 minutes ago   Up 36 minutes   8332/tcp, 18332-18333/tcp, 18443-18444/tcp, 38332-38333/tcp, 0.0.0.0:8333->8333/tcp            bitcoin
```

# Se não tem erro basta acessar o site com https://fedimint.seu-dominio.com (As vezes melhor acessar com Janela Anônima)
![image](https://github.com/user-attachments/assets/225cb7a5-2aa1-46ed-a580-58c1f83fa3f4)


## IMPORTANTE

# Caso precise Reiniciar do ZERO
Apague o diretorio fedimint-services antes de executar novamente o script
