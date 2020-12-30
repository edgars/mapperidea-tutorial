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
    


