# Izing

Um sistema para gestão de atendimento multicanais centralizado.


**IMPORTANTE**: não garantimos que a utilização desta ferramenta não irá gerar bloqueio nas contas utilizadas. São bots que em sua maioria utilizam APIs secundarias para comunicação com os fornecedores dos serviços. Use com responsabilidade!

<br/>

## Screenshots

![Doação](screenshots/Bot.gif)
<br/>

![Doação](screenshots/dashboard.gif)
<br/>

![Doação](screenshots/izing.gif)
___

<br/>

## Principais funcionalidades

- Multíplos canais de atendimento ✅
- Multíplos usuários simultâneos por canais de atendimento ✅
- Iniciar conversa com contatos existentes (whatsapp) ✅
- Construção de Chatbot interativo ✅
- Enviar e receber mensagens ✅
- Enviar e receber mídias diversas (imagens/áudio/documentos) ✅
- Multiempresas (abordagem de base compartilhada)

<br/>

## Instalando
Seguem links sugerimos:
-  [Como Instalar o IZING - Método 2023](https://www.youtube.com/watch?v=0j1v6m4Nk74&t=379s)

-  =====================================
INSTALAÇÃO do aaPanel com iZing 2023
====================================

▶️ UBUNTU 22.04

▶️ COMANDOS PARA PREPARAR E INSTALAR O QUE É NECESSÁRIO NO SERVIDOR

timedatectl set-timezone America/Sao_Paulo && apt update && apt upgrade -y && apt install -y libgbm-dev wget unzip fontconfig locales gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils python2-minimal build-essential postgresql-14 redis-server && add-apt-repository -y ppa:rabbitmq/rabbitmq-erlang && wget -qO - https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.deb.sh | sudo bash && apt install -y rabbitmq-server && rabbitmq-plugins enable rabbitmq_management && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && apt install -y ./google-chrome-stable_current_amd64.deb && rm -rf google-chrome-stable_current_amd64.deb && wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && bash install.sh aapanel && rm -rf install.sh && reboot

❗❗❗ A máquina vai reiniciar.

▶️ ACESSAR E CONFIGURAR O AAPANEL + POSTGRESQL + REDIS + RABBITMQ.

🔹 Após instalar o Nginx 1.21 e fazer as configurações de costume da área "Settings" instale:

➥ PM2 Manager

🔹 No Node.js version manager instale a versão 14.21.1 do Node.
🔹 No PM2 Manager configure a versão 14.21.1 do Node.

🔹 Vá nas configurações do SYS Firewall e abra as portas:
➥ 5432 (PostgreSQL)
➥ 6379 (Redis)
➥ 5672 (RabbitMQ)

🔹 Edite os arquivos:
➥ /etc/postgresql/14/main/postgresql.conf
Descomentar e deixar a linha como abaixo:
listen_addresses = '*'

➥ /etc/postgresql/14/main/pg_hba.conf
Deixar a linha como abaixo:
host all all 0.0.0.0/0

➥ /etc/redis/redis.conf
Descomentar e deixar a linha como abaixo:
requirepass 2000@23

🔹 Configure o PostgreSQL no terminal.
sudo -u postgres psql
ALTER USER postgres PASSWORD '2000@23';
\q

sudo -u postgres psql
CREATE DATABASE izing;
\q

🔹 Configure o RabbitMQ no terminal.
rabbitmqctl add_user admin 123456
rabbitmqctl set_user_tags admin administrator
rabbitmqctl set_permissions -p / admin "." "." ".*"

❗❗❗ É INTERESSANTE DAR UM REBOOT APÓS ESSA ETAPA!

▶️ INSTALAÇÃO DO IZING.

🔹 Clonar repositório.
git clone https://github.com/ldurans/izing.io.git /www/wwwroot

🔹 Editar o .env do backend (nano, cp, etc...).
➥ Ex.: nano /www/wwwroot/NOME_DA_PASTA/backend/.env

▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ 

NODE_ENV=dev
BACKEND_URL=https://xxxx.xxxxx.xxxxx
FRONTEND_URL=https://xxxx.xxxxx.xxxxx

# URL PARA O ADMIN-FRONTEND
ADMIN_DOMAIN=https://xxxx.xxxxx.xxxxx

PROXY_PORT=443
PORT=xxxxx

DB_DIALECT=postgres
DB_PORT=5432
POSTGRES_HOST=localhost
POSTGRES_USER=postgres
POSTGRES_PASSWORD=SENHA_DO_POSTGRESQL
POSTGRES_DB=NOME_DA_DB

JWT_SECRET=DPHmNRZWZ4isLF9vXkMv1QabvpcA80Rc
JWT_REFRESH_SECRET=EMPehEbrAdi7s8fGSeYzqGQbV5wrjH4i

IO_REDIS_SERVER=localhost
IO_REDIS_PASSWORD=SENHA_DO_REDIS
IO_REDIS_PORT='6379'
IO_REDIS_DB_SESSION='2'

#CHROME_BIN=/usr/bin/google-chrome
#CHROME_BIN=/usr/bin/google-chrome-stable
#CHROME_BIN=null



RABBITMQ_DEFAULT_USER=USUARIO_RABBITMQ
RABBITMQ_DEFAULT_PASS=SENHA_RABBITMQ
# AMQP_URL='amqp://USUARIO_RABBITMQ:SENHA_RABBITMQ@localhost:5672?connection_attempts=5&retry_delay=5'

# API OFICIAL (INTEGRAÇÃO EM DESENVOLVIMENTO)
API_URL_360=https://waba-sandbox.360dialog.io

# DADOS PARA UTILIZAÇÃO DO CANAL DO FACEBOOK
FACEBOOK_APP_ID=3237415623048660
FACEBOOK_APP_SECRET_KEY=3266214132b8c98ac59f3e957a5efeaaa13500

▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ 

▶️ SUBIR O BACKEND.

❗❗❗ Certifique-se de ter criado o banco de dados!

🔹 Execute o comando:

npm install 
npm run build 
npx sequelize db:migrate 
npx sequelize db:seed:all

▶️ SUBIR O FRONTEND.

🔹 Editar o .env do frontend (nano, cp, etc...).
➥ Ex.: nano /www/wwwroot/NOME_DA_PASTA/frontend/.env

▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ 

URL_API='https://xxxx.xxxxx.xxxxx'
FACEBOOK_APP_ID='23156312477653241'

▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ ▲ 

🔹 Executar os comandos:

npm i -g @quasar/cli
npm install
quasar build -P -m pwa



▶️ CONFIGURAR O PM2 PARA INICIAR COM O SERVIDOR

pm2 startup ubuntu -u root

▶️ SUBIR E MAPEAR AS INSTÂNCIAS DO BACKEND, FRONTEND E ADMIN-FRONTEND

🔹 Caminhos no PM2 MANAGER DO AAPANEL:

➥ BACKEND:
Startup file: /www/web/NOME_DA_PASTA/backend/dist/server.js
Run dir: /www/web/NOME_DA_PASTA/backend

🔹 Caminhos no WEBSITE DO AAPANEL:
➥ FRONTEND: /www/web/NOME_DA_PASTA/frontend/dist/pwa

Se essa informação foi útil pra você, considere fazer um PIX para 

(Telefone) 85985282207


Agradecimentos ao amigo de grupo @Thiago


==== ==== ==== ==== ==== ====
FIM! FIM! FIM! FIM! FIM! FIM!
==== ==== ==== ==== ==== ====

<br/>

## Atualizando

Izing é um trabalho em progresso e estamos frequentemente adicionando novas funcionalidades e correções de bugs.

<br/>

**IMPORTANTE**: verifique sempre o .env.example e ajuste o seu .env antes de atualizar, uma vez que algumas novas variáveis podem ser adicionadas.


<br/>

## FIQUE ATENTO

A utilização desta ferramenta é feita por sua conta e risco. O código é aberto e todos podem contribuir.

Este projeto não é afiliado, associado, autorizado, endossado por, ou de qualquer forma oficialmente ligado à WhatsApp, ou a qualquer uma das suas filiais ou afiliadas. O website oficial da WhatsApp pode ser encontrado em <https://whatsapp.com>. "WhatsApp", bem como nomes, marcas, emblemas e imagens relacionadas são marcas registadas dos seus respectivos proprietários.

--------------------------
<br/>


#### Curtiu? Apoie o projeto!! Com sua doação, será possível continuar com as atualizações. Segue QR code (PIX)  

[<img src="donate.jpeg" height="150" width="200"/>](donate.jpeg)

--------------------------
<br/>

## **Licença e seus requerimentos**

Izing é open-source, licenciado com base na licença GNU Affero General Public License Version 3 [(AGPLv3)](https://www.gnu.org/licenses/agpl-3.0.pt-br.html). O objetivo da licença AGPL é maximizar a liberdade do usuário e incentivar as empresas a contribuir com o código aberto.

Você pode usar o izing em sua própria estrutura, desde que não seja para fins de comercialização.
Você pode fazer um fork do projeto para realizar suas alterações, implementar os recursos desejados, mas deverá abrir o código para a comunidade, conforme previsto pela licença. 

Uma vez que você deseje utilizar o izing para fins comerciais, todas as suas alterações, seu código fonte, precisa ser aberto (open source) para acesso pela comunidade, conforme licença. Bem como, deverá de forma clara, evidenciar aos seus usuários/clientes em menção de destaque ao projeto oficial (https://izing.io). Também é requerido a menção que você fornece uma versão alterada do izing e, em algum lugar do seu site, deverá fornecer o link para o repositório do seu projeto, permitindo que todos possam verificar as mudanças realizadas.

