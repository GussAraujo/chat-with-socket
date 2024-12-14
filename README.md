# Chat com Python Usando Sockets

Este projeto é um sistema de chat simples implementado em Python usando a biblioteca `socket`. Ele inclui um servidor e um cliente que permitem múltiplos usuários se conectarem e trocarem mensagens em tempo real. Também há suporte para envio de mensagens privadas e autenticação por senha.

## Arquivos do Projeto

- **`server.py`**: Contém a lógica do servidor que gerencia conexões, autenticação e troca de mensagens entre os clientes.
- **`client.py`**: Implementa a interface do cliente que se conecta ao servidor e permite o envio e recebimento de mensagens.

## Funcionalidades

- **Autenticação por senha:** O servidor exige uma senha para que os clientes possam se conectar.
- **Mensagens públicas:** Todos os clientes conectados recebem mensagens enviadas ao chat público.
- **Mensagens privadas:** Um cliente pode enviar mensagens diretamente para outro cliente.
- **Comando para sair:** Os usuários podem sair do chat digitando `@sair`.
- **Manuseio de desconexões inesperadas:** O servidor detecta quando um cliente desconecta inesperadamente e notifica os outros usuários.

## Dependências

- Python 3.x

## Como Executar

### Passo 1: Iniciar o Servidor

1. Abra um terminal.
2. Execute o seguinte comando:

   ```bash
   python server.py
   ```

3. O servidor será iniciado na porta `5000` e estará pronto para aceitar conexões.

### Passo 2: Iniciar o Cliente

1. Abra um novo terminal.
2. Execute o seguinte comando:

   ```bash
   python client.py
   ```

3. Insira a senha solicitada pelo servidor (a senha padrão é `a`).
4. Após autenticação bem-sucedida, insira um nome de usuário e comece a interagir no chat.

## Comandos Disponíveis no Chat

- **`@sair`**: Sai do chat.
- **`@privado:<destinatário> <mensagem>`**: Envia uma mensagem privada para o usuário especificado.

## Estrutura dos Códigos

### `server.py`

O servidor gerencia:
- Conexões de clientes.
- Autenticação por senha.
- Mensagens públicas e privadas.
- Manutenção da lista de clientes conectados.
- Remoção de clientes desconectados.

### `client.py`

O cliente permite:
- Conectar-se ao servidor.
- Enviar e receber mensagens.
- Autenticar-se com senha e nome de usuário.

## Motivação da Escolha do Protocolo de Transporte

O protocolo escolhido foi o **TCP (Transmission Control Protocol)** devido às suas características de:
- **Confiabilidade:** O TCP garante que as mensagens sejam entregues corretamente e na ordem correta.
- **Controle de fluxo:** Ele gerencia a taxa de envio para evitar sobrecarregar o receptor.
- **Persistência de conexão:** O TCP estabelece uma conexão contínua, essencial para a comunicação em tempo real de um chat.

Essas características tornam o TCP ideal para aplicações onde a entrega precisa e ordenada de mensagens é fundamental, como em um sistema de chat.

## **Fluxo de Comunicação Técnico**

### **Estabelecimento de Conexão**
1. O cliente inicia uma conexão TCP com o servidor na porta `5000`.
2. Após a conexão, o servidor aguarda a senha enviada pelo cliente.
3. Se a senha estiver correta, o servidor aceita a conexão e solicita o nome de usuário.

### **Troca de Mensagens**
1. **Mensagens Públicas:**
   - O cliente envia mensagens públicas com o formato `[timestamp] <username> mensagem`.
   - O servidor retransmite essas mensagens para todos os outros clientes conectados, exceto para o remetente.

2. **Mensagens Privadas:**
   - O cliente utiliza o comando `@privado: <destinatário> <mensagem>`.
   - O servidor verifica o destinatário na lista de clientes conectados.
     - Se encontrado, o servidor encaminha a mensagem ao destinatário.
     - Caso contrário, o servidor informa ao remetente que o usuário não foi encontrado.

3. **Sair do Chat:**
   - O cliente envia o comando `@sair`.
   - O servidor remove o cliente da lista de conexões e notifica os demais usuários sobre a saída.

### **Tratamento de Erros**
1. **Conexão Perdida:**
   - Se um cliente desconectar inesperadamente, o servidor remove o cliente da lista e notifica os demais.

2. **Destinatário Não Encontrado:**
   - O servidor retorna uma mensagem ao remetente indicando que o destinatário não está conectado.

3. **Senha Incorreta:**
   - O servidor encerra a conexão imediatamente se a senha estiver errada.

---

## **Erros Comuns**

- **Senha Incorreta:**
  - Certifique-se de usar a senha `123456` ao conectar-se ao servidor.

- **Destinatário de Mensagem Privada Não Encontrado:**
  - Verifique o nome do destinatário antes de enviar uma mensagem privada.

- **Servidor Não Iniciado:**
  - Certifique-se de que o servidor foi iniciado antes de executar o cliente.