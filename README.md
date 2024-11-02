# Servidor Nginx
## Servidor Nginx e Monitoramento de Serviço
Este projeto tem como objetivo configurar um servidor Nginx no Linux, implementar um script de monitoramento que valida o status do serviço e automatizar a execução do script a cada 5 minutos. O script gera logs sobre o status do serviço, diferenciando quando o serviço está online ou offline, e os resultados são armazenados em arquivos separados. Todo o processo é versionado para controle.

## Requisitos
- Distribuição Linux (ex: Ubuntu, Debian)
- Permissão de superusuário (root) para instalação e configuração
- Nginx instalado e rodando
- Editor de texto para editar scripts e configurar o cron job
- Git para versionamento

1. Instalar o Nginx
Atualize os pacotes:

` bash
sudo apt update `

Instale o Nginx:

` bash
sudo apt install nginx `

Inicie o serviço do Nginx:

` bash
sudo systemctl start nginx `

- Habilite o serviço para iniciar automaticamente com o sistema:

` bash 
sudo systemctl enable nginx `

Verifique o status do Nginx:

` bash
  sudo systemctl status nginx`

  > Acesse "http://localhost" no navegador para confirmar a instalação e o funcionando do servidor.
  

2. Criar o Script de Monitoramento 
- Crie um arquivo de script para verificar o status do Nginx e registrar os logs.
- Crie um diretório para os logs:

` bash
mkdir ~/nginx_status_logs ` 

3. Crie o arquivo do script:

` bash
  nano ~/check_nginx.sh `
  
4. Adicione o seguinte conteúdo ao script:

```` bash

#!/bin/bash

LOG_DIR=~/nginx_status_logs 
DATA_HORA=$(date '+%Y-%m-%d %H:%M:%S') 
SERVICE="Nginx" 
  
SERVICE_STATUS=$(systemctl is-active nginx)

if [ "$SERVICE_STATUS" = "active" ]; then STATUS="ONLINE" 
MENSAGEM="O serviço está rodando normalmente." echo "$DATA_HORA - $SERVICE - $STATUS - $MENSAGEM" >> $LOG_DIR/nginx_online.log 
else STATUS="OFFLINE" MENSAGEM="O serviço está offline ou inativo." 
echo "$DATA_HORA - $SERVICE - $STATUS - $MENSAGEM" >> $LOG_DIR/nginx_offline.log 

fi 

 ``````

5. Dê permissão de execução ao script:

` bash
chmod +x ~/check_nginx.sh `

6. Automatizar a Execução do Script 
Para que o script seja executado a cada 5 minutos automaticamente, utilize a ferramenta ` cron `.

Edite o arquivo:

` bash 
crontab -e ` 

- Adicione a seguinte linha ao final do arquivo:

` */5 * * * * ~/check_nginx.sh `

Isso configurará o cron para executar o script a cada 5 minutos. E, por fim, para concluir que o servidor está rodando. Verifique seu ip com o comando:

` ip addr show `


7. Git para o versionamento
Instale o GitHub CLI

` sudo apt install gh `

- Faça o login:

` gh auth login `

Selecione as opções oferecidas no terminal e vá seguindo as intruções propostas.

## Repósitorio Git

` git init `

` git add .`


