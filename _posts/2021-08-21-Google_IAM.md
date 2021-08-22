---
layout: post
title: "Google IAM"
---

Esse é o primeiro post da séria sobre Google Cloud Platform. Serão posts que fazem parte dos meus estudos sobre a cloud do google.

Com o Identity and Access Management (IAM), os administradores autorizam quem pode realizar ações em determinados recursos.

## O que são membros?

Indo na console basta acessar o menu lateral e ir em IAM & Admin. Vamos encontrar o campo chamado de **Members (membros)**

Membros são usuários que podemos criar e visualizar certos recursos na console google cloud.

## O que são roles?

Roles são "regras" que podemos herdar/criar para cada tipo de recurso. Com as regras podemos limitar acessos ou dar acessos a determinado usuário.

Podemos visualizar as **roles** via menu lateral indo em **Roles** ou em **IAM & Admin**

## O que é a Organização?

A organização é a empresa para qual você está trabalhando nesse projeto. Podemos ter o exemplo de Organização **Sua Empresa** e ter um projeto **Projeto da Empresa**. Então os usuários terão acessos aos recursos que fazem parte do projeto e da organização.

## Criando um usuário

Para criar um usuário basta acessar IAM & Admin e clicar em Add/Adicionar, colocar o e-mail de um membro e escolher a sua role.

Podemos criar membros com vários e-mails válidos e dar a permissão nessária cada tipo de usuários como desenvolvedores, analistas de infraestrutura ou administradores de banco de dados.

Ao criar um membro podemos marcar a opção de **Enviar um e-mail de confirmação** para que o novo usuários seja notificado sobre o acesso do google cloud.

## Criando novas Regras

Quando criamos regras podemos aumentar ou limitar o acesso de um determinado usuário logado.

Podemos ter regras para usuários que só querem mexer com Google Storage ou somente para quem vai gerenciar máquinas virtuais (VM - Compute Engine)

Para criar uma regra devemos ir em IAM & Admin → Roles → +Create Role

## Laboratório 1

- Criar uma identidade com um e-mail válido
- Adicionar esse e-mail em uma role chamada de **Storage Admin e solicitar o envio de e-mail**
- Acessar o e-mail recebido e navegar pelo console do google cloud
- Busque por **Cloud Storage** e verifique se o acesso foi validado no menu de Storage
- Depois busque por **Compute Engine** e verifique se o acesso foi **negado** ao acessar o recurso.

## Laboratório 2

Nesse laboratório vamos criar uma nova regra e retirar do usuário adicionado anteriormente o poder de admin do Google Storage. Queremos que ele só tenha acesso alguns buckets/objetos.

Vamos criar uma regra chamada de **Gerenciar Storages (buckets)** com os seguintes dados:

**Title:** Gerenciar Storages (buckets)

**Description:** Regra para gerenciar buckets, criar lista buckets e objetos

**ID:** Padrão

**Role lauch Stage:** Alfa

Clicando em no botão +ADD PERMISSIONS filtre no campo **Filter permissions by role** e escreva **Storage Admin** e depois selecione a role e click **OK**

No campo **Filter** escreva um nome da propriedade ou um valor. Busque e marque a caixa de seleção de cada propriedade abaixo:

- resourcemanager.projects.get
- storage.buckets.create
- storage.buckets.getIamPolicy
- storage.buckets.list
- storage.multipartUploads.create
- storage.objects.create
- storage.objects.get
- storage.objects.getIamPolicy
- storage.objects.list
- storage.objects.setIamPolicy
- storage.objects.update

Depois de selecionar as propriedades clique no botão **SAVE**

Ao finalizar a criação da regra, devemos adicioná-la ao usuário alvo do laboratório. Onde será o usuário criado anteriormente.

Vamos novamente em IAM → ✏️ (Edit Member) → +ADD ANOTHER ROLE. Selecione a regrar **Gerenciar Storages (buckets).** Delete clicando no ícone da lixeira e depois no botão **SAVE**

Agora em uma aba anônima do seu navegador acesse o [https://console.cloud.google.com](https://console.cloud.google.com/) e coloque o e-mail e a senha de usuário cadastrado no primeiro laboratório.

Busque por Cloud Storage e localize os bucket/objetos que esse usuário herdou do projeto.
