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