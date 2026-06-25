# ChatBot_Telegram_n8n
Desafio Prático: Bot de Clima no Telegram com N8N

# 🌤️ Bot de Clima no Telegram com n8n

## 📖 Descrição do Projeto
Este projeto consiste em um chatbot interativo no Telegram, desenvolvido inteiramente através de fluxos de automação no **n8n**. O objetivo principal do bot é receber o nome de uma cidade (e estado) enviada pelo usuário, consultar a API gratuita do **OpenWeather**, processar os dados recebidos e retornar a temperatura atual em graus Celsius de forma amigável.

O fluxo também conta com tratamento de erros: caso o usuário digite uma cidade inválida ou um formato não reconhecido, o bot responde com uma mensagem de orientação.

---

## 🚀 Como importar o workflow no n8n

Para rodar este projeto no seu próprio ambiente n8n, siga os passos abaixo:

1. Faça o download do arquivo `workflow-chatbot-telegram.json` presente neste repositório.
2. Abra a interface do seu n8n.
3. No painel principal, clique em **Add Workflow** (Adicionar Workflow) para criar um fluxo em branco.
4. No canto superior direito, clique no menu de opções (os três pontinhos `...`) e selecione **Import from File** (Importar de Arquivo).
5. Selecione o arquivo `.json` que você baixou. O fluxo completo aparecerá na sua tela.

> **Nota:** O arquivo JSON disponibilizado está limpo e não contém nenhuma credencial ou chave privada.

---

## 🔐 Configuração das Credenciais

Para que o fluxo consiga se comunicar com o Telegram e com o OpenWeather, você precisará configurar as suas próprias chaves de API no n8n.

### 1. Credencial do Telegram (`TELEGRAM_BOT_TOKEN`)
1. No Telegram, converse com o [@BotFather](https://t.me/botfather) e crie um novo bot usando o comando `/newbot`.
2. Copie o Token HTTP gerado.
3. No n8n, vá no menu lateral esquerdo em **Credentials** > **Add Credential**.
4. Pesquise por **Telegram API** e cole o seu token no campo solicitado.
5. Salve e vincule esta credencial aos nós do Telegram (Trigger e Send Message) dentro do fluxo.

### 2. Credencial do OpenWeather (`OPENWEATHER_API_KEY`)
1. Crie uma conta no site [OpenWeather](https://openweathermap.org/) e gere uma API Key gratuita.
2. No n8n, abra o nó de **HTTP Request** (nomeado como "Pesquisa a Temperatura").
3. Na seção de Autenticação (*Authentication*), certifique-se de que está configurado como **Query Auth**.
4. Crie uma nova credencial colando a sua chave gerada. O n8n enviará automaticamente o parâmetro `appid` junto com a sua chave (variável esperada: `OPENWEATHER_API_KEY`) durante a requisição.

---

## ⚙️ Como executar e testar o Chatbot

Após importar o fluxo e configurar ambas as credenciais:

1. No canto superior direito do n8n, ative o botão **Active** (mude de inativo para ativo). *Isso fará com que o bot fique ouvindo o Telegram em tempo real.*
2. Abra o aplicativo do Telegram e inicie uma conversa com o bot que você criou.

### 🧪 Exemplos de Uso

**Cenário de Sucesso:**
* **Você envia:** `Curitiba, PR`
* **Bot responde:** `🌤️ A temperatura em Curitiba é de 18°C.`
* **Você envia:** `São Paulo, SP`
* **Bot responde:** `🌤️ A temperatura em São Paulo é de 20°C.`

**Cenário de Erro (Tratamento de Falha):**
* **Você envia:** `Grifnória` *(ou qualquer cidade inexistente)*
* **Bot responde:** `❌ Cidade não encontrada. Use o formato "Cidade, UF" (ex.: São Paulo,SP).`

---
*Projeto desenvolvido como parte do Desafio Prático de Agentes e Automação.*
