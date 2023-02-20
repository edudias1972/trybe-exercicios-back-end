# trybe-exercicios-back-end
trybe-exercicios-back-end
https://github.com/edudias1972/trybe-exercicios-back-end.git
O que você vai aprender neste módulo?
Configurar e colocar em um container suas aplicações utilizando o Docker 🐋;

Usar banco de dados relacionais com o MySQL 🎲;

Construir o código do back-end com o Node.JS 👩‍, utilizando bancos de dados relacionais e não relacionais;

Usar o Typescript 🏋️ para programar em alto nível com o JS;

Evoluir a qualidade do nosso código com o SOLID e com programação orientada a objetos (POO) 🧐;

Usar bancos de dados não relacionais com o MongoDB, utilizando documentos e coleções 📝;

Depois dessa experiência, você não será a mesma pessoa! Na verdade, será uma pessoa desenvolvedora preparada para mandar muito bem no mercado de trabalho. 😍

Você será capaz de:
Compreender o conceito de empacotamento de aplicações;
Compreender o que é o Docker e quais problemas ele resolve;
Compreender o que é uma imagem Docker;
Compreender o que é um container Docker;
Instalar o Docker;
Executar seu primeiro container Docker;
Compreender quais são os principais comandos para utilização do Docker na interface de linha de comando (CLI);
Obter imagens vindas de um Registry e executá-las como um container!
Por que isso é importante?
Enquanto pessoas desenvolvedoras é comum nos depararmos com diversas ferramentas e tecnologias, tendo que lidar com uma quantidade significativa de ambientes distintos durante o ciclo de desenvolvimento. Por exemplo, temos:

o ambiente local, que é o computador que usamos para desenvolver;
o ambiente de staging, que utilizamos para testar e validar as funcionalidades;
o ambiente de produção acessado pelas pessoas usuárias do produto.
Esse cenário exige que sejam feitas a preparação e configuração de todo o ambiente com as tecnologias necessárias, além de fazê-las funcionar em conjunto.

Fazer isso nem sempre é uma tarefa simples! O processo se torna ainda mais complexo quando há múltiplos ambientes, distintos entre si, e também há a necessidade de rodar em diversas máquinas (desde sua máquina pessoal local, servidores externos pagos, ou mesmo uma máquina virtual) que, muitas vezes, possuem configurações e utilizam sistemas operacionais diferentes.

Essa frase é famosa justamente porque precisamos lidar com os diferentes cenários citados até aqui.

Por exemplo, se uma pessoa desenvolve utilizando uma distribuição ‘A’ de Linux, outra utiliza Windows e outra Mac e no servidor roda uma distribuição ‘B’ de Linux, todas elas estão trabalhando no mesmo projeto, e da mesma forma, pois estão disponibilizando-o para o ambiente de produção, em um servidor remoto comum, conhecido como processo de deploy ou implantação.

Além dos diferentes sistemas operacionais, é comum que existam softwares, ferramentas e dependências distintas ou com versões diferentes em cada máquina. Dessa maneira, é muito difícil garantir que o que funciona na máquina de uma pessoa funcionará na máquina de outra sem a necessidade de fazer novas configurações. Inclusive, não conseguimos nem garantir que também funcionará nos servidores durante o processo de deploy.

Para resolver estes problemas de complexidade e de compatibilidade, bem como economizar o tempo no processo de preparação de uma máquina para rodar um programa específico, foi criado o Docker. 🐋

Isso funciona em todas as máquinas
Isso funciona em todas as máquinas
Com o Docker também conseguimos simular e testar facilmente um ambiente completo, de maneira leve e inteligente, em questão de minutos, podendo replicar tais configurações para outra máquina com facilidade, além de conseguir trabalhar com nossas aplicações em escala de forma simples!

Portanto, por meio do Docker resolvemos o problema de incompatibilidade com outros sistemas, dado que ele funciona como uma espécie de “empacotador” de todas essas dependências e requisitos para que sua aplicação funcione em qualquer ambiente! Isso torna simples sua disponibilização!

Por todas essas vantagens, o Docker ganhou muito espaço e seu uso é cada vez mais comum!

As maiores empresas de tecnologia utilizam o Docker para manter grandes arquiteturas, assim como as pequenas empresas utilizam de suas facilidades para manter suas aplicações no ar de forma simples e com menos custos.

Se olharmos o Google Trends (dados sobre pesquisas no Google), começando pelo ano de lançamento do Docker (2013) até o fim da década (2019), conseguimos ter um bom indicador dessa popularidade por meio do número de pesquisas pelo software “Docker” nesse período. Muito disso se deve ao conceito de “conteinerização” (colocar em containers) de aplicações, que é adotado por muitas tecnologias atualmente.

Dados sobre interesse pelo software Docker no Google Trends
Dados sobre interesse pelo software Docker no Google Trends
Dessa forma, é essencial saber Docker, tanto para se adequar ao mercado como para aproveitar seus benefícios durante o ciclo de vida de nossas aplicações.


1. Desinstale versões anteriores
Caso você já possua alguma versão de Docker instalada na sua máquina e queira refazer o processo de instalação para atualizar ou para corrigir algum problema, primeiro você deve remover os pacotes da versão que está na sua máquina. Para isso, utilize o seguinte comando no terminal:

Copiar
sudo apt-get remove docker* containerd runc
Caso nenhum dos pacotes esteja instalado, esse comando retornará o erro E: Impossível encontrar o <nome-do-pacote>. Nesse caso, é só prosseguir com a instalação.

👀 De olho na dica: o Docker preserva informações sobre imagens, containers, volumes e redes na pasta /var/lib/docker/. Nesse processo, esses arquivos não são apagados. Para remoção completa do Docker no seu sistema, consulte a seção Desinstalando o Docker no final desse tópico.

2. Instalando as dependências iniciais
Para habilitar a obtenção dos repositórios via HTTPS pelo apt-get, instale os pacotes listados abaixo. Nós precisamos disso para prosseguir a instalação:

Copiar
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
3. Adicionando a chave pública do repositório Docker em nossa máquina
Para adicionar a chave GPG* oficial do repositório do Docker, execute o comando a seguir:

⚠️ Este passo é necessário pois precisamos obter uma chave pública dos servidores da empresa Docker Inc para garantir que qualquer pacote obtido através da Internet esteja assinado por esta chave, evitando assim possíveis ataques de segurança.

Copiar
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
Se tudo der certo, você não deve receber nenhum retorno visual.

4. Adicionando o repositório remoto na lista do apt
Para finalmente adicionar o repositório oficial do Docker no apt, execute o seguinte comando:

Copiar
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Perceba que adicionamos o repositório stable (em $(lsb_release -cs) stable), isso significa que teremos somente o repositório com as versões estáveis do Docker.

Em distribuições baseadas no Ubuntu (como o Linux Mint), talvez você precise alterar o comando $(lsb_release -cs) para uma versão do Ubuntu que seja compatível com aquele sistema. Por exemplo: caso utilize o Linux Mint Tessa, você deve alterar o valor para bionic.

⚠️Importante: o Docker não garante seu funcionamento em sistemas fora dos requisitos de sistema operacional.

5. Instalando o Docker no Linux
Agora sim, vamos à instalação do Docker!

Primeiro, vamos garantir que os índices dos pacotes do apt estão atualizados, já que adicionamos um novo repositório:
Copiar
sudo apt-get update
Vamos instalar a última versão estável do Docker Engine - Community, que é uma versão mantida pela própria comunidade, já que o Docker é open source.
Para isso, execute no terminal:

Copiar
sudo apt-get install docker-ce docker-ce-cli containerd.io
6. Adicionando seu usuário ao grupo de usuários Docker
Para evitar o uso de sudo em todos os comandos Docker que formos executar, vamos dar as devidas permissões ao nosso usuário.

Primeiro crie um grupo chamado docker:
Copiar
sudo groupadd docker
Caso ocorra uma mensagem: groupadd: grupo 'docker' já existe, é só prosseguir.

Então, use o comando abaixo para adicionar seu usuário a este novo grupo:
Copiar
sudo usermod -aG docker $USER
⚠️ Execute o comando exatamente como ele está acima, considerando as letras maiúsculas e minúsculas.

Para ativar as alterações realizadas nos grupos, você pode realizar logout e login de sua sessão ou executar o seguinte comando no terminal:
Copiar
newgrp docker
⚠️ Se após esse comando você tiver algum problema, reinicie sua máquina. Depois de reiniciar siga para os próximos passos

7. Inicie o Daemon do Docker
O Daemon é um serviço que fica no background, ou seja, é um serviço que sempre está em execução e aguarda por comandos feitos por meio do CLI. Entretanto, para que este serviço fique sempre disponível, precisamos ativá-lo, até mesmo após reiniciarmos nosso computador.

Para consultar o status atual do daemon do Docker, execute o seguinte comando:
Copiar
sudo systemctl status docker
O comando anterior deve retornar algo como um pequeno relatório sobre o serviço, onde consta seu status de funcionamento:
Copiar
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Thu 2021-09-23 11:55:11 -03; 2s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
    Process: 2034 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=0>
   Main PID: 2034 (code=exited, status=0/SUCCESS
Caso o parâmetro Active esteja como stop/waiting ou no nosso caso, como inactive, rode o comando start para iniciá-lo:
Copiar
sudo systemctl start docker
Ao consultar o status novamente, o processo deverá estar como start/running/active.

Agora, vamos habilitar o daemon do Docker para iniciar durante o boot:
Copiar
sudo systemctl enable docker
8. Valide a instalação
Para validar se tudo ocorreu como deveria na instalação, vamos executar o tão esperado hello world do Docker:

Copiar
docker run hello-world

Preciso instalar tudo o que é necessário dentro da imagem?
Sim, porém lembre-se que não precisamos reinventar a roda. Vamos comparar os dois cenários abaixo:

🔺Problema: você precisa executar um código JavaScript usando Node. O que você faz?

1️⃣ Cenário 1: Cria uma receita que, partindo de uma imagem Docker vazia:

Faz a instalação de um sistema operacional Linux
Faz a instalação das dependências para poder instalar o Node
Faz a instalação do Node
Copia seu código-fonte para dentro da imagem
Feito!

2️⃣ Cenário 2: Cria uma receita que, partindo de uma imagem Docker com Linux e Node já instalados:

Copia seu código-fonte para dentro da imagem
Feito!

Percebeu a diferença?

Muitas pessoas já usam o Docker para executar aplicações em Node, por exemplo. Se já existe uma “receita” de como construir uma Imagem Docker com Linux e Node já instalados, podemos usar essa imagem como base para criarmos uma nova imagem!

Agora, como vamos obter essas imagens já construídas? Será que existe algum tipo local de compartilhamento ou catálogo de imagens Docker prontas? 🤔 Sim, já existe e se chama Registry.

Registry
Registry é um local remoto onde podemos enviar e baixar imagens Docker. Podemos utilizá-lo como um catálogo de imagens Docker, onde é possível criar novas imagens usando outras imagens do catálogo como base. Com isso, temos uma biblioteca completa de aplicações e ferramentas já prontas para uso em uma imagem Docker! 🌟

Normalmente, este serviço é oferecido em duas categorias:

Veja alguns exemplos de registries públicos:

Docker Hub: a própria Docker Inc. oferece um serviço de registry público;
Quay Container Registry: a empresa Red Hat também oferece um serviço semelhante.
As grandes empresas de serviços em nuvem, como Amazon, Google Cloud Platform e Microsoft Azure, possuem seus próprios serviços de Registry! Entretanto, são serviços pagos. Acesse os links abaixo caso queira conhecer melhor cada um deles:

Amazon Elastic Container Registry (ECR), oferecida pela Amazon.
Google Container Registry (GCR), oferecido pelo Google Cloud Platform.
Azure Container Registry (ACR), oferecido pela Microsoft Azure.
Até agora já aprendemos vários conceitos novos, mas não tivemos mão na massa! Vamos conhecer nossos primeiros comandos do Docker pra ficar mais interessante?

Bora continuar mergulhando no incrível mundo de Docker! 🐋

Chegou a hora de finalmente conhecermos os comandos básicos de interação com o Docker, através do CLI.

⚠️ os comandos feitos através do CLI são enviados para a API interna do Docker, que, por sua vez, envia os comandos para o Daemon.

📝 Anote aí: Alguns pontos importantes antes de começar:

docker <comando> <subcomando> <parâmetros> é o formato padrão para comandos não-abreviados no CLI;

Utilize o parâmetro --help no <comando> ou <subcomando> para ter a relação completa do que pode ser executado a partir deles;

Exemplo: docker container --help ou docker container run --help.
Os <parâmetros> são opcionais na execução dos comandos;

O conteúdo faz referência à documentação oficial do Docker.

Nos exemplos desta seção, nós usaremos imagens Docker que já foram construídas e publicadas no Docker Hub de maneira pública. Em um próximo momento, vamos aprender como criar nossas próprias imagens Docker e executá-las como containers!
Listando imagens
Primeiro, vamos aprender a visualizar as imagens Docker em nosso computador! Veremos o nome, sua data de criação e seu tamanho em disco.

➡️ Utilize o comando docker images para visualizar todas as imagens Docker que já estão presentes em sua máquina.

Ao tentar executar um container com uma imagem específica e esta imagem não estiver presente em nossa máquina, o Docker por padrão tentará obter a imagem Docker através do seu Registry, o Docker Hub. Veja um exemplo de saída do comando em uma máquina sem nenhuma imagem:
Copiar
pessoa@trybe:~/course$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
Agora, veja um exemplo de saída do comando com uma máquina com várias imagens Docker:
Copiar
pessoa@trybe:~/course$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
python       3.10      de1ec279ff75   14 hours ago   919MB
alpine       3.14      e04c818066af   2 weeks ago    5.59MB
Isso significa que se tentarmos executar um container utilizando essas imagens e com essas tags, o Docker utilizará a versão presente na máquina, e não tentará obtê-la novamente do Docker Hub.

Listando containers
➡️ Utilize o comando docker ps ou o comando mais novo, o docker container ls, para listar todos os containers em execução neste momento em sua máquina.

Veja o exemplo abaixo em uma máquina que não há nenhum container em execução no momento:
Copiar
pessoa@trybe:~/course$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
pessoa@trybe:~/course$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
Agora, veja o exemplo de saída abaixo quando temos alguns containers em execução no momento:
Copiar
pessoa@trybe:~/course$ docker container ls
CONTAINER ID   IMAGE         COMMAND        CREATED          STATUS          PORTS     NAMES
1cc75e507cd0   alpine:3.14   "sleep 5000"   7 seconds ago    Up 6 seconds              angry_mirzakhani
9a38f7a32b42   python:3.10   "sleep 5000"   15 seconds ago   Up 15 seconds             hungry_yonath
Entretanto, por padrão, o comando docker ps não exibe containers que foram parados ou que terminaram sua execução. Para visualizar todos os containers atuais, incluindo os que estão em execução e também parados, é necessário utilizar a flag -a. Veja o exemplo de saída do comando abaixo:

Copiar
pessoa@trybe:~/course$ docker container ls -a
CONTAINER ID   IMAGE         COMMAND        CREATED          STATUS          PORTS                  NAMES
1cc75e507cd0   alpine:3.14   "sleep 5000"   7 seconds ago    Up 6 seconds                           angry_mirzakhani
9a38f7a32b42   python:3.10   "sleep 5000"   15 seconds ago   Up 15 seconds                          hungry_yonath
14a00a2e09c9   alpine:3.14   "/bin/sh"      12 minutes ago   Exited (0) 12 minutes ago              meu-container
Acabamos de explicar como verificar a lista de imagens e lista de containers, pois nos próximos exemplos nós vamos usar estes mesmos comandos em conjunto com os novos comandos que vamos aprender. 👀

Executando um novo container
➡️ Utilize o comando docker container run <flags>? <imagem>:<tag> <argumentos>? para executar um container utilizando a imagem identificada pelo <imagem>:<tag>.

O exemplo abaixo executa um container usando a imagem Docker alpine e a tag 3.14:
Copiar
pessoa@trybe:~/course$ docker container run alpine:3.14 echo "Hello World"
Unable to find image 'alpine:3.14' locally
3.14: Pulling from library/alpine
8663204ce13b: Pull complete
Digest: sha256:06b5d462c92fc39303e6363c65e074559f8d6b1363250027ed5053557e3398c5
Status: Downloaded newer image for alpine:3.14
Hello World!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                 CREATED          STATUS                      PORTS     NAMES
52712fa829f0   alpine:3.14   "echo 'Hello World'"   19 seconds ago   Exited (0) 19 seconds ago             xenodochial_kapitsa
⚠️ Os parâmetros <flags>? e <argumentos>? são opcionais (o que é sinalizado pelo uso de ?), porém vamos aprender seu uso mais adiante.

Recapitulando 🧠
Vamos entender passo-a-passo tudo o que aconteceu durante a execução do comando anterior:

Pedimos para o Docker criar um novo container, baseado na imagem chamada alpine, usando a tag 3.14 e passando os argumentos echo e "Hello World";
O Docker verifica se já temos esta imagem, com esta tag, no disco da máquina;
Se a imagem não é encontrada, o Docker imprime na tela a mensagem Unable to find image 'alpine:3.14' locally e começa a baixar a imagem do Docker Hub;
Com a imagem e a tag presentes no disco da máquina, o Docker cria um processo isolado e utiliza a imagem Docker como o “disco” base para este processo;
Como estamos subindo este container passando os argumentos echo e "Hello World", o comportamento padrão da imagem alpine é executar este comando. Por isso, nós vemos a saída Hello World no terminal!
Ao executar o comando docker ps -a, verificamos que o container foi criado, porém ele já terminou sua execução e ficou com o status Exited.
Curiosidade: a imagem alpine é uma imagem Docker especial, pois é muito pequena (apenas 5.59MB) e já possui os comandos básicos de uma distribuição Linux. Nos próximos exemplos abaixo vamos utilizar bastante essa imagem por ser pequena e prática de usar!

⚠️ Atenção: veja que o Docker atribuiu um nome aleatório para o nosso container. O Docker segue a seguinte regra para dar um nome a um novo container: <adjetivo>_<nome>. Entretanto, podemos utilizar a flag --name <nome-da-sua-escolha> para dar um nome específico ao container criado, em vez de obter um nome aleatório dado pelo Docker.

Veja um exemplo abaixo onde nós utilizamos a flag para dar o nome meu-container para o novo container que desejamos executar:

Copiar
pessoa@trybe:~/course$ docker container run --name meu-container alpine:3.14 echo "Hello World 2"
Hello World 2!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                 CREATED          STATUS                      PORTS     NAMES
6b3491ce9502   alpine:3.14   "echo 'Hello World 2'" 11 seconds ago   Exited (0) 11 seconds ago             meu-container
52712fa829f0   alpine:3.14   "echo 'Hello World'"   2 minutes ago    Exited (0) 2 minutes ago              xenodochial_kapitsa
Perceba que o container do exemplo anterior chamado xenodochial_kapitsa não foi removido, mesmo que sua execução já tenha sido encerrada. Este é o comportamento padrão do Docker, pois ao terminar a execução, o container ainda permanece disponível para ser executado novamente.

Você pode remover os containers exemplificados acima usando o comando docker rm <nome-do-container>.

📝 Anote ai: um container só pode ser removido com o comando docker rm <nome-do-container> se ele estiver parado ou tiver sua execução terminada**.

Vamos remover os dois containers mostrados anteriormente e verificar a lista de containers novamente:

Copiar
pessoa@trybe:~/course$ docker rm xenodochial_kapitsa
xenodochial_kapitsa
pessoa@trybe:~/course$ docker rm meu-container
meu-container
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                 CREATED          STATUS                      PORTS     NAMES
Note que a lista de containers está está vazia agora!

Modo “auto-remover”
Este modo é útil para testar várias imagens Docker sem ficar com uma lista de containers parados. A flag --rm indica para o Docker que desejamos que um container seja removido ao final da sua execução. Veja abaixo um exemplo do uso da flag:

Copiar
pessoa@trybe:~/course$ docker container run --rm alpine:3.14 echo "Hello World 3"
Hello World 3!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
Perceba que após criar um container com a imagem alpine:3.14 e executar o comando de listar os containers (com a flag -a), não há nenhum container atualmente na máquina. Isso significa que o container criado pelo comando docker run executou, terminou sua execução e o Docker já fez a remoção deste container automaticamente.

⚠️Importante: a flag --rm vai remover apenas o container! A imagem alpine:3.14 ainda estará presente na máquina. Podemos confirmar isso executando o comando docker images. Veja abaixo a saída ao executar os três comandos em sequência:

Copiar
pessoa@trybe:~/course$ docker container run --rm alpine:3.14 echo "Hello World 4"
Hello World 4!
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
pessoa@trybe:~/course$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
alpine       3.14      e04c818066af   2 weeks ago    5.59MB
Modo “segundo plano”
A flag -d ou --detach faz com que a execução do container ocorra em segundo plano, ou seja, embora não esteja visível, o container executará de forma assíncrona. Esta opção é interessante quando o programa a ser executado é um servidor ou algum processo que você sabe previamente que terá uma execução demorada.

Veja abaixo a saída ao executar um container no modo detached. Neste exemplo, trocamos o argumento echo pela execução do programa sleep, que fará com que o container continue sua execução por 300 segundos (5 minutos):

Copiar
pessoa@trybe:~/course$ docker container run --rm -d alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3e
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
81e61d38ca40   alpine:3.14   "sleep 300"   12 seconds ago   Up 12 seconds             amazing_thompson
Perceba que ao executar o comando docker ps para visualizar os containers em execução atualmente, vemos nosso novo container executando o comando sleep 300. Porém, o container está sendo executado em segundo plano, por isso ele não travou a utilização do nosso terminal pelo uso da flag -d.

Para forçar a parada de execução do container acima, podemos usar o comando docker stop <nome-do-container>. Este comando força o container a terminar sua execução atual. Veja a seguir a saída ao executar o comando, usando o nome do container que obtivemos no exemplo acima:

Copiar
pessoa@trybe:~/course$ docker container run --rm -d alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3e
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
81e61d38ca40   alpine:3.14   "sleep 300"   12 seconds ago   Up 12 seconds             amazing_thompson
pessoa@trybe:~/course$ docker stop -t 0 amazing_thompson
amazing_thompson
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
Curiosidade: o comando docker stop envia um pedido educado (chamado internamente de SIGTERM) ao container para que ele tenha tempo de encerrar tudo o que precisa antes de parar sua execução de fato. Entretanto, o comando sleep que estamos utilizando ignora esse pedido educado do Docker. Para que o pedido seja forçado (chamado internamente de SIGKILL), vamos utilizar a flag -t 0.

Pronto! Conseguimos forçar a paralisação de um contêiner de segundo plano utilizando o comando docker stop.

Mas e se quiséssemos nos conectar no terminal dentro do container, enquanto ele está em execução? 🤔

Para isso, vamos conhecer os comandos avançados do Docker! 🐋

Comandos avançados no Docker
Acessando o terminal do container
O Docker nos permite executar um comando dentro de um container que já está em execução, isso é muito útil, pois nos ajuda a encontrar problemas durante a execução dos nossos projetos.

Nós vamos utilizá-lo para executar o programa sh, que nos permite simular um acesso de terminal dentro do container que já está em execução! Legal, né?

Vamos utilizar o comando docker exec -it <nome-do-container> <comando-a-ser-executado>, testando o acesso ao terminal com o mesmo exemplo de container criado anteriormente:
Copiar
pessoa@trybe:~/course$ docker container run --rm -d --name meu-container alpine:3.14 sleep 300
81e61d38ca40cb4707f44d9aba8c803c23ab4a45c23a83c55278eace2b345c3
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
99ee42188fa7   alpine:3.14   "sleep 300"   14 seconds ago   Up 13 seconds             meu-container
pessoa@trybe:~/course$ docker exec -it meu-container sh
/ # ps aux
PID   USER     TIME  COMMAND
    1 root      0:00 sleep 300
   14 root      0:00 sh
   20 root      0:00 ps aux
/ # exit
pessoa@trybe:~/course$ docker stop -t 0 meu-container
meu-container
pessoa@trybe:~/course$ docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS          PORTS     NAMES
Recapitulando 🧠
Vamos entender passo a passo o que aconteceu nos comandos anteriores:

1 - Criamos um novo container a partir da imagem alpine, com a tag 3.14:

No modo detached (-d);
Atribuindo o nome de meu-container (--name);
Solicitando sua remoção após finalização (--rm);
Substituindo o comando padrão para um comando customizado (sleep 300).
2 - Verificamos a lista de containers usando docker ps, apenas para validar o sucesso do comando anterior:

Executamos o comando docker exec -it meu-container sh;

Passando a flag -t e solicitando a criação de uma sessão de terminal;
Passando a flag -i, necessária para que a sessão seja interativa;
O comando a ser executado será sh, que é um programa de terminal linux.
3 - Já dentro do container, executamos um comando ps aux:

Este comando lista todos os processos em execução no momento;
Veja que legal: Dentro do container, os únicos processos em execução são:
sleep 300, que especificamos na inicialização do container;
sh, que especificamos na hora de abrir a sessão interativa;
ps aux, que acabamos de executar para obter esta lista;
É só isso! Dentro do container, não existe mais nenhum outro processo em execução! Aqui temos a confirmação do isolamento dos containers do resto dos processos da nossa máquina!
4 - Usamos o comando exit para sair do terminal do container;

5 - Forçamos a parada de execução do container usando o comando docker stop;

6 - Validamos que não há nenhum container restante na máquina usando docker ps -a.

Ainda não ficou nítido? Confira na figura abaixo ilustrando a relação entre o comando e a execução do comando no container.

docker-exec
Passos do Docker durante a execução de um comando.
Ver os logs de um container em execução
Quando executamos um novo container no modo detached, isto é, em segundo plano, nós deixamos de ver as informações (logs, erros, etc) que o programa está executando. Entretanto, o Docker oferece um comando para que a gente possa ver essas informações sem precisar se conectar diretamente ao terminal do container.

O comando é o seguinte: docker logs <flags> <nome-do-container>. Vamos ver um exemplo de saída deste comando:
Copiar
pessoa@trybe:~/course$ docker container run -d --name meu-container alpine:3.14 date
b89b81f17d0cb19edfcfae94d13f3b6dc0953d7cd9b1aaf0dbf4680d1d9b75ee
pessoa@trybe:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND   CREATED         STATUS                    PORTS     NAMES
b89b81f17d0c   alpine:3.14   "date"    2 seconds ago   Exited (0) 1 second ago             meu-container
pessoa@trybe:~$ docker logs meu-container
Tue Apr 26 13:29:32 UTC 2022
pessoa@trybe:~$ docker rm meu-container
meu-container
pessoa@trybe:~$
Ainda não ficou nítido? Confira na figura abaixo ilustrando a relação entre o comando e a obtenção dos logs do container.

docker-logs
Passos do Docker durante a obtenção dos logs.
Recapitulando 🧠
Vamos entender passo a passo o que aconteceu nos comandos anteriores:

1 - Criamos um novo container a partir da imagem alpine, com a tag 3.14:

No modo detached (-d);
Atribuindo o nome de meu-container (--name);
Substituindo o comando padrão para um comando customizado (date).
2 - Verificamos a lista de containers usando docker ps, apenas para validar o sucesso do comando anterior:

A saída do comando mostra que o container já parou sua execução;
Porém, ainda podemos ver os logs de um container parado sem problemas.
3 - Executamos o comando docker logs meu-container:

Não especificamos nenhuma flag.
4 - É exibido na tela a mensagem Tue Apr 26 13:29:32 UTC 2022, que é a saída do comando date, feito dentro do container.

5 - Após isso, removemos o container usando o comando docker rm.

Monitorando os processos dentro de um container
O comando docker top, assim como nos terminais Linux, traz as informações sobre os processos que estão sendo rodados dentro do container, o que não inclui, por exemplo, serviços que são compartilhados com o sistema hospedeiro.

O comando a seguir é útil para quando estamos os rodando em segundo plano:

Copiar
gabriel@trybe:~$ docker container run -d --rm --name meu-container alpine:3.14 sleep 300
6942640dda0e7d5e3db3fb122ab2e6c77f0d4bcf75b8c1082143cedf8215a193
gabriel@trybe:~$ docker top meu-container
UID      PID     PPID     C     STIME     TTY   TIME       CMD
root     5299    5278     0     09:35     ?     00:00:00   sleep 300
gabriel@trybe:~$ docker stop -t 0 meu-container
meu-container
Recapitulando 🧠
**Vamos entender passo a passo o que aconteceu nos comandos anteriores:

1 - Criamos um novo container a partir da imagem alpine, com a tag 3.14:

No modo detached (-d);
Solicitando sua remoção após finalização (--rm).
Atribuindo o nome de meu-container (--name);
Substituindo o comando padrão para um comando customizado (sleep 300);
2 - Verificamos a lista de processos do container usando docker top:

A saída do comando mostra que existe apenas um processo em execução, que é o processo que especificamos.
3 - Forçamos a parada do container usando o comando docker stop.

Limpando containers que não estão sendo utilizados
O comando docker container prune remove todos os containers inativos do seu computador. Além disso, ele pede uma confirmação para executar a operação e no final mostra a quantidade de espaço em disco recuperado. Veja um exemplo de saída do comando abaixo:

Copiar
pessoa@trybe:~/course$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
ed2aa643a36af0d3805812a6114e6da1a339f8059e373246270f0446c20f2f7f
[várias linhas]
108085a4660a7e69d1625503f0b078ecc94155edf4b2023796eadad35f1e65f6

Total reclaimed space: 442B
pessoa@trybe:~/course$
Utilizando os comandos do CLI na prática
Depois de aprender tantos comandos, chegou a hora de praticar! 

$ docker container run Hello-world

$ docker container run <imagem>:<tag>

$ docker container run ubuntu 

$ docker container run ubuntu echo 'Olá Tribers!'

$ docker container ps 

$ docker constainer ps -a 

$ docker container run ubuntu echo 'Ola mundo!'

$ docker container ps -l  

$ docker container start id_docontainer

$ docker container stop id_container

Removendo todos os containers 
$ docker container prune   // deleta todos os containers 

removendo um container 
$ docker container rm -f 

Rodando um container 
$ docker container rum -it -d ubuntu

Verificando o container 
$ docker container ls 
Removendo um container pelo iD
$ docker container rm -f id_Container 

Verificando se foi removido o container 
$ docker container ls -a

Criando um container e dando nome para ele:
$ docker container run --name hello-trybe ubuntu

Removendo um container pelo nome 

$ docker container rm hello-trybe

Verificando se o container foi removido

$ docker container ls -a

Revisão dos conceitos
Quanta coisa nova sobre Docker em apenas um dia de conteúdo!

Para te ajudar, vamos revisar todos os nomes e conceitos que aprendemos hoje:

Docker: conjunto de ferramentas (Daemon, API, CLI) para gerenciar imagens e containers.

Arquivo Dockerfile: arquivo com linguagem própria, com os passos necessários para criar uma nova imagem Docker usando o código-fonte de um projeto.

Imagem Docker: é o projeto “compactado”, que foi construído de acordo com os passos contidos no arquivo Dockerfile. Pode ser usado como base para criar novas imagens Docker.

Container: é a execução de projeto através da sua imagem Docker já construída anteriormente.

Registry: é o local remoto onde podemos enviar e baixar imagens Docker. Um registry pode ser público ou privado.

Docker Hub:

É o registry oficial da empresa Docker Inc.
Ele é público, porém possui alguns limites.
É possível assinar o serviço para utilizá-lo como registry privado.

 




