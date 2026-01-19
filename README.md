# Cria-o_de_GPO_Servidor
Este procedimento descreve como criar e aplicar uma GPO no Active Directory para:  Ocultar todas as unidades no Este Computador,  Bloquear o acesso às unidades pelo Windows Explorer , Aplicar a política por usuário , Centralizar o controle via Group Policy Management





1- Abra o Group Policy Management.

![1Barra_de_pesquisa_GPO](https://github.com/user-attachments/assets/7b73e434-fafc-4660-98be-7a9e59f270bf)

2- Configuração do Security Filtering
- Navegue pela estrutura:

Domínio
 └── servidor01.srv
     └── clientes

- Localize o grupo da empresa.
- Clique com o botão direito e selecione:
- Create a GPO in this domain, and Link it here
- Defina um nome para a GPO (ex: GPO_Bloqueio_Unidades_Usuarios).
  
![2Create_a_GPO_in_this_domain](https://github.com/user-attachments/assets/0f530ace-722f-4ecd-bdb4-b5db8f992c20)


3- Configuração do Security Filtering
- Selecione a GPO criada.
- Na seção Security Filtering, remova: Authenticated Users
- Adicione apenas o grupo ou usuários que devem receber a política.
  
![3Security_filtering](https://github.com/user-attachments/assets/6c0f972a-6d13-4367-806f-0109311a6904)

4 e 5- Edição da GPO
- Clique com o botão direito na GPO.
- Selecione Edit.
- Navegue pelo caminho:

User Configuration
 └── Policies
     └── Administrative Templates
         └── Windows Components
             └── File Explorer

![4Edit_GPO](https://github.com/user-attachments/assets/32b0511a-fd69-485b-a25b-99dbf7cb22e2)
![5User_policies](https://github.com/user-attachments/assets/e2f7f7cb-b523-4955-b547-e56e3945d916)

6 e 7- Configurações de Restrição
- Ocultar Unidades no “Este Computador”
- Política:
  - Hide these specified drives in My Computer
  - Configuração:
  - Marque Enabled
  - Em Options, selecione:
  - Restrict all drives
  

![6Setting](https://github.com/user-attachments/assets/45a0fffb-f53b-4ff8-bf67-4f84ffd81cc5)
![7Enable](https://github.com/user-attachments/assets/7b8d1fdc-fe8c-4f9d-8075-e91b379dc484)

8- Atualização da Política
 -  Atualização via Group Policy Management
 -  Volte ao Group Policy Management.
 -  Clique com o botão direito no grupo da empresa.
    - Selecione:
    - Group Policy Update

    ℹ️ Importante:
    Como a política é de User Configuration, ela:
    - Só é aplicada no login do usuário
    - Não entra em vigor imediatamente se o usuário já estiver logado
  
    ![8Update](https://github.com/user-attachments/assets/b0434400-941b-47c9-a34d-34cdf9b4ada6)

  9- Atualização Imediata (Opcional)
  - Para aplicar a política imediatamente a um usuário específico:
  - Acesse o servidor via RDP com o usuário do cliente.
  - Abra o Prompt de Comando (CMD).
  - Execute:
  - gpupdate /force : isso ira atoalizar e aplicar as politicas

   ![9CMD_usuario](https://github.com/user-attachments/assets/891c6ebc-d5ba-4cca-9f20-b00fafbe5440)


10 -  Resultado Final 

- Para o usuário impactado:
❌ Não vê nenhuma unidade
❌ Não acessa discos pelo Explorer
❌ Não acessa digitando caminhos (C:\, D:\)

- Para o administrador:

✔ Controle centralizado

✔ Aplicação por usuário ou grupo

✔ Fácil gerenciamento e reversão

⚠️ Observação de Segurança

- Esta GPO bloqueia o acesso apenas via Windows Explorer.
- Ela não altera permissões NTFS.

- Para bloqueio total (leitura/escrita por qualquer meio), considere:
- Permissões NTFS
- AppLocker ou SRP
-Bloqueio de CMD e PowerShell

![10PC_usuario](https://github.com/user-attachments/assets/8fb1ac78-bf27-424c-beb6-fc18b038cf29)


