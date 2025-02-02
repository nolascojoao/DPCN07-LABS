# Laboratório 4: Amazon S3

**Curso:** Preparatório para o exame AWS Solutions Architect Associate (C03)


**Instituição:** [Escola da Nuvem](https://escoladanuvem.org/)


**Turma:** DPCN07 - JAN/2025

## [Veja os prints do laboratório](#prints) 🔥

---

## 🎯 **Objetivo do Laboratório**
Aprender a usar os recursos de armazenamento e segurança do Amazon S3, focando em:

- **Versionamento:** Manter um histórico de versões dos arquivos.
- **Ciclo de Vida:** Automatizar a movimentação de arquivos entre diferentes classes de armazenamento.
- **URLs pré-assinadas:** Gerar links temporários para acesso seguro a objetos específicos.

---

## 🌐 **Cenário**
Você é responsável pelo armazenamento em nuvem da sua empresa e precisa garantir que os dados estejam armazenados de forma segura, organizada e com custos otimizados.

---

## 📋 **Pré-requisitos**
- **Conta AWS:** Crie uma conta gratuita, se necessário.
- **Navegador Web:** Chrome, Firefox, Edge, etc.
- **Arquivos de Teste:** Criaremos um arquivo de texto simples para os testes.

---

## 🚀 **Início do Laboratório**

### 1️⃣ **Criação do Bucket (Repositório de Arquivos)**

#### 1.1 **Acessar o console do S3**
- Faça login no Console de Gerenciamento da AWS.
- Na barra de pesquisa, digite "S3" e selecione o serviço "S3" nos resultados.

#### 1.2 **Selecionar a Região AWS `us-east-1` (Norte da Virgínia)**
- No canto superior direito do console, verifique se a região "US East (N. Virginia)" (`us-east-1`) está selecionada.  
- Caso contrário, clique no nome da região atual e escolha "US East (N. Virginia)" na lista.

#### 1.3 **Criar o Bucket**
- Na página do S3, clique no botão laranja **"Criar bucket"**.

#### 1.4 **Nome do Bucket**
- Insira um nome único globalmente para o seu bucket. Por exemplo: `joao-bucket-lab3`.  
  ⚠️ **Importante:** Os nomes de bucket devem seguir regras específicas:
  - Apenas letras minúsculas, números, pontos (.) e hífens (-).

#### 1.5 **Configurações do Bucket**
- **Região da AWS:** Mantenha **"US East (N. Virginia) us-east-1"**.
- **Propriedade do objeto:** Mantenha como **ACLs desabilitadas (recomendado)**.
- **Bloquear acesso público:** Marque a opção **"Bloquear todo o acesso público"**.
- **Versionamento de bucket:** **Desativar** (ativaremos posteriormente).
- **Criptografia padrão:** Mantenha **SSE-S3**.
- **Configurações avançadas:** Mantenha desativado.

#### 1.6 **Criar o Bucket**
- Revise todas as configurações.
- Clique no botão **"Criar bucket"**.

---

### 2️⃣ **Upload de Arquivos e Versionamento**

#### 2.1 **Acessar o Bucket**
- Na lista de buckets, encontre e clique no nome do bucket que você acabou de criar.

#### 2.2 **Criação do Arquivo de Teste (`Lab3.txt`)**
1. Vá para a Área de Trabalho do seu computador.  
2. Clique com o botão direito em uma área vazia, selecione **"Novo > Documento de Texto"**.  
3. Nomeie o arquivo como `Lab3.txt`.  
4. Abra o arquivo e digite: **"Versão 1"**.  
5. Salve o arquivo.

#### 2.3 **Upload do Arquivo para o Bucket S3**
1. Dentro do seu bucket, clique no botão **"Fazer Upload"**.  
2. Arraste e solte o arquivo `Lab3.txt` ou clique em **"Adicionar arquivos"** e selecione o arquivo.  
3. Mantenha as configurações padrão e clique em **"Fazer Upload"**.

#### 2.4 **Verificação**
- Após o upload, você verá o arquivo `Lab3.txt` listado no bucket.

#### 2.5 **Habilitar Versionamento**
1. Na aba **"Propriedades"**, encontre a seção **"Versionamento de bucket"**.  
2. Clique em **"Editar"**, selecione **"Ativar"** e salve.

#### 2.6 **Upload de uma Nova Versão do Arquivo**
1. Abra `Lab3.txt` e adicione: **"Versão 2"**.  
2. Salve e refaça o upload.

#### 2.7 **Acessar Histórico de Versões e Restaurar**
- Marque a opção **"Listar versões"** no bucket para visualizar as diferentes versões.  
- Clique na versão desejada para baixá-la.

---

### 3️⃣ **Regra de Ciclo de Vida**

#### 3.1 **Acessar a Aba "Gerenciamento"**
- Dentro do bucket, clique em **"Gerenciamento"**.

#### 3.2 **Criar uma Regra de Ciclo de Vida**
- Clique em **"Criar regra de ciclo de vida"**.

#### 3.3 **Configurar a Regra**
- Nome: `MoverParaGlacierApos30Dias`.  
- **Ações de ciclo de vida:**  
  - Transição para **Glacier Instant Retrieval** após **30 dias**.  
  - Expirar versões em **1 dia**.

#### 3.4 **Criar a Regra**
- Clique em **"Criar regra"**.

---

### 4️⃣ **URLs Pré-assinadas**

#### 4.1 **Selecionar um Objeto**
- Desmarque **"Listar versões"** para facilitar a visualização.  
- Clique em `Lab3.txt`.

#### 4.2 **Gerar uma URL Pré-assinada**
1. Clique em **"Ações" > "Compartilhar com um URL pré-assinado"**.

#### 4.3 **Configurar a Data de Expiração**
- Defina um período curto, como **1 minuto**.

#### 4.4 **Gerar a URL**
- Clique em **"Criar URL pré-assinado"**.

#### 4.5 **Copiar e Testar a URL**
- Abra a URL em uma janela anônima.

---

## ⚠️ **Observações Importantes**
- Explore as **políticas de bucket** para controle de acesso granular.
- Fique atento aos limites da **camada gratuita da AWS**.
- **Excluir Recursos:** Após concluir o laboratório, exclua o bucket e o arquivo.

---

## 🏁 **Conclusão**
Parabéns! Você aprendeu conceitos fundamentais do Amazon S3:

- **Organização:** Como os buckets funcionam como contêineres para arquivos.
- **Segurança:** A importância de bloquear acesso público e URLs pré-assinadas.
- **Proteção de Dados:** Como o versionamento permite recuperar versões antigas.
- **Otimização de Custos:** Uso de regras de ciclo de vida para movimentar dados.

---

## Prints

![1](https://github.com/user-attachments/assets/970db159-b386-4263-8271-283e66c008b3)

![2](https://github.com/user-attachments/assets/d334565b-41e6-4af9-b1e0-d9967ac1fbad)

![3](https://github.com/user-attachments/assets/f6e4212f-d1b5-4aea-b672-328fccbbe000)

![4](https://github.com/user-attachments/assets/a4f55533-a1a3-4c18-8043-aa1d791d126a)

![5](https://github.com/user-attachments/assets/94b0bcfd-a50b-4a73-91ef-8eba51a970df)

![6](https://github.com/user-attachments/assets/8bcd04fd-c434-476c-8638-2d332e843f2b)

![7](https://github.com/user-attachments/assets/f756b5c2-2b78-42b7-b0c4-7dc1812a00db)

![8](https://github.com/user-attachments/assets/f8e7ca0a-d0b2-48a5-9c1c-857264e221a1)
