# kedrominiclass
Uma miniclass para a utilização do Kedro

## Instalando o Kedro

```pip install kedro==0.18.1```

**A versão não precisaria ser especificada, mas a 0.18.2 saiu dia 08/07/22 e portanto estava conflitando com os kedro starters.

## Inicializando um projeto Kedro

Você pode inicializar um projeto Kedro de duas formas:

> kedro new

ou 

> kedro starter

### Inicializando do zero

Ao optar pela opção kedro new, a única pergunta realizada no terminal é pelo nome do projeto.

1. Defina o nome do seu projeto e pressione enter

> kedro_miniclass

2. Defina o nome do repositório (ou pode apenas pressionar enter para manter o mesmo)
3. Defina o nome do pacote python (também pode apenas dar enter para manter o mesmo)

Você verá que uma nova pasta será criada e ela terá a seguinte estrutura:

kedro_miniclass
    - conf
    - data
    - docs
    - logs
    - notebooks
    - src
    .gitignore
    pyproject.toml
    README.md
    setup.cfg

Isso é o que chamamos de scaffolding, uma forma de criar um esqueleto inicial para o projeto, e com isso vem alguns benefícios:

- Uma estrutura geral é criada
- Já vem em formato de lib python possível de ser instalada, por exemplo.
- Traz artifícios para se criar uma documentação usando o sphinx.
- Permite que as configurações fiquem isolada do código.

### E se eu tivesse inicializado com um kedro starter?

> kedro starter list

Starters from kedro

```astro-airflow-iris:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: astro-airflow-iris
astro-iris:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: astro-airflow-iris
pandas-iris:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: pandas-iris
pyspark:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: pyspark
pyspark-iris:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: pyspark-iris
spaceflights:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: spaceflights
standalone-datacatalog:
  template_path: git+https://github.com/kedro-org/kedro-starters.git
  directory: standalone-datacatalog
  ```


Vamos selecionar o de spaceflights para brincarmos.

> kedro new -s spaceflights

1. Defina o nome do projeto, repositório e pacote python
> kedro_miniclass_spaceflights

Com isso, a mesma estrutura acima será criada, mas com o benefício de ter dados já criados do dataset spaceflights.

## Estrutura funcional do Kedro

A arquitetura do kedro pode ser encontra pode ser vista conforme abaixo:

<img src="https://kedro.readthedocs.io/en/stable/_images/kedro_architecture.png" />

É composta em cinco partes:

- Um projeto Kedro, que contém:
    - Um diretório conf/, que contém arquivos de configuração do projeto, como data catalog, parametros, etc.
    - Um diretório src/, que contém o código fonte do projeto, o que inclui:
        - Um diretório de pipelines
        - Um arquivo settings.py que contém configurações como hooks customizados, addons e demais opções de customização avançada
        - **pipeline_registry.py**, um arquivo que define os pipelines do projeto, para que sejam executados pelo kedro run --pipeline.
        - **__main__.py**, arquivo que serve como entrypoint do projeto no modo pacote python.
    - Um arquivo **pyproject.toml**, identifica o projeto com metadados como:
        - package name
        - project name
        - project version

- Kedro starters:
    Projetos pré empacotados para experimentação e aprendizado do framework Kedro.

- Kedro library:
    A biblioteca consiste em quatro unidades independentes para seu funcionamento, cada uma responsável por uma parte na execução do pipeline:
    - **Config Loader** provê a capacidade de efetuar o parsing e carregamento das configurações definidas no projeto.
    - **Pipeline** traz consigo uma coletanea de abstrações para modelar data pipelines.
    - **Runner** fornece tipos de estratégia diferentes para executar o pipeline.
    - **I/O** provê uma coleção de abstrações para lidar com o I/O do projeto, incluindo o DataCatalog, e muitas implementações de dataset.

- Kedro framework:
    O framework atua como interface entre o projeto e a Kedro library. Consiste em quatro peças:
    - Session - gerencia o ciclo de vida do kedro run.
    - Context - guarda a configuração e a principal funcionalidade do Kedro, também servindo como ponto de entrada de interação com componentes core da biblioteca. (É onde se costuma aplicar um contexto customizado do Spark, por exemplo)
    - Hooks - define as especificações de hooks disponíveis
    - CLI - define os comandos padronizados da Kedro CLI, e funcionalidades para carregar comandos de CLI customizados.

- Kedro extension:
    Addons customizados criads pela comunidade do Kedro, tal como o Kedro Viz que permite visualizar seus pipelines de uma forma bonita.



