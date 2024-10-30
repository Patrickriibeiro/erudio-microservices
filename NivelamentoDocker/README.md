## Nivelamento Docker

Url Spring Docker: https://spring.io/guides/gs/spring-boot-docker

Você deve fornecer uma visão clara e concisa de como o Dockerfile está configurado, bem como instruções para construir e executar a imagem Docker :

### 1. **Descrição do Dockerfile**
- **Imagem base**: Especifique qual imagem base está sendo usada (por exemplo, `FROM openjdk:17-jdk-alpine`).
- **Propósito**: Explique brevemente o propósito do Dockerfile, como por exemplo, "Este Dockerfile configura um ambiente de execução para um aplicativo Java com Spring Boot."

### 2. **Como Construir a Imagem Docker**
- **Comando de Build**: Inclua o comando para construir a imagem Docker. Por exemplo:
  ```bash
  docker build -t nome-da-imagem .
  ```
  Substitua `nome-da-imagem` pelo nome que você deseja dar à sua imagem.

### 3. **Como Executar a Imagem Docker**
- **Comando de Execução**: Forneça o comando para executar a imagem. Por exemplo:
  ```bash
  docker run -p 8080:8080 nome-da-imagem
  ```
  Aqui, substitua `nome-da-imagem` pelo nome da imagem que você construiu e ajuste as portas conforme necessário.

### 4. **Variáveis de Ambiente e Configurações**
- **Variáveis de Ambiente**: Liste quaisquer variáveis de ambiente que precisam ser configuradas antes de executar a imagem, e como elas podem ser configuradas. Por exemplo:
  ```bash
  docker run -e ENV_VAR=value -p 8080:8080 nome-da-imagem
  ```

### 5. **Volumes e Persistência de Dados**
- **Montagem de Volumes**: Explique como montar volumes, se necessário, para persistência de dados ou configuração adicional. Por exemplo:
  ```bash
  docker run -v /host/path:/container/path -p 8080:8080 nome-da-imagem
  ```

### 6. **Portas Expostas**
- **Portas**: Especifique quais portas são expostas e por que. Por exemplo, "A porta 8080 é exposta para acessar a aplicação web."

### 7. **Dependências Externas**
- **Dependências**: Mencione qualquer dependência externa necessária para construir ou executar a imagem. Por exemplo, "Este Dockerfile requer acesso à internet para baixar pacotes durante o build."

### 8. **Exemplos de Uso**
- **Exemplo de Execução**: Forneça um exemplo completo de como usar o Dockerfile, incluindo a construção da imagem e a execução de um contêiner.

```markdown
## Docker

### Construindo a Imagem

Para construir a imagem Docker para este projeto, utilize o seguinte comando:

```bash
docker build -t meu-aplicativo-java .
```

### Executando o Contêiner

Para executar o contêiner, utilize o comando abaixo:

```bash
docker run -p 8080:8080 meu-aplicativo-java
```

### Variáveis de Ambiente

Você pode configurar variáveis de ambiente utilizando a flag `-e`:

```bash
docker run -e ENV_VAR=value -p 8080:8080 meu-aplicativo-java
```

### Volumes

Para persistência de dados, monte um volume local:

```bash
docker run -v /host/path:/container/path -p 8080:8080 meu-aplicativo-java
```

Para "tagear" uma imagem Docker como `latest` no Docker Registry, você pode usar o comando `docker tag`. Esse comando permite que você crie um alias (`latest`) para uma imagem que já tenha sido criada. Vou descrever o processo:

### Passos para "tagear" uma imagem como `latest`

1. Primeiro, construa ou tenha a imagem que deseja "tagear":
   ```bash
   docker build -t meu-repositorio/minha-imagem:v1 .
   ```

2. Em seguida, crie uma tag `latest` para a mesma imagem:
   ```bash
   docker tag meu-repositorio/minha-imagem:v1 meu-repositorio/minha-imagem:latest
   ```

3. Agora, faça o push para o registry (ex.: Docker Hub, AWS ECR, etc.):
   ```bash
   docker push meu-repositorio/minha-imagem:latest
   ```

### Resumo
O comando completo seria:

```bash
docker build -t meu-repositorio/minha-imagem:v1 .
docker tag meu-repositorio/minha-imagem:v1 meu-repositorio/minha-imagem:latest
docker push meu-repositorio/minha-imagem:latest
```

Essa prática de "tagear" a última versão como `latest` é útil para manter o ambiente atualizado com a versão mais recente.

Para buscar imagens no Docker Hub diretamente pela linha de comando, você pode usar o comando `docker search`. Esse comando permite que você procure por imagens disponíveis no Docker Registry (Docker Hub) com base em uma palavra-chave.

### Exemplo de Uso

```bash
docker search nome-da-imagem
```

Por exemplo, para buscar imagens relacionadas ao MySQL:

```bash
docker search mysql
```

### Explicação dos Campos Retornados

O comando `docker search` exibe uma lista de imagens com as seguintes informações:

- **NAME**: Nome da imagem.
- **DESCRIPTION**: Descrição breve sobre o que a imagem faz.
- **STARS**: Número de "estrelas" ou avaliações positivas que a imagem recebeu.
- **OFFICIAL**: Indica se a imagem é oficial (geralmente feita e mantida pela própria empresa que fornece o software, como MySQL, Redis, etc.).
- **AUTOMATED**: Mostra se a imagem é gerada automaticamente a partir de um repositório (como o GitHub) com base em arquivos de configuração.

### Filtros Úteis

Você pode adicionar opções para refinar a busca:

- `--filter=stars=[número]`: Mostra apenas imagens com um certo número de estrelas (avaliações).
  
  ```bash
  docker search --filter=stars=100 mysql
  ```

- `--filter=is-official=true`: Mostra apenas imagens oficiais.

  ```bash
  docker search --filter=is-official=true mysql
  ```

Esses filtros ajudam a encontrar imagens confiáveis e amplamente usadas.

Para remover uma imagem Docker local, você pode usar o comando `docker rmi`. Esse comando aceita o ID ou o nome da imagem como argumento.

### Comando Básico

```bash
docker rmi nome-da-imagem
```

ou, se preferir, usando o ID da imagem:

```bash
docker rmi id-da-imagem
```

### Exemplo Prático

1. Primeiro, liste as imagens para identificar o nome ou ID da imagem que deseja remover:

   ```bash
   docker images
   ```

2. Em seguida, remova a imagem:

   ```bash
   docker rmi mysql:latest
   ```

### Forçar a Remoção

Se a imagem estiver sendo usada por um ou mais containers, você pode adicionar a opção `-f` (forçar):

```bash
docker rmi -f nome-da-imagem
```

### Remover Todas as Imagens

Para remover todas as imagens de uma vez:

```bash
docker rmi $(docker images -q)
```

Isso irá limpar todas as imagens, liberando espaço em disco.

O comando `docker logs -f` é usado para visualizar os logs de um container em tempo real. O `-f` (ou `--follow`) permite acompanhar o fluxo contínuo dos logs, similar ao comando `tail -f`.

### Exemplo de Uso

```bash
docker logs -f nome-do-container
```

ou, se preferir, usando o ID do container:

```bash
docker logs -f id-do-container
```

### Opções Úteis

- **`--tail [N]`**: Limita o número de linhas exibidas a partir do final dos logs. Por exemplo, para mostrar apenas as últimas 50 linhas:

  ```bash
  docker logs -f --tail 50 nome-do-container
  ```

- **`--since [tempo]`**: Mostra logs a partir de um determinado tempo. Você pode especificar em minutos, horas, etc. Exemplo:

  ```bash
  docker logs -f --since 1h nome-do-container
  ```

Esse comando é muito útil para monitorar aplicações e debugar problemas em containers em execução.

### Dependências Externas

```bash
Este Dockerfile requer acesso à internet para baixar dependências durante o build.
```

### Observação 
arquivo Dockerfile deve sempre começar com letra maiúscula. Além disso, todos os arquivos e subdiretórios presentes no mesmo diretório do Dockerfile serão incluídos na construção da imagem Docker. Certifique-se de que apenas os arquivos necessários para a aplicação estejam neste diretório para evitar incluir arquivos desnecessários na imagem final.