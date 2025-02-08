# Laboratório 2: Amazon EC2 e Armazenamento EBS

**Curso:** Preparatório para o exame AWS Solutions Architect Associate (C03)


**Instituição:** [Escola da Nuvem](https://escoladanuvem.org/)

**Turma:** DPCN07 - JAN/2025

**Professora:** [Josely Castro](https://www.linkedin.com/in/joselybcastro)

## [Veja os prints do laboratório](#prints) 🔥

---

## Objetivo  
Trabalhar com instâncias EC2 e volumes EBS, aprendendo a criar, configurar e gerenciar esses recursos.

---

## Cenário  
Você precisa provisionar um servidor web simples na AWS. Para isso, você criará uma instância EC2, adicionará um volume EBS para armazenar os dados do site e configurará backups automáticos para garantir a segurança dos dados.

---

## Pré-requisitos  
- Uma conta AWS com acesso ao console de gerenciamento.  
- Navegador web.  

---

## Tarefas  

### 1. **Provisionando a Instância EC2**  

- **Selecione a Região AWS**: `us-east-1` (Norte da Virgínia).  
- **Acesse o console do EC2**:  
  - Clique em **"Lançar instâncias"**.  
  - Selecione uma AMI (Amazon Machine Image) do **Amazon Linux 2**.  
  - Escolha o tipo de instância `t2.micro` (ou `t3.micro`, elegíveis para a camada gratuita).  
  - Configure o par de chaves para acesso SSH:  
    - Clique em **"Criar novo par de chaves"**.  
    - Nomeie o par de chaves e mantenha as configurações padrão.  
  - Em **"Configurar armazenamento"**, clique em **"Adicionar novo volume"** e configure o tamanho desejado (exemplo: **8 GB**).  
- Lance a instância.  

---

### 2. **Conectando-se à Instância EC2 via SSH**  

#### Usando o MobaXterm:  
1. Abra o MobaXterm.  
2. Clique em **"Session"** no canto superior esquerdo.  
3. Selecione **"SSH"**.  
4. Insira o endereço IP público da instância no campo **"Remote host"**.  
5. Em **"Specify username"**, digite `ec2-user` (para Amazon Linux 2).  
6. Clique em **"Advanced SSH settings"** e marque a opção **"Use private key"**.  
7. Clique em **"Browse"**, selecione o arquivo `.pem` da sua chave de par e conecte.  

---

### 3. **Preparando o Volume EBS**  

1. **Identifique o novo volume**:  
   - Execute:  
     ```bash
     lsblk
     ```  
   - Verifique o dispositivo correspondente ao seu volume EBS (exemplo: `/dev/xvdf`) e anote o nome.  

2. **Formate o volume**:  
   - Execute:  
     ```bash
     sudo mkfs.ext4 /dev/xvdf
     ```  
   - Substitua `/dev/xvdf` pelo nome do dispositivo identificado.  

3. **Crie um diretório para montagem**:  
   - Execute:  
     ```bash
     sudo mkdir /mnt/dados
     ```  

4. **Monte o volume**:  
   - Execute:  
     ```bash
     sudo mount /dev/xvdf /mnt/dados
     ```  
   - Valide a montagem:  
     ```bash
     lsblk
     ```  

---

### 4. **Gerenciando Backups do Volume EBS**  

1. **Criar um Snapshot do Volume**:  
   - No console do EC2, vá para **"Volumes"** e selecione o volume EBS.  
   - Clique em **"Ações"** > **"Criar snapshot"**.  
   - Nomeie o snapshot (exemplo: "Não apague, risco de demissão") e adicione uma tag para organização (exemplo: **"FinOps"**).  

2. **Configurar Políticas de Snapshot Automático**:  
   - Navegue até **"Snapshots"** e selecione o snapshot criado.  
   - Clique em **"Ações"** > **"Criar política de snapshot"**.  
   - Configure a política para criar snapshots automaticamente com a frequência desejada (exemplo: diariamente).  

---

### Dicas:  


• Se você precisar desmontar o volume, use o comando `sudo umount /mnt/dados`.  
• Para que o volume seja montado automaticamente a cada reinicialização da instância, você precisará editar o arquivo `/etc/fstab`. Consulte a documentação da AWS para obter instruções específicas sobre como fazer isso.  
• Lembre-se de substituir `/dev/xvdf` pelo nome real do seu dispositivo EBS.  

Acesse o console do EC2 e navegue até "Volumes":  
• Selecione o volume EBS que você criou.  
• Clique em "Ações" e selecione "Criar snapshot".  
• Dê um nome descritivo ao snapshot (ex: "Não apague , risco de demissão").  

**Obs:** Adicione uma tag para melhor organização e para ajudar o departamente de FinOps.  

Criar snapshot  
• Navegue até "Snapshots" e selecione o snapshot que você criou.  
• Clique em "Ações" e selecione "Criar política de snapshot".  
• Configure a política para criar snapshots automaticamente com a frequência desejada (ex: diariamente).  

---

### Prints

![1-ec2-launch](https://github.com/user-attachments/assets/23db8d93-a023-4821-a182-58b5818a8c46)

![2-ssh-into-ec2](https://github.com/user-attachments/assets/e50e3029-65ec-449c-8bde-79f24e81f983)

![3-xvdb](https://github.com/user-attachments/assets/8c95c0e4-98b3-4507-a226-7134e5c90ac3)

![4-create-snap](https://github.com/user-attachments/assets/50c1fc8d-b609-46cc-8ac3-66a0a9d8925d)

![5-create-snap2](https://github.com/user-attachments/assets/07180fa8-187a-44e0-9ea1-8f6cf2be320c)

![6-create-snap3](https://github.com/user-attachments/assets/07c0dd4c-d5ab-4418-be40-a9ff20e94f46)

![7-snap](https://github.com/user-attachments/assets/8db37525-15ad-46a3-a56d-c237f8d04ab8)

![create-snap-lifecycle-policy-1](https://github.com/user-attachments/assets/e02b90fc-85d2-4ff0-be9a-24b0debcc605)

![create-snap-lifecycle-policy-2](https://github.com/user-attachments/assets/d008fb26-ec52-4b2f-b03e-1f542d83d25c)

![create-snap-lifecycle-policy-2-1](https://github.com/user-attachments/assets/3a86ea39-a8ed-428e-881c-c5051ffdf2b2)

![create-snap-lifecycle-policy-3](https://github.com/user-attachments/assets/45376053-a8b9-4cf0-a0bb-6977e34470c5)

![create-snap-lifecycle-policy-4](https://github.com/user-attachments/assets/01b0785e-9c32-46c7-ac15-0939b1883d78)


Aqui vai uma sugestão:


- [Laboratório prático: Snapshots de EBS com AWS CLI e Python](https://github.com/nolascojoao/aws-ebs-snapshot-lab)
