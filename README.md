# servidor_nginx
README - Servidor Nginx e Monitoramento de Serviço
Este projeto tem como objetivo configurar um servidor Nginx no Linux, implementar um script de monitoramento que valida o status do serviço, e automatizar a execução do script a cada 5 minutos. O script gera logs sobre o status do serviço, diferenciando quando o serviço está online ou offline, e os resultados são armazenados em arquivos separados. Todo o processo é versionado para controle.

- Requisitos
Distribuição Linux (ex: Ubuntu, Debian)
Permissão de superusuário (root) para instalação e configuração
Nginx instalado e rodando
Editor de texto para editar scripts e configurar o cron job
Git para versionamento
Passos para Instalação e Configuração
1. Instalar o Nginx
Atualize os repositórios de pacotes:

bash
sudo apt update
Instale o Nginx:

bash
sudo apt install nginx
Inicie o serviço do Nginx:

bash
sudo systemctl start nginx
Habilite o serviço para iniciar automaticamente com o sistema:

bash
sudo systemctl enable nginx
Verifique o status do Nginx:

bash
sudo systemctl status nginx
O serviço deve estar rodando.

2. Criar o Script de Monitoramento
Crie um arquivo de script para verificar o status do Nginx e registrar os logs.

Crie um diretório para os logs:

bash
mkdir ~/nginx_status_logs
Crie o script check_nginx.sh:

bash
nano ~/check_nginx.sh
Adicione o seguinte conteúdo ao script:

bash

#!/bin/bash

LOG_DIR=~/nginx_status_logs
DATA_HORA=$(date '+%Y-%m-%d %H:%M:%S')
SERVICE="Nginx"
SERVICE_STATUS=$(systemctl is-active nginx)

if [ "$SERVICE_STATUS" = "active" ]; then
    STATUS="ONLINE"
    MENSAGEM="O serviço está rodando normalmente."
    echo "$DATA_HORA - $SERVICE - $STATUS - $MENSAGEM" >> $LOG_DIR/nginx_online.log
else
    STATUS="OFFLINE"
    MENSAGEM="O serviço está offline ou inativo."
    echo "$DATA_HORA - $SERVICE - $STATUS - $MENSAGEM" >> $LOG_DIR/nginx_offline.log
fi
Dê permissão de execução ao script:

bash
chmod +x ~/check_nginx.sh
3. Automatizar a Execução do Script com Cron
Para que o script seja executado a cada 5 minutos automaticamente, utilize o cron.

Edite o arquivo de crontab:

bash
crontab -e
Adicione a seguinte linha ao final do arquivo:

bash
Copiar código
*/5 * * * * ~/check_nginx.sh

Isso configurará o cron para executar o script a cada 5 minutos.

E, por fim, para concluir que o servidor está rodando. Verifique seu ip com o comando

ip addr show

e após isso cole-o na URL do navegador de sua preferência.

E pronto, seu servidor estará ativo.
