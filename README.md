# 🚀 Configuração de Ambiente com Docker, Laravel, Postgres, NGINX e Redis

Este projeto tem como objetivo criar um ambiente de desenvolvimento completo utilizando **Docker**, integrado com **Postgres**, **NGINX**, **Redis** e **Laravel**.  
A configuração foi feita para simplificar o setup e permitir que todos os serviços rodem de forma isolada em containers, facilitando a manutenção e escalabilidade.

---

## 📂 Estrutura de Pastas

No diretório `C://`, crie uma pasta com o nome do seu projeto.  
Dentro dela, siga a seguinte estrutura:

```
📂 nome-do-projeto
├── 📂 docker
│   ├── 📂 php        # Configuração do PHP/Laravel
│   │   └── Dockerfile
│   ├── 📂 nginx      # Configuração do NGINX
│   │   └── nginx.conf
│   ├── 📂 db         # Configuração do Postgres
│   │   └── Dockerfile
│   └── 📂 redis      # Configuração do Redis
│       └── Dockerfile
├── 📂 application    # Código do Laravel
└── docker-compose.yml
```

---

## 🛠 Passo a Passo

### 1️⃣ Criar o arquivo `docker-compose.yml`
Este arquivo será responsável por orquestrar todos os containers (**PHP/Laravel**, **Postgres**, **NGINX** e **Redis**).  
Dentro dele também será indicado o caminho da pasta `application`, onde ficará o projeto Laravel.

---

### 2️⃣ Subir os containers
Com todos os arquivos de configuração criados, rode:

```bash
docker compose up
```

---

## ⚡ Instalação do Laravel no Docker

Antes de criar o projeto Laravel, certifique-se de que todos os containers estão rodando.

```bash
docker compose run --rm app composer create-project --prefer-dist laravel/laravel application
```

Ao finalizar, o Laravel vai gerar automaticamente uma chave no arquivo `.env`, na variável `APP_KEY`.

---

### 🔑 Adicionar `APP_KEY` ao `docker-compose.yml`

Localize a seção `environment` no serviço do Laravel e adicione junto a chave gerado:

```yaml
environment:
  - COMPOSER_HOME=/composer
  - COMPOSER_ALLOW_SUPERUSER=1
  - APP_ENV=local
  - APP_KEY=base64:V9lMOMKFhL7IdZ9/3KcjtT24SIqRw+Oz7ObmYy9YvJQ=
```

---

### 🔄 Reiniciar os containers

Após atualizar o `docker-compose.yml`, reinicie os containers:

```bash
# Encerrar containers
docker compose down

# Subir novamente
docker compose up
```