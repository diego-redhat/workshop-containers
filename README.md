# ![image](https://github.com/user-attachments/assets/6e497687-0862-4b6f-92e1-a442097c97a8)

# 📌 Podman - Demo

O objetivo desta demonstração é colocar em prática alguns conceitos básicos de containers, abordando desde a criação até a execução, e como essas tecnologias podem simplificar o desenvolvimento e a implantação de aplicações..

---

## 1. 🔹 Baixando nossa primeira imagem de contêiner

#### Neste passo, vamos aprender como baixar a nossa primeira imagem de contêiner:

```podman pull quay.io/fedora/httpd-24-micro:latest```

---
&nbsp;

## 2. 🔹 Confirmando a imagem baixada

#### Com o comando a seguir, é possível verificar a imagem baixada e observar seu tamanho:

```podman image ls```

![image](https://github.com/user-attachments/assets/5b7e8a32-c4b1-4f71-b5b5-8d332bb4970f)

---
&nbsp;

## 3. 🔹 Executando nosso primeiro container

#### Agora, vamos executar nosso primeiro container com a imagem do passo anterior:

`podman run -dit -p 8000:8080 --name meu_container quay.io/fedora/httpd-24-micro:latest`

---
&nbsp;

## 4. 🔹 Verificando o container em execução

#### Em seguida, podemos verificar se o container está em execução:

``podman container ls``

![image](https://github.com/user-attachments/assets/afa3cb92-a8fd-4dbc-bc00-840b9d2c8521)



---
&nbsp;

## 5. 🔹 Testando nosso webserver em funcionamento

#### Agora, basta abrir o navegador e acessar a URL http://127.0.0.1:8000 para verificar o funcionamento do webserver localmente:

![image](https://github.com/user-attachments/assets/c92a596f-e3ba-47f1-888d-564bed88c3f4)

---
&nbsp;

## 6. 🔹 Para finalizar, vamos parar e remover nosso container 

#### Primeiro, é necessário obter o ID do nosso container:

`podman container ls`

![image](https://github.com/user-attachments/assets/faa2d04e-9a62-4316-bf21-a5f2b41cd9d8)

#### Em seguida, basta remover os containers seguindo os passos abaixo:

`podman stop ef1885a19531`

`podman rm ef1885a19531`

---
&nbsp;

## 7. 🔹 Run-gns3

#### After installation, you can start GNS3 by searching for the "GNS3" application in your desktop environment menu or by running:

```gns3```

💡 On the first run, GNS3 will open a setup wizard. For local usage, select "Run appliances on my local computer" and follow the instructions.


---
&nbsp;

## 8. 🔹 Agora, vamos criar nossa primeira imagem de container

#### Baixe o projeto demo-app para o seu ambiente local utilizando o seguinte comando:

`gns3`

---
&nbsp;


