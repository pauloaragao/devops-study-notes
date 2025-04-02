# Comandos do Dockerfile

## FROM
Define a imagem base para o container. É o primeiro comando em um Dockerfile e essencial para iniciar a construção da imagem.

**Exemplo:**
```dockerfile
FROM ubuntu:20.04
```

---

## RUN
Executa comandos durante a construção da imagem. Geralmente usado para instalar pacotes ou executar scripts.

**Exemplo:**
```dockerfile
RUN apt-get update && apt-get install -y curl
```

---

## WORKDIR
Define o diretório de trabalho dentro do container. Todos os comandos subsequentes serão executados nesse diretório.

**Exemplo:**
```dockerfile
WORKDIR /app
```

---

## COPY
Copia arquivos ou diretórios do sistema host para o sistema de arquivos do container.

**Exemplo:**
```dockerfile
COPY . /app
```

---

## ADD
Semelhante ao `COPY`, mas com funcionalidades adicionais, como a extração automática de arquivos `.tar`. Ou como arquivos remotos também. 

**Exemplo:**
```dockerfile
ADD app.tar.gz /app
```

---

## LABEL
Adiciona metadados à imagem, como informações do autor ou descrição. Que podem ser usada para identificar quem executou. Pode usar o comando para verificar (Ex: docker inspect nome-da-imagem) 

**Exemplo:**
```dockerfile
LABEL maintainer="seuemail@exemplo.com"
```

---

## ENV
Define variáveis de ambiente que estarão disponíveis no container.

**Exemplo:**
```dockerfile
ENV APP_ENV=production
```

---

## VOLUME
Cria um ponto de montagem para persistência de dados, permitindo que dados sejam armazenados fora do container.

**Exemplo:**
```dockerfile
VOLUME /data
```

---

## ARG
Define variáveis de build que podem ser passadas como argumentos durante a construção da imagem.

**Exemplo:**
```dockerfile
ARG VERSION=1.0
```

---

## EXPOSE
Informa qual porta o container expõe, mas não a publica automaticamente no host.

**Exemplo:**
```dockerfile
EXPOSE 8080
```

---

## USER
Define o usuário que executará os comandos no container. Por padrão, o usuário é `root`.

**Exemplo:**
```dockerfile
USER appuser
```

---

## CMD
Define o comando padrão a ser executado quando o container iniciar. Pode ser sobrescrito ao executar o container.

**Exemplo:**
```dockerfile
CMD ["npm", "start"]
```

---

## ENTRYPOINT
Define o comando principal do container, permitindo que argumentos adicionais sejam passados durante a execução.

**Exemplo:**
```dockerfile
ENTRYPOINT ["python", "app.py"]
```

# Comandos Docker

## docker images
Lista todas as imagens disponíveis localmente no host Docker.

**Exemplo:**
```bash
docker images
```

**Saída esperada:**
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              20.04               1d622ef86b13        2 weeks ago         72.9MB
```

---

## docker image prune
Remove imagens não utilizadas para liberar espaço no disco. Este comando remove apenas imagens que não estão associadas a nenhum container.

**Exemplo:**
```bash
docker image prune
```

**Saída esperada:**
```
WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] y
```

---

## docker inspect
Exibe informações detalhadas sobre um container ou uma imagem, como configurações, volumes, variáveis de ambiente, etc.

**Exemplo para inspecionar uma imagem:**
```bash
docker inspect ubuntu:20.04
```

**Exemplo para inspecionar um container:**
```bash
docker inspect my-container
```

**Saída esperada (parcial):**
```json
[
    {
        "Id": "sha256:1d622ef86b13...",
        "RepoTags": [
            "ubuntu:20.04"
        ],
        "Config": {
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ]
        }
    }
]
```

---

## docker ps
Lista os containers em execução no momento.

**Exemplo:**
```bash
docker ps
```

**Saída esperada:**
```
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NAMES
d1b2c3d4e5f6   ubuntu:20.04   "/bin/bash"             10 minutes ago   Up 10 minutes                          my-container
```

---

## docker ps -a
Lista todos os containers, incluindo os que não estão em execução.

**Exemplo:**
```bash
docker ps -a
```

**Saída esperada:**
```
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS                  NAMES
d1b2c3d4e5f6   ubuntu:20.04   "/bin/bash"             10 minutes ago   Exited (0) 5 minutes ago                          my-container
```