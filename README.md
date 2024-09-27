# Tutorial: Importar Repositório, Executar Testes e Gerar Relatório no GitHub Actions

Neste tutorial, você aprenderá como importar um repositório do GitHub que contém testes JMeter, executar esses testes usando GitHub Actions e gerar um relatório.

## Pré-requisitos

1. **Conta no GitHub**: Você precisa de uma conta no GitHub.
2. **JMeter Test Plan**: O repositório deve conter um arquivo `.jmx` com um plano de teste JMeter.

## Passo 1: Importar o Repositório

1. **Acesse o GitHub**: Vá para [GitHub](https://github.com/iuricdq/projetopassagem.git).
2. **Localize o Repositório**: Encontre o repositório que você deseja importar. Isso pode ser um repositório público ou um privado ao qual você tenha acesso.
3. **Fork do Repositório**:
   - Clique no botão **Fork** no canto superior direito da página do repositório.
   - Isso criará uma cópia do repositório na sua conta do GitHub.

## Passo 2: Clonar o Repositório (opcional)

Se você deseja fazer modificações localmente:

1. **Abra o Terminal**.
2. **Clone o Repositório**:
   ```bash
   git clone https://github.com/iuricdq/projetopassagem.git
   cd nome-do-repositorio


## Passo 3: Configurar o GitHub Actions
Verifique o Workflow:

Navegue até a pasta .github/workflows no seu repositório.
Confirme se existe um arquivo de workflow YAML (por exemplo, ci.yml) com a seguinte configuração
        ```bash
            
            name: CI
        
        on:
          push:
            branches: [ "main" ]
          pull_request:
            branches: [ "main" ]
          workflow_dispatch:
        
        jobs:
          build:
            runs-on: ubuntu-latest
        
            steps:
              # Checkout do repositório
              - name: Checkout repository
                uses: actions/checkout@v4
        
              # Execute os testes JMeter
              - name: Run JMeter Tests
                uses: rbhadti94/apache-jmeter-action@v0.5.0
                if: always()
                with:
                  testFilePath: teste/CompraPassagem90thPercentil.jmx
                  outputReportsFolder: reports/
                  args: "--loglevel INFO -JMyProperty=Value --jmeterlogconf=log.conf"
                  plugins: "tilln-junit"
        
              # Fazer upload dos relatórios como artefatos
              - name: Upload JMeter reports
                uses: actions/upload-artifact@v3
                with:
                  name: jmeter-reports
                  path: reports/
### Ajuste o Caminho do Arquivo: Certifique-se de que testFilePath aponta para o local correto do seu arquivo .jmx.


#Passo 4: Executar o Teste
Faça um Push para a Branch main:

Se você fez alterações localmente, faça commit e push para a branch main.
        '''bash
        
            
        git add .
        git commit -m "Configurar testes JMeter"
        git push origin main

## Passo 4:Executar Manualmente (Opcional):

-  1 Vá para a aba Actions no seu repositório.
-  Clique no workflow desejado e, em seguida, clique no botão Run workflow.

  
##  Passo 5: Visualizar os Resultados
-  Acesse a aba Actions: No seu repositório, clique na aba Actions.
-  Selecione o Workflow: Clique na execução que você deseja verificar.
-  Visualize os Relatórios:
-  Na seção "Artifacts", você verá os relatórios gerados.
-  Clique no link para baixar e visualizar os relatórios JMeter.


# Tutorial: Executar Teste JMeter Localmente

Neste tutorial, você aprenderá como baixar o arquivo `teste/CompraPassagem90thPercentil.jmx`, executar o JMeter localmente e instalar o plugin `jmeter-junit-reporter`.

## Passo 1: Pré-requisitos

1. **Apache JMeter**: Certifique-se de que o JMeter está instalado na sua máquina. Você pode baixar a versão mais recente em [JMeter Downloads](https://jmeter.apache.org/download_jmeter.cgi).
2. **Java JDK**: O JMeter requer o Java JDK instalado. Verifique se você tem o Java instalado executando `java -version` no terminal.

## Passo 1: Baixar o Arquivo de Teste

1. **Clone o Repositório** (ou baixe o arquivo diretamente):
   - Se você tiver Git instalado, execute o seguinte comando no terminal para clonar o repositório:

     ```bash
     git clone https://github.com/iuricdq/projetopassagem.git

- Navegue até o diretório clonado

     ```bash
     cd nome-do-repositorio
- Se preferir, você pode baixar o arquivo diretamente do repositório. Acesse o arquivo teste/CompraPassagem90thPercentil.jmx e clique em "Raw". Em seguida, salve o arquivo no seu computador.

## Passo 2: Instalar o Plugin jmeter-junit-reporter
- Baixar o Plugin:

- Acesse a página do plugin no [JMeter Plugins](https://jmeter-plugins.org/).
- Baixe o arquivo JAR do plugin jmeter-junit-reporter.
- Instalar o Plugin:

- Coloque o arquivo JAR do plugin na pasta lib/ext do diretório de instalação do JMeter. Por exemplo:
- C:\apache-jmeter-x.y\lib\ext (Windows)
- /home/usuario/apache-jmeter-x.y/lib/ext (Linux/Mac)

## Passo 3: Executar o Teste JMeter
- Inicie o JMeter:

- Navegue até o diretório de instalação do JMeter e inicie o JMeter executando o arquivo jmeter.bat (Windows) ou jmeter (Linux/Mac).
    '''bash
       
      cd /caminho/para/apache-jmeter-x.y/bin
      ./jmeter  # Linux/Mac
      jmeter.bat  # Windows
      Abrir o Arquivo de Teste:

- No JMeter, vá em File > Open e selecione o arquivo CompraPassagem90thPercentil.jmx que você baixou.
  

### Executar o Teste:

Clique no botão Iniciar (o botão verde) na barra de ferramentas para começar a execução do teste.
Visualizar os Resultados:

Após a execução do teste, você pode visualizar os resultados utilizando o plugin jmeter-junit-reporter ou o View Results Tree para verificar as respostas.








   
