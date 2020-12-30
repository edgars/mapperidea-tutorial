# Instalando o Mapperidea

Este é um Gist/Post que mostra como instalar o Mapperidea e rodá-lo pela primeira vez.

## Instalando Node, NPM e NVM

Eu recomendo você instalar os seguintes módulos em sua máquina:

 - node (o principal)
 - npm (sem ele, você não vive no mundo node.js)
 - nvm (para que você tenha liberdade de ambientes e versões do mundo node)

### Instalando o  mapperidea-cli
A CLI é o principal para você poder usar a plataforma. Para poder instalar em sua máquina digite: 

    npm install -g mapperidea-cli

ps- Claro que você terá que ter os pré-requisitos acima. 

Para testar a instalação, digite o seguinte comando: 

    mapperidea -h

Você deverá ter mais ou menos o mesmo output abaixo:

    Usage: mapperidea [options] [command]
    
    Mapperidea CLI
    
    Options:
      -V, --version                                                         output the version number
      -h, --help                                                            output usage information
    
    Commands:
      authorize|a <email> <machine>                                         Authorize this machine to use your mapperidea user
      init|i <project> <mainMindMap>                                        Initialize and register a Mapperidea project
      push|p <project>                                                      Push maps to mapperidea cloud
      generate|g <project> <language> <generator> [generatorParameters...]  Generate output for that project using declared language and generator, with optional parameters

## 1- Registrando seu usuário
Você precisa registrar seu usuário e máquina, para isso você utilizará o comando *mapperidea register*, no caso, eu usei o seguinte: 

    mapperidea authorize edgar@skalena.com mac2020

Com isto, meu ambiente local agora é capaz de fazer push de projetos para o serviço central (SaaS) do mapperidea, além de poder receber os códigos gerados. 

## 2- Criando seu primeiro projeto
Para fins de demonstração, nós iremos gerar nossos Swaggers das APIs (contratos), ou seja, este será nosso template. 
Crie a seguinte estrutura de diretórios:

    projeto_helloworld
    ├── mdm (pasta onde você guardará seus mapas mentais)
    │   └── io.mapperidea.samples.mm
    └── src (onde serão gerados seus códigos)

Com a estrutura acima, estamos prontos a baixar o exemplo de mapa mental io.mapperidea.samples.mm , que contém o gerador para Swagger de estrutura de classes/dados. 
    
## 3 - Configurando a Ferramenta de Mapas Mentais
Para usar o mapperidea, você tem duas opções:

 - Freemind - http://freemind.sourceforge.net/wiki/index.php/Download
 - Freeplane - https://www.freeplane.org/wiki/index.php/Home 

Particularmente, eu preferi o freeplane, por parecer estar com o desenvolvimento mais ativo. Ambas ferramentas são gratuitas e opensource.  A única coisa que você precisará para desenvolver com mapperidea é uma ferramenta de Mapas Mentais, que no final das contas, irá criar as definição usando semântica XML como padrão de escrita dos arquivos. 

Por favor, instale uma delas, mas este tutorial irá seguir o Freeplane.

### Configurando a Iconografia

O mapperidea, traz uma idéia de você representar suas idéias e o tipo dos artefatos através de ícones, ou seja, cada ícone representa algo, no caso, o artefato que você quer gerar.  

1. Vamos baixar a biblioteca de ícones que você irá precisar daqui deste link: https://static.academy.mapperidea.io/mapperideaIcons.zip , por favor, descompacte este arquivo e observe o passo 2.
2. Com o Freeplane já instalado e aberto, vá em **Tools -> Open user directory** e abra a opção “freeplane_userdir”. Copie todos os ícones do ***passo 1*** para a pasta *icons*, se esta página não existir a crie por favor. 
3. Reinicie o Freeplane (feche-o e abra-o novamente). 

Para mais dicas, acesse este link: https://docs.mapperidea.io/ref-guide/en/functions/miscellaneous/tips/tips.html 

### Abrindo o mapa de exemplo

Faça o download do mapa de exemplo deste link: https://github.com/edgars/mapperidea-tutorial/blob/master/mdm/io.mapperidea.samples.mm (Salvar Arquivo como), e copie o mesmo para a pasta **mdm** de seu projeto. A nossa estrutura estará agora desta maneira:

    projeto_helloworld
    ├── mdm (pasta onde você guardará seus mapas mentais)
    │   └── io.mapperidea.samples.mm (<----)
    └── src (onde serão gerados seus códigos)

Ao abrir o mapa mental, você verá uma estrutura assim:

![mapa mental - exemplo](https://github.com/edgars/mapperidea-tutorial/raw/master/img/figura1.png)

Neste mapa, observe primeiramente apenas as primeiras estruturas filhas:

    io.mapperidea.samples
    ├── config --> Aqui são as configurações gerais do mapa
    └── domain --> Aqui são os objetos que você irá usar como mapas para gerar códigos

Quando você observa a parte de `domain/company` você pode observar 3 entidades: 

 -  Company
 - CompanyType
 - CostCenter

Estas 3 entidades, podem dar origem a qualquer artefato gerado, para esta demonstração, iremos mostrar como gerar um Swagger na forma mais correta possível. 

#### Geradores
Uma das configurações de `config`, são os geradores, que podem estar criados no próprio mapa mental, ou podem ser refereciados externamente (outra arquivo).  Em nosso exemplo, temos 2 geradores: 

 - restAPI
 - listPackages
 - 
Veja abaixo:

![geradores](https://github.com/edgars/mapperidea-tutorial/raw/master/img/figura2.png)

Um dos conceitos mais interessantes do mapperidea é a disponibilização de `templates`, a idéia é um momento no futuro ter um marketplace tão rico quanto ***Wordpress*** possui de seus temas e plugins. 

## 4- Gerando código

Primeiro passo: Initializar o projeto, como se fosse mais uma vez o git, você irá fazer isto de dentro da pasta `mdm`. 

    mapperidea init projeto_helloworld io.mapperidea.samples.mm
    
O resultado será:

    Project projeto_helloworld configured:
          with main mind map: io.mapperidea.samples.mmm
          located at home folder: ./projetos/projeto_helloworld/mdm

O segundo passo para gerar os códigos é fazer o "push" do seu projeto para o motor em nuvem do mapperidea, para isso você utilizará o seguinte comando, dentro da pasta `mdm`.

    mapperidea push projeto_helloworld io.mapperidea.samples.mm

`resposta: Project projeto_helloworld not initialized!`

    Map structure pushed!

Com isto, o mapperidea (mas ou menos como o git), saberá que você está está trabalhando com o mapa mental `io.mapperidea.samples.mm` com um projeto chamado `projeto_helloworld`.

Vamos até o diretório src, que está no mesmo nível do mdm, e digite o seguinte comando:

    mapperidea generate projeto_helloworld swagger listPackages > genApi.sh
                        [nome projeto  ] [linguagem] [generator] > arquivo de saída

![geradores](https://github.com/edgars/mapperidea-tutorial/raw/master/img/figura3.png)

Dentro da pasta src, será gerado o seguinte arquivo: `genApi.sh` (se usar Windows, por favor, use/renomeie para .bat ).

Depois do chmod a+x no arquivo, pode executar o arquivo `./genAPI.sh`:

O resultado irá criar o seu arquivo .yaml com a definição do Swagger. 

## 5 - Resultado

Veja o Swagger gerado:

![geradores](https://github.com/edgars/mapperidea-tutorial/raw/master/img/figura4.png)

## Testando no 42Crunch 

 - [ ] To-Do - Para ser atualizado

## Conclusão

Gostou? Peça seu trial em https://mapperidea.io 





