# Docker para Ubuntu 18.04 e derivados

Para seguir este documento/tutorial, você precisará do seguinte: 

1. Uma distro Linux, no caso a Ubuntu 18.04, incluindo um usuário sudo não-root e um firewall.
2. Uma conta no [Docker Hub]() se você deseja usar sua próprias imagens e enviá-las ao Docker Hub.

## Instalando o Docker 

Para instalar o Docker no Ubuntu 18.04 e derivados e ainda poder receber automaticamente as futuras atualizações dele, você deve fazer o seguinte:

1. Abra um terminal (use as teclas CTRL + ALT + T)
2. Use o comando abaixo para atualizar o sistema

```
sudo apt update && sudo apt upgrade
```

3. Instale alguns pacotes necessários à instalação do Docker, usando o comando abaixo

```
sudo apt-get install apt-transport-https ca-certificates curl gnupg software-properties-common
```

4. Em seguida, adicione a chave GPG do repositório do Docker. Isso serve para adicionar ainda mais segurança aos pacotes que serão baixados

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

5. Use o comando abaixo para adicionar o repositório do Docker

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

6. É hora de instalar o Docker. Para isso, execute o seguinte comando

```
sudo apt install docker-ce
```

7. No final da instalação, para ter o serviço endo executado na inicialização do sistema, use os seguintes comandos

```
sudo systemctl enable docker

sudo systemctl start docker
```

8. Para garantir que o Docker esteja totalmente funcional, é uma boa ideia verificar o status do serviço

```
sudo systemctl status docker
```

9. Finalmente, veja a versão do Docker

```
docker -v ou docker --version
```

Agora que o Docker está instalado corretamente, vamos fazer os primeiros testes.

O Docker tem muitas imagens para quase tudo. É necessário procurar o que queremos, baixá-lo e usá-lo.

Por exemplo, para procurar uma imagem que contenha um servidor LAMP, use o seguinte comando:

```
sudo docker search lamp
```

Em seguida, use o comando abaixo para instalar a imagem escolhida

```
sudo docker pull nickistre/ubuntu-lamp-wordpress
```

Se você quiser listar todas as imagens que você instalou, use este comando

```
sudo docker images
```
































































































































































