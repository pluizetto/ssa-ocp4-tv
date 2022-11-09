# ssa-ocp4-tv
SManager Solution Architects - OpenShift 4 - Test Drive

## Instruções - Test Drive OpenShift 4:
   -
   -
   -
   -

## Pré-requisitos:
   
   - Crie um fork, utilizando a sua própria conta do Github, do repositório a seguir (não este que contém os exércicios): https://github.com/pluizetto/ruby-hello-world

   -
   -
   -
   -
   -
   




## 1 - Explorando o ambiente:

   - Console
   - Perfil dev
   - Perfil admin

## 2 - (Instrutor) Liberação de Acesso - Projetos individuais
  
  - (Participantes) Acessar o perfil de desenvolvedor e aguardar a liberação do seu projeto (namespace). 

## 3 - Explorando o CLI:

 #### Comandos:
 
      $ oc project
      $ oc projects
      $ oc get pods
      $ oc get nodes

## 4- Deploy da aplicação com Pipeline:

1. Altere para o perfil de desenvolvedor
2. Selecione o menu +Add;
3. Valide que o projeto está selecionado ao lado direito do perfil de desenvolvedor ("Project: namespace-xyz");
4. Clicar em "**Git Repository > Import from Git**";
5. Preencha os dados solicitados:
      - No campo **Git Repo URL:** insira a url do seu projeto GitHub;
      - Clique em **Show advanced Git options** e insira no campo **Git Reference:** master
      - Em **Appplication name** e em **Name**, altere os valores para: app-$(número do seu projeto)
      - Marcar o checkbox **Add pipeline**;
      - Desmarcar o checkbox **Create a route to the Application**;
      - Cilcar em **Resource limits**;
      - No formulario que será aberto, preencha com os seguintes valores:
         - CPU -> Request = 20 milicores;
         - CPU -> Limit = 50 milicores;
         - Memory -> Request = 70 Mi;
         - Memory -> Limit = 150 Mi;
      - Clique no botão "Create";
      - Aguarde o processo de construção (build) e escalação da aplicação (0 para 1). Acompanhe os logs da execução em: **Pipelines > app-$(número do seu projeto)** > PipelineRuns > app-$(número do seu projeto)-xyz > Logs**;
      - Clique em **Topology** ;
      - Clique em cima do circulo azul da sua aplicação **app-$(número do seu projeto)**;
      - Explore as opções apresentadas (Details, Resources, Observe);
           
## 5 - Crie uma rota HTTP para a aplicação:
1. Clique em **Project** no canto esquerdo do console;
2. Clique em **Route** > **Create Route**, e preencha conforme abaixo:
      - **Name**: http-app-$(número do seu projeto)
      - **Hostname**: app-$(número do seu projeto).apps.cluster-9k4xg.9k4xg.sandbox474.opentlc.com
      - **Service**: app-$(número do seu projeto)
      - **Target port**: 8080 -> 8080 (TCP)
      - Clicar em **Create**;
      - Acesse a rota em seu navegador;
      - Anote a rota em um bloco de notas;

## 6 - Crie uma rota HTTPS para a aplicação:
1. Clique em **Project** no canto esquerdo do console;
2. Clique em **Route** > **Create Route**, e preencha conforme abaixo:
      - **Name**: https-app-$(número do seu projeto)
      - **Hostname**: secure-app-$(número do seu projeto).apps.cluster-9k4xg.9k4xg.sandbox474.opentlc.com
      - **Service**: app-$(número do seu projeto)
      - **Target port**: 8080 -> 8080 (TCP)
      - Marque o checkbox **Secure Route**;
      - **TLS termination**: Edge
      - **Insecure traffic**: Redirect
      - Clicar em **Create**;
      - Acesse a rota em seu navegador;
      - Tente acessar a rota como HTTP e veja o comportamento do "Redirect";
      - Anote a rota em um bloco de notas;
      - Envie ambas as rotas (HTTP e HTTPS) no chat.

## 7- Adicionar Trigger/Webhook no Pipeline:

1. Clique em "Topology" no menu lateral, e abra a URL do POD chamado "Triggers", conforme abaixo:
<img width="1438" alt="Screen Shot 2022-03-27 at 19 39 30" src="https://user-images.githubusercontent.com/85974419/160304231-b6139533-f04f-46f9-ba55-a3e7bac45d0a.png">

2. Copie a URL;

<img width="1438" alt="Screen Shot 2022-03-27 at 19 43 51" src="https://user-images.githubusercontent.com/85974419/160304329-9ed20a35-9975-4256-9b73-ef896f9fada7.png">

3. Acesse seu repositório (repoistório clonado anteriormente), e clique nas seguintes opções: Settings -> Webhooks -> Add webhook:

<img width="1438" alt="Screen Shot 2022-03-27 at 19 50 10" src="https://user-images.githubusercontent.com/85974419/160304525-e1548a74-bbfb-422c-84cb-ceb8d14c3fa6.png">

4. No formulario que aparecerá insira a URL do Trigger no campo "Payload URL", e em "Content type" selecione a opção "aplication/json", depois clique no botão "Add webhook";

<img width="1438" alt="Screen Shot 2022-03-27 at 20 43 58" src="https://user-images.githubusercontent.com/85974419/160306378-fc15429f-6281-4c2e-88ee-a12b93a9a467.png">


## 8 - Teste de Trigger com o Webhook do GitHub:

#### Passos para teste:

Acesse seu GitHub e abra o repositório clonado para executar as tarefas abaixo.

1. Alterar o arquivo "/views/main.erb" na **linha 26**. Remova o conteúdo antes do comentário "Edite essa linha", e insira seu nome. (não remova nada antes ou depois da linha 26)

2. Após essa alteração clique no botão "commit changes";

<img width="1433" alt="Screen Shot 2022-03-28 at 12 51 23" src="https://user-images.githubusercontent.com/85974419/160437667-c55f3ac4-41c0-42d4-bc4d-41d90f9283fa.png">

3. No console do OCP, voce pode acompahar a Pipeline iniciando um novo build e deploy da nova versão da Aplicação;

<img width="1433" alt="Screen Shot 2022-03-28 at 12 54 54" src="https://user-images.githubusercontent.com/85974419/160438431-80a22fcc-81c6-44f8-9c9d-b837b3480bf8.png">

      
## 9 - Escalando a aplicação manualmente (via Web Console)

1. Clique em "Topology", depois clique dentro do círculo azul no POD da aplicação, e ao lado direito em "Details" clique no botão para subir mais uma instancia da Aplicação:

<img width="1433" alt="Screen Shot 2022-03-28 at 13 40 40" src="https://user-images.githubusercontent.com/85974419/160447055-731acc1e-5db1-4b1c-9943-612914efb0bc.png">


## 10 - Downscale manual (via Webc Console)

1. Acessar no menu lateral a opção "Topology", clique no icone do POD da aplicação e na sessão "Details" clique no botão para baixar as instancias da Aplicação:

<img width="1433" alt="Screen Shot 2022-03-28 at 13 40 40" src="https://user-images.githubusercontent.com/85974419/160447055-731acc1e-5db1-4b1c-9943-612914efb0bc.png">


## 11 - Autoscale da aplicação:

1. Acessar no menu lateral a opção "Topology", clique no icone do POD da aplicação e na sessão "Actions" clique na opcão "Add HorizontalPodAutoscaler":

<img width="1433" alt="Screen Shot 2022-03-28 at 14 05 37" src="https://user-images.githubusercontent.com/85974419/160450990-9b32debb-c508-4f97-ae16-e8407d55f76b.png">

2. Será aberto um formulario para preenchimento dos parametros, colocar os valores e clique no botão "Save" comforme imagem:

<img width="1433" alt="Screen Shot 2022-03-28 at 14 07 26" src="https://user-images.githubusercontent.com/85974419/160451001-f3d08378-cfdb-4796-ae37-28b511271396.png">


## 12 - Acessando os logs da aplicação

1. Acessar no menu lateral a opção "Topology", clique no icone do POD da aplicação e na sessão "Resources" clique no botão para baixar as instancias da Aplicação:

<img width="1433" alt="Screen Shot 2022-03-28 at 13 58 04" src="https://user-images.githubusercontent.com/85974419/160449754-b05ceaf4-a703-4c6b-8731-c433bad4f531.png">

2. Abrirá a tela de logs da aplicação:

<img width="1433" alt="Screen Shot 2022-03-28 at 13 59 49" src="https://user-images.githubusercontent.com/85974419/160449765-3848ba95-a4f4-4832-8bad-bcfa120d0f85.png">


## 13 - Teste de carga usando Apache Benchmark:

1. No menu lateral clique em "+Add" e em "All services":

![image](https://user-images.githubusercontent.com/41959558/172454062-b160fc57-b4a6-4eb3-8984-4f40c9d1dcd2.png)

2. Procure por por "httpd" e clique na primeira opção, depois em "Instantiate Template":

![image](https://user-images.githubusercontent.com/41959558/172454783-4d0505a0-88d3-4bac-b062-2fd5e433d59d.png)

3. Mude o nome para "apache-benchmark" (Apache Benchmark) e clique em "create":

![image](https://user-images.githubusercontent.com/41959558/172455323-2f129341-8468-43ae-a5f6-4434e3b79ac8.png)

4. Acesse o seu projeto (namespace) via Web Terminal, e entre no POD do Apache Benchmark. Em seguida execute o comando para disparar a carga na URL da aplicação e observe novas instâncias sendo criadas para atender a carga.

![image](https://user-images.githubusercontent.com/41959558/172460826-c8f57d43-b1f1-4441-a467-af594bb9bdbd.png)


