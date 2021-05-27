# wso2am-3.2.0-wso2am-analytics-3.2.0
## Guia de instalação e configuração da aplicação

- 1º Instale o vagrant na sua máquina 
- 2º Instale um hypervisor: hyperv, virtualbox, vmware etc..
- 3º Clone o repositório
- 4º Entre no diretório clonado com o comando: "cd repositorio_clonado"
- 5º Baixe o wso2am-3.2.0.zip https://wso2.com/api-management/previous-releases/
- 6º Descompacte no diretório "/data"
- 7º baixe o wso2am-analytics-3.2.0.zip https://github.com/wso2/analytics-apim/archive/refs/tags/v3.2.0.zip
- 8º Descompacte no diretório "/data"
- 9º Abra o o diretório principal em um terminal como "PowerShell", "Terminal Linux", etc..
- 10 º Execute o comando vagrant up para subir a máquina no hypervisor


## Url´s de acesso das aplicações:
- https://ip_do_host:9443/admin
- https://ip_do_host:9443/carbon
- https://ip_do_host:9443/publisher
- https://ip_do_host:9443/devportal
- https://ip_do_host:9643/analytics-dashboard

## Para gerenciar a máquina virtual use o seguinte comando: 
- vagrant ssh 
### A máquina virtual esta com o IP 192.168.0.51, altere no Vagrantfile se houver necessidade.
Estão configurados os seguintes serviços no "/etc/systemd/system":
- 1º wso2ApimWso2Server ->  executa o /opt/wso2/wso2am-3.2.0/bin/wso2server.sh
- 2º wso2ApimWorker     ->  executa o /opt/wso2/wso2am-analytics-3.2.0/bin/worker.sh
- 3º wso2ApimDashboard  ->  executa o /opt/wso2/wso2am-analytics-3.2.0/bin/dashboard.sh

### Comandos para start, stop e reload do wso2am-3.2.0:
- 1º sudo service wso2ApimWso2Server start
- 2º sudo service wso2ApimWso2Server stop
- 3º sudo service wso2ApimWso2Server reload

### Comandos para start, stop e reload do wso2am-analytics-3.2.0 worker
- 1º sudo service wso2ApimWorker start
- 2º sudo service wso2ApimWorker stop
- 3º sudo service wso2ApimWorker reload

### Comandos para start, stop e reload do wso2am-analytics-3.2.0 dashboard
- 1º sudo service wso2ApimDashboard start
- 2º sudo service wso2ApimDashboard stop
- 3º sudo service wso2ApimDashboard reload

### Comandos para verificação dos serviços wso2am-3.2.0
- ps -ef | grep wso2

# Comandos úteis do vagrant:
## Up
* vagrant up
  * Cria e inicia a instancia após o comando vagrant init

## Reload
* vagrant reload
  * Reinicia a instancia do box ativo

## Suspend
* vagrant suspend
  * Stopa a instancia ativa, congelando seu estado atual

## Resume
* vagrant resume
  * Ativa a instancia suspensa, até então, pelo comando vagrant suspend

## Halt
* vagrant halt
  * Manda um comando para desligar a instancia ativa, finalizando todos os processos antes de finalizar

## Destroy
* vagrant destroy
  * Destroy a instancia ativa

## SSH
* vagrant ssh
  * Acessa a instancia ativa via ssh

## Status
* vagrant status
  * Informa o status atual da instancia
