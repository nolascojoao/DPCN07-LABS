# Laboratório 3: VPC

**Curso:** Preparatório para o exame AWS Solutions Architect Associate (C03)


**Instituição:** [Escola da Nuvem](https://escoladanuvem.org/)


**Turma:** DPCN07 - JAN/2025

---

## Objetivo  
Criar uma VPC funcional com uma sub-rede pública e uma privada, configurar segurança básica e testar a conectividade.

---

## Cenário  
Você precisa criar uma rede virtual isolada na AWS para hospedar seus recursos. 


Essa rede terá uma sub-rede pública para um servidor web e uma sub-rede privada para um banco de dados, garantindo a segurança e o isolamento dos seus dados.

---

## Pré-requisitos  
- Uma conta AWS com acesso ao console de gerenciamento.  
- Navegador web.  
- MobaXterm (Portable Edition):
	- https://download.mobatek.net/2502024121622306/MobaXterm_Portable_v25.0.zip

---

## Tarefas  

### 1. **Criar a VPC:**  

- Passo 1: Acesse o console AWS e selecione a Região AWS us-east-1 (Norte da Virgínia).
- Passo 2: Acesse o console do VPC: Abra seu navegador web e acesse o console de gerenciamento da AWS. No menu de serviços, procure por "VPC" e clique nele.
- Passo 3: Clique em "Suas VPCs" e depois em "Criar VPC".
- Passo 4: Escolha a opção "VPC e muito mais".
- Passo 5: Em "Geração automática da etiqueta de nome", mude o nome "projeto" por "MinhaVPC-seu-nome-sobrenome".
- Passo 6: Defina um bloco CIDR para sua VPC: 10.0.0.0/16.
- Passo 7: Em "Tenancy = Locação ", selecione "Default = padrão".
- Passo 8: Em "Número de zonas de disponibilidade (AZs)" escolha 1.
- Passo 9: Em "Número de sub-redes públicas", escolha 1.
- Passo 10: Em "Número de sub-redes privadas", escolha 1.
- Passo 11: Em "Gateways NAT", selecione "Nenhum".
- Passo 12: Em "Endpoints da VPC", selecione "Nenhum".
- Passo 13: Clique em "Personalizar blocos CIDR de sub-redes"
- Passo 14: Em "Bloco CIDR da sub-rede pública em us-east-1a", informe "10.0.1.0/24"
- Passo 15: Em "Bloco CIDR da sub-rede privada em us-east-1a", informe "10.0.20.0/24"

- Passo 16: Finalize clicando em "Criar VPC"
- Passo 17: Verifique se a VPC foi criada clicando em "Suas VPCs". 

---

### 2. **Criar Grupos de Segurança:**  

- Passo 1: No painel de navegação, clique em "Grupos de segurança" e depois em "Criar grupo de segurança".

- Passo 2: Informe um nome para o grupo de segurança: "SG-Web-seu-nome-sobrenome".

- Passo 3: Em "Descrição", adicione: "Regras para acesso ao servidor web".
- Passo 4: Selecione a VPC que você criou (MinhaVPC-seu-nome-sobrenome).
- Passo 5: Na seção "Regras de entrada", clique em "Adicionar regra".
- Passo 6: Em "Tipo", selecione "HTTP".
- Passo 7: Em "Origem", selecione "Qualquer local-IPv4" (0.0.0.0/0).
- Passo 8: Clique novamente em "Adicionar regra".
- Passo 9: Em "Tipo", selecione "HTTPS".
- Passo 10: Em "Origem", selecione "Qualquer local-IPv4" (0.0.0.0/0).
- Passo 11: Clique novamente em "Adicionar regra".
- Passo 12: Em "Tipo", selecione "SSH".
- Passo 13: Em "Origem", selecione "Meu IP".
- Passo 14: Clique em "Criar grupo de segurança".
- Passo 15: Repita os passos 1 a 4 para criar um grupo de segurança para a instância de banco de dados:
  - Nome: "SG-BD-seu-nome-sobrenome"
  - Descrição: "Regras para acesso ao servidor de banco de dados"

- Passo 16: No grupo de segurança do banco de dados (SG-BD-seu-nome-sobrenome), adicione as seguintes regras de entrada:

	- Passo 16.1: Clique em "Adicionar regra".
	- Passo 16.2: Em "Tipo", selecione "SSH".
	- Passo 16.3: Em "Origem", selecione "Personalizado" e, no campo ao lado, insira o bloco CIDR da sua VPC: 10.0.0.0/16.
	- Passo 16.4 (MySQL): Clique em "Adicionar regra".
		- Em "Tipo", selecione "MySQL/Aurora".
		- Em "Origem", selecione "Personalizado" e, no campo ao lado, insira
	- bloco CIDR da sua VPC: 10.0.0.0/16.


- Passo 16.5 (PostgreSQL - Opcional): Se for usar PostgreSQL, clique em "Adicionar regra".
	- Em "Tipo", selecione "PostgreSQL".
	- Em "Origem", selecione "Personalizado" e, no campo ao lado, insira
    - bloco CIDR da sua VPC: 10.0.0.0/16.
- Passo 17: Clique em "Criar grupo de segurança".  

---

### 3. **Lançar Instâncias EC2:**  

Passo 1: No menu de serviços, procure por "EC2" e clique nele.
- Passo 2: Clique em "Instâncias" e depois em "Executar instâncias".
- Passo 3: Em "Nome", informe: ServidorWeb-seu-nome-sobrenome.

- Passo 4: Em "Imagem da Amazon Machine (AMI)", selecione: Amazon Linux 2023 (HVM), SSD Volume Type.
- Passo 5: Em "Tipo de instância", escolha: t2.micro.
- Passo 6: Em "Par de chaves (login)", crie um novo par de chaves ou use um existente.
	- Se for criar um novo, clique em "Criar novo par de chaves".
	- Nome do par de chaves: SeuNome.
	- Tipo de Chave Privada: .pem
	- Clique em "Criar par de chaves".
	- Salve o arquivo SeuNome.pem em um local seguro.
- Passo 7: Em "Configurações de rede", clique em "Editar"

- Passo 8: Em "VPC - Obrigatório", selecione a VPC que você criou (MinhaVPC-seu-nome-sobrenome).

- Passo 9: Em "Sub-rede", selecione a sub-rede pública (10.0.1.0/24).
- Passo 10: Em "Atribuir automaticamente IP público", verifique se está Habilitado.
- Passo 11: Em "Grupo de segurança", escolha "Selecionar grupo de segurança existente".

- Passo 12: Em "Grupos de segurança comuns", escolha "SG-Web-seu-nome-sobrenome".

- Passo 13: Em "Configurações de armazenamento", deixe como padrão.
- Passo 14: Clique em "Executar instância".

- Passo 15: Repita os passos 2 a 6 e 13 e 14 para lançar a instância ServidorBD-seu-nome-sobrenome. Os demais passos serão detalhados abaixo.

	- Passo 15.1: Em "Nome", informe: ServidorBD-seu-nome-sobrenome.
	- Passo 15.2: Em "Configurações de rede", clique em "Editar".
	- Passo 15.3: Em "VPC - Obrigatório", selecione a VPC que você criou (MinhaVPC-seu-nome-sobrenome).
	- Passo 15.4: Em "Sub-rede", selecione a sub-rede privada (10.0.20.0/24).
	- Passo 15.5: Em "Atribuir automaticamente IP público", certifique-se de que esteja Desabilitado.
	- Passo 15.6: Em "Grupo de segurança", escolha "Selecionar grupo de segurança existente".

	- Passo 15.7: Em "Grupos de segurança comuns", escolha "SG-BD-seu-nome-sobrenome ".

	- Passo 15.8: Em "Tipo de instância", escolha: t2.micro.
	- Passo 15.9: Em "Par de chaves (login)", selecione Lab4 (ou o nome que você deu ao par de chaves).  

---

### 4. **Testar a Conectividade (Usando MobaXterm):**  

Passo 1: Baixe e instale o MobaXterm
- Baixe o MobaXterm Portable Edition:
https://download.mobatek.net/2502024121622306/MobaXterm_Portable_v25.0.zip
	- Extraia o conteúdo do arquivo zip para uma pasta de sua preferência.
	- Execute o arquivo MobaXterm_Personal_25.0.exe
- Passo 2: Conecte-se à instância web (ServidorWeb-seu-nome-sobrenome) via SSH usando o MobaXterm.

  - No MobaXterm, clique em "Session" e selecione "SSH".

  - Em "Remote host", insira o endereço IP público do ServidorWeb-seu-nome-sobrenome (você encontra esse IP no console da AWS, na descrição da instância).
	- Marque "Specify username" e insira: ec2-user.
	- Clique em “Advanced SSH settings”.
	- Marque "Use private key" e selecione o arquivo .pem que você baixou (ex: SeuNome.pem).
	- Clique em "OK".
	- Se for solicitado a confirmar a chave, clique em "Accept".
- Passo 3: A partir da instância web (ServidorWeb-seu-nome-sobrenome), tente acessar a internet. Utilize o comando ping 8.8.8.8. Deve funcionar. (TIRE UM PRINT DESSA TELA PARA ANEXAR NA ATIVIDADE AO FINALIZAR NO CLASSROOM)

- Passo 4: Conecte-se à instância do banco de dados (ServidorBD-seu-nome-sobrenome) via SSH, utilizando a instância web (ServidorWeb-seu-nome-sobrenome) como "trampolim" (bastion host).

	- A partir da sessão SSH já aberta para o ServidorWeb-seu-nome-
sobrenome no MobaXterm, faça o seguinte procedimento: 
```bash
ssh -i "<caminho_para_chave>/SeuNome.pem" ec2-user@<endereço_IP_privado_do_ServidorBD-seu-nome-sobrenome>
```
(Substitua <caminho_para_chave> pelo caminho onde você salvou o arquivo SeuNome.pem e <endereço_IP_privado_do_ServidorBD-seu-nome-sobrenome> pelo IP privado do ServidorBD-seu-nome-sobrenome - você encontra esse IP no console da AWS, na descrição da instância).

- Passo 5: A partir da instância do banco de dados (ServidorBD-seu-nome-sobrenome), tente acessar a internet. O comando ping 8.8.8.8 não deve funcionar, pois a instância está em uma sub-rede privada sem acesso à internet pois o NAT Gateway não foi configurado na criação da VPC. (TIRE UM PRINT DESSA TELA PARA ANEXAR NA ATIVIDADE AO FINALIZAR NO CLASSROOM)

---

Demonstração do instrutor(a): Configurar um Nat Gateway para acesso da instância de Banco de Dados a internet.


**Observações:**
- Lembre-se de encerrar as instâncias EC2 quando não estiverem em uso para
evitar custos.


- Após concluir as tarefas, você pode excluir os recursos criados neste laboratório,
como as instâncias EC2, o Internet Gateway (criado automaticamente com a VPC),
as sub-redes e a própria VPC.


- Atenção: Exclua os recursos na ordem inversa da criação para evitar erros. Exclua
primeiro as instâncias, depois o EIP (se criado), depois os grupos de segurança, e
por fim a VPC (que excluirá automaticamente as sub-redes e o Internet Gateway.

---

**Documentação Adicional:**
- VPC: https://docs.aws.amazon.com/vpc/
- EC2: https://docs.aws.amazon.com/ec2/

**Grupos de Segurança:**
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html
- MobaXterm: https://mobaxterm.mobatek.net/
Após concluir as tarefas, você pode excluir os recursos criados neste laboratório, como as instâncias EC2, o NAT Gateway, o Internet Gateway, as sub-redes e a VPC.

---

Aqui vai uma sugestão:


- [Laboratório prático: Snapshots de EBS com AWS CLI e Python](https://github.com/nolascojoao/aws-ebs-snapshot-lab)
