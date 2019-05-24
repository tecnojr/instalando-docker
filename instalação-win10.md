# Docker - Windows 10 Pro

O intuito deste documento é mostrar como instalar e utilizar o Docker Desktop for Windows para Windows 10 em poucos minutos. Antes, veja alguns requisitos que você precisa atender:

  1. Você deve ter o suporte a virtualização habilitado em seu computador;
  2. Seu Windows deve ser 64 bits versão 1607 e build: 14393.0;
  3. Você deve habilitar o recurso do hyper-v;
  4. Baixe o Docker para o Windows pelo [link.](https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe). Apesar de não ser necessário, posteriormente será preciso ter uma conta para usar as funcionalidades.

## Ativando o Hyper-v e o suporte a virtualização

Primeiro vá até o **Painel de Controle** > **Programas** > **Ativar ou desativar recursos do Windows**. Dentre as várias opções que irão aparecer marque as seguintes: **Containers**, **Hyper-V**.

Dê algum tempo para o Windows aplicar alterações, após isso, reinicie o computador.

## Instalando o Docker for Windows

Após essa etapa inicial, baixe o Docker for Windows e execute o instalador (você precisará fazer logon. Crie uma conta se você não tiver um), espere um tempo até que ele baixe os pacotes de código. Após essa etapa irá aparecer duas opções de configuração: 1. **Adicionar atalho ao Desktop**, 2. **Usar os contêineres do Windows ao invés dos contêineres do Linux**. Neste documento/tutorial eu irei utilizar os contêineres do Windows ao invés dos do Linux, logo marque a segunda opção. Após o processo de instalação terminar, aparecerá um botão, clique nele para reiniciar novamente o computador. [Instruções de instalação detalhadas](https://docs.docker.com/docker-for-windows/install/) podem ser encontradas na documentação do Docker. 

## Instalar imagens de contêiner base

Os contêineres do Windows são criados a partir de imagens base. O comando a seguir extrairá a imagem base do Nano Server.

```
docker pull mcr.microsoft.com/windows/nanoserver:1809
```

Assim que é feito o pull da imagem, executar `docker images` retornará uma lista de imagens instaladas, neste caso, a imagem do Nano Server.

```
docker images

REPOSITORY             TAG          IMAGE ID           CREATED        SIZE
microsoft/nanoserver   latest     105d76d0f40e        4 days ago     652 MB
```

## Executando seu primero contêiner do Windows

Para este exemplo simples, uma imagem de contêiner "Hello World" será criada e implantada. Para obter a melhor experiência, execute estes comandos em um shell de CMD ou no Windows PowerShell elevado.

>O ISE do Windows PowerShell não funciona para sessões interativas com contêineres. Embora o contêiner esteja em execução, pode parecer que ele está parado.

Primeiro, inicie um contêiner com uma sessão interativa da imagem `nanoserver`. Depois que o contêiner for iniciado, você receberá um shell de comando de dentro do contêiner.

```
docker run -it mcr.microsoft.com/windows/nanoserver:1809 cmd.exe
```

Dentro do contêiner, criaremos um arquivo de texto simples "Hello World".

```
echo "Hello World!" > Hello.txt
```

Quando tiver concluído, saia do contêiner.

```
exit
```

Agora, você criará uma nova imagem de contêiner do contêiner modificado. Para ver uma lista de contêineres, execute o seguinte e anote a ID do contêiner.

```
docker ps -a
```

Execute o seguinte comando para criar uma nova imagem ‘HelloWorld’. Substitua com a ID do seu contêiner.

```
docker commit <containerid> helloworld
```

Quando tiver concluído, você terá uma imagem personalizada que contém o script hello world. Isso pode ser visto com o seguinte comando.

```
docker images
```

Finalmente, para executar o contêiner, use o comando `docker run`.

```
docker run --rm helloworld cmd.exe /s /c type Hello.txt
```

O resultado do comando `docker run` é que um contêiner em execução em isolamento do Hyper-V foi criado da imagem 'HelloWorld', uma instância do cmd foi iniciada no contêiner e executados uma leitura de nosso arquivo (saída ecoada para o shell) e, em seguida, o contêiner foi parado e removido.


















