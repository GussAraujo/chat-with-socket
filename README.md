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