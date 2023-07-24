<p align="center">
	<img src="https://github.com/nocodeleaks/quepasa/raw/main/src/assets/favicon.png" alt="Quepasa-logo" width="100" />	
	<p align="center">Quepasa é um software de código aberto, totalmente gratuito, para troca de mensagens com a plataforma Whatsapp</p>
</p>

<hr />

**Manual de Instalação ChatWoot**

sudo apt update && apt upgrade -y
</p>
wget https://get.chatwoot.app/linux/install.sh
</p>
chmod +x install.sh
</p>
./install.sh --install
</p>
Use as opções abaixo
</p>
yes
</p>
chatwoot.dominio.com.br
</p>
contato@dominio.com.br
</p>
yes para todos
</p>
<hr />

**Alterando Idioma e ativando sua tela de cadastro**

</p>
cd /home/chatwoot/chatwoot
</p>
nano .env
</p>
Altere a linha
</p>
DEFAULT_LOCALE=pt_BR
</p>
ENABLE_ACCOUNT_SIGNUP=true
</p>
sudo systemctl restart chatwoot.target
</p>
Acesse: seudominio.com.br
</p>
Faça seu cadastro
</p>

<hr />

**Habilitando configurações ocultas do Chatwoot**

</p>
No banco de dados PostgreSQL
</p>
sudo -i -u postgres psql
</p>
\c chatwoot_production
</p>
update installation_configs set locked = false;
</p>
\q
</p>

<hr />

**NOMES CHATWOOT TERMOS E POLITICA DE PRIVACIDADE**

**Acesse super Admin**
</p>
https://seudominio.com.br/super_admin
</p>
Opção>installation_configs
</p>
LOGO
</p>
LOGO_THUMBNAIL
</p>
NOMES CHATWOOT:
</p>
Alterando nomes na plataforma
</p>
INSTALLATION_NAME
</p>
BRAND_NAME
</p>
TERMOS E POLITICA DE PRIVACIDADE
</p>
TERMS_URL
</p>
PRIVACY_URL
</p>
BRAND_URL
</p>
WIDGET_BRAND_URL
</p>

<hr />
<hr />

**Manual de Instalação N8N**

</p>
cd
</p>
</p>
sudo npm install n8n -g
</p>
npm update -g n8n
</p>
</p>
npm install pm2 -g
</p>
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
</p>
sudo apt install ./google-chrome-stable_current_amd64.deb
</p>
sudo nano /etc/nginx/sites-available/n8n
</p>
</p>
</p>

```
server {
  server_name n8n.dominio.com;
  
  underscores_in_headers on;

  location / {

   proxy_pass http://127.0.0.1:5678;
   proxy_pass_header Authorization;
   proxy_set_header Upgrade $http_upgrade;
   proxy_set_header Connection "upgrade";
   proxy_set_header Host $host;
   proxy_set_header X-Forwarded-Proto $scheme;
   proxy_set_header X-Forwarded-Ssl on; # Optional
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_http_version 1.1;
   proxy_set_header Connection "";
   proxy_buffering off;
   client_max_body_size 0;
   proxy_read_timeout 36000s;
   proxy_redirect off;
  }
  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
  ssl_protocols TLSv1.2 TLSv1.3;
} 
  ```

</p>
</p>
</p>
sudo ln -s /etc/nginx/sites-available/n8n /etc/nginx/sites-enabled
</p>
sudo certbot --nginx
</p>
sudo service nginx restart
</p>
</p>
pm2 start n8n --cron-restart="0 0 * * *" -- start
</p>

**EXECUTE COMANDO ABAIXO PARA NÃO CAIR QUANDO REINICIAR A VPS**

</p>
sudo pm2 startup ubuntu -u root && sudo pm2 startup ubuntu -u root --hp /root && sudo pm2 save
</p>
cd /root/.n8n
</p>
</p>
nano .env
</p>
Altere as seguintes variaveis baixo no arquivo .env
</p>
C8Q_QP_DEFAULT_USER=coloque email do Quepasa
</p>
C8Q_QP_BOTTITLE=Nome da Plataforma
</p>
C8Q_CW_PUBLIC_URL=domniochatwoot
</p>
C8Q_QP_CONTACT=Seu email
</p>
C8Q_QP_CONTACT=Seu email
</p>
WEBHOOK_URL=https://conector.dominio.com.br
N8N_EDITOR_BASE_URL=https://conector.dominio.com.br
</p>

```
C8Q_SINGLETHREAD=false
C8Q_QUEPASAINBOXCONTROL=1001
C8Q_GETCHATWOOTCONTACTS=1002
C8Q_QUEPASACHATCONTROL=1003
C8Q_CHATWOOTPROFILEUPDATE=1004
C8Q_POSTTOWEBCALLBACK=1005
C8Q_POSTTOCHATWOOT=1006
C8Q_CHATWOOTTOQUEPASAGREETINGS=1007
C8Q_CW_PUBLIC_URL="chatwoot.seudominio.com.br"
C8Q_QP_DEFAULT_USER="contato@seudominio.com.br"
C8Q_QP_BOTTITLE="Chatwoot"
C8Q_QP_CONTACT="contato@seudominio.com.br"
N8N_EDITOR_BASE_URL="https://conector.dominio.com.br"
WEBHOOK_URL="https://conector.dominio.com.br"
```

</p>
cp .env /root
</p>
</p>
pm2 restart all --update-env
</p>


<hr />
<hr />

**Manual de Instalação API Quepasa**

</p>

</p>
cd
</p>
</p>

```
git clone https://github.com/nocodeleaks/quepasa /opt/quepasa-source
bash /opt/quepasa-source/helpers/install.sh
bash /opt/quepasa-source/helpers/update-workflows.sh
```


</p>

</p>
sudo nano /etc/nginx/sites-available/quepasa
</p>


```
server {

  server_name quepasa.dominio.com.br;

  location / {

    proxy_pass http://127.0.0.1:31000;

    proxy_http_version 1.1;

    proxy_set_header Upgrade $http_upgrade;

    proxy_set_header Connection 'upgrade';

    proxy_set_header Host $host;

    proxy_set_header X-Real-IP $remote_addr;

    proxy_set_header X-Forwarded-Proto $scheme;

    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    
    proxy_cache_bypass $http_upgrade;

  }

  }
```

sudo ln -s /etc/nginx/sites-available/quepasa /etc/nginx/sites-enabled
</p>
</p>
sudo certbot --nginx
</p>
sudo service nginx restart
</p>
</p>

<hr />

**Ativando SSL da API Quepasa**

nano /opt/quepasa-source/src/.env
</p>
Adicione linha 1
</p>
APP_TITLE=Nome da Sua Empresa
</p>

Alterar linha 2
</p>
WEBSOCKETSSL=false
</p>
para
</p>
WEBSOCKETSSL=true
</p>
Alterar linha 8
</p>
REMOVEDIGIT9=true
</p>
systemctl restart quepasa
</p>

<hr />
<hr 

**Instalando Redis**

</p>
sudo add-apt-repository ppa:redislabs/redis
</p>
sudo apt update
</p>
sudo apt install redis
</p>
sudo apt-get install libvips
</p>

<hr />
</p>


***Execute esse processo abaixo parra deixar mais rapida sua API**

nano /etc/hosts

Adicione isso na primeira linha 
127.0.0.1       localhost app.dominio.com.br conector.dominio.com.br api.dominio.com.br

<hr />

**Instalação Finalizadas**

</p>
chatwoot.seudominio.com.br
</p>
n8n.seudominio.com.br
</p>
quepa.dominio.com.br/setup
</p>
Faça os cadastros em todos eles
</p>

</p>


<hr />
<hr 

**Configue os Worflows no N8N**

Adicione nodes ao seu N8N
</p>
n8n-nodes-chatwoot
</p>
n8n-nodes-quepasa
</p>
Acesse opção Credenciais, adicione suas credenciais Postgres, salve.
</p>
reboot
</p>
Após colocar credeciais nos Worflows salve todos 
</p>


<hr />

**Criando sua Caixa de Entrada**

</p>
Envia uma mensagem para Contato Criado
</p>
Quepasa Control
</p>
/qrcode
</p>
Leia QRCODE
</p>
<hr />
<hr />

**Pronto tudo Funcionando**

<hr />
<hr />


**Opcional: Para individualizar conversas entre agentes**


```bash

mv /home/chatwoot/chatwoot/app/javascript/dashboard/components/ChatList.vue /home/chatwoot/chatwoot/app/javascript/dashboard/components/ChatList.vue.old

```

</p>
cd /home/chatwoot/chatwoot/app/javascript/dashboard/components
</p>

```bash

wget "https://raw.githubusercontent.com/EngajamentoFlow/quepasa/main/ChatList.vue"

```

</p>
Após alterações acima, rebuildar seu Chatwoot
</p>
sudo -i -u chatwoot
</p>
cd chatwoot
</p>
rake assets:precompile RAILS_ENV=production
</p>
exit
</p>
systemctl daemon-reload && systemctl restart chatwoot.target
</p>

<hr />
<hr />

**Gostou do Tutorial? Faça sua Contribuição**

<img src="https://github.com/EngajamentoFlow/quepasa/blob/main/Contribui%C3%A7%C3%A3o.png" alt="Quepasa-logo" width="200" />
</p>


**PIX CNPJ**

```
45959142000119	
```

<hr />
<hr />
