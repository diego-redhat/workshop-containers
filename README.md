# ![image](https://github.com/user-attachments/assets/6e497687-0862-4b6f-92e1-a442097c97a8)

# 📌 Podman - Demo

O objetivo desta demonstração é colocar em prática alguns conceitos básicos de containers, abordando desde a criação até a execução, e como essas tecnologias podem simplificar o desenvolvimento e a implantação de aplicações..

## 1. Baixando nossa primeira imagem de contêiner

#### Neste passo, vamos aprender como baixar a nossa primeira imagem de contêiner:

```podman pull quay.io/fedora/httpd-24-micro:latest```

## 2. Confirmando a imagem baixada

#### Com o comando a seguir, é possível verificar a imagem baixada e observar seu tamanho:

```podman image ls```

![image](https://github.com/user-attachments/assets/5b7e8a32-c4b1-4f71-b5b5-8d332bb4970f)

## 3. Executando nosso primeiro container

#### Agora, vamos executar nosso primeiro container com a imagem do passo anterior:

`podman run -dit -p 8000:8080 --name meu_container quay.io/fedora/httpd-24-micro:latest`

## 4. Verificando o container em execução

#### Em seguida, podemos verificar se o container está em execução:

``podman container ls``

![image](https://github.com/user-attachments/assets/20965d7b-f6d0-469f-8289-106c67567b85)

#### Para verificar que o container está isolado da maquina host, pegue o ID gerado e acesse-o:

`podman exec -it 80402d266d18 bash`

#### Observe que se trata de um SO completamente diferente:

![image](https://github.com/user-attachments/assets/8ca1bc3f-3248-4906-a012-1cc9ee9cea3b)

#### Digite o comando abaixo para retornar para maquina host:

`exit`

## 5. Testando nosso webserver em funcionamento

#### Agora, basta abrir o navegador e acessar a URL http://127.0.0.1:8000 para verificar o funcionamento do webserver localmente:

![image](https://github.com/user-attachments/assets/c92a596f-e3ba-47f1-888d-564bed88c3f4)

## 6. Para finalizar, vamos parar e remover nosso container 

#### Primeiro, é necessário obter o ID do nosso container:

`podman container ls`

![image](https://github.com/user-attachments/assets/faa2d04e-9a62-4316-bf21-a5f2b41cd9d8)

#### Em seguida, basta remover os containers seguindo os passos abaixo:

`podman stop ef1885a19531`

`podman rm ef1885a19531`

## 7. Agora, vamos criar nossa primeira imagem de container

#### Baixe o projeto demo-app para o seu ambiente local e acesse utilizando os seguintes comandos:

`git clone https://github.com/diego-redhat/demo-app.git`

`cd demo-app`

## 8. Antes de construir nossa imagem, vamos analisar o arquivo Containerfile

`cat Containerfile`

```dockerfile
FROM quay.io/doliveira1277/golang-demo-base:v1.0 AS builder

WORKDIR /app

COPY . .

RUN go mod download

RUN go build -o demo-app

FROM quay.io/doliveira1277/golang-demo-runtime:v1.0

WORKDIR /app/

COPY --from=builder /app/demo-app .

COPY static/ /app/static/

EXPOSE 8080

CMD ["./demo-app"]
```

## 9. Realizando o Build da Imagem

`podman build -t my-image:v1.0 .`

## 10. Vamos verificar se nossa imagem foi criada com sucesso

#### Neste passo, vamos confirmar se a imagem my-image na versão v1.0 foi criada corretamente

`podman image ls`

![image](https://github.com/user-attachments/assets/d13b9788-e07f-475c-a867-72664ef7b1ba)

## 11. Após validar a criação da imagem, podemos criar o container

`podman run -dit -p 8000:8080 my-image:v1.0`

## 12. Testando nossa aplicação em funcionamento

#### Agora, basta abrir o navegador e acessar a URL http://127.0.0.1:8000 para verificar o funcionamento:

![image](https://github.com/user-attachments/assets/e097a736-cb39-4331-a4ef-379397608b4a)

## 13. Gerando um novo container a partir da mesma imagem

#### A tecnologia de containers permite que múltiplos containers sejam executados a partir da mesma imagem criada.

#### Será necessário alterar apenas a porta de origem no host. Para validar, repita o procedimento descrito no passo 12:

`podman run -dit -p 8001:8080 my-image:v1.0`

## 14. Vamos criar uma nova versão da nossa aplicação

#### Antes, precisamos fazer um pequeno ajuste no nosso código:

`vim static/index.html`

#### Altere a versão do arquivo PNG de `image_v1.png` para `image_v2.png`

![image](https://github.com/user-attachments/assets/08631632-6a76-484b-bfc8-a9c48f1314c6)

#### Para salvar a alteração, execute o comando abaixo no editor Vim:

`esc + :wq!`

## 15. Realizando o build da versão v2.0 da aplicação

`podman build -t my-image:v2.0 .`

## 16. Confirmando a criação da versão v2.0

`podman image ls`

![image](https://github.com/user-attachments/assets/7a2af6e9-8e8b-4f67-a4ef-1431646847a1)

## 17.  Podemos criar o novo container e realizar os testes.

`podman run -dit -p 8002:8080 my-image:v2.0`

![image](https://github.com/user-attachments/assets/c71a2bbe-ce49-4553-9978-320c1b808eab)

---
&nbsp;

