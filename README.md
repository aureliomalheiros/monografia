# monografia
###Modo de usar

#### 1. Primeiro passo faça o backup do ambiente 
#### 2. Passo instalação do NMAP
	
	Para sistemas operacionais DEB
		> $sudo apt-get update
		> $sudo apt-get install nmap -y
	Para sistemas operacionais RPM
		> $sudo yum update
		> $sudo yum install nmap -y
	
#### 3. O arquivo tcp-port-scan-lld.sh deve ser enviado para o servidor Zabbix
	
	Deve ser enviado para o seguinte diretório:
		/usr/lib/zabbix/externalscripts

		Depois dê permissões de execução:

		$sudo chmod +x tcp-port-scan-lld.sh
		
		##### Para fazer um teste digite o seguinte comando
			> $sudo ./tcp-port-scan-lld.sh IP-HOST

#### 4. É necessário validar o Zabbix está com  permissões para executar scripts externos

	Abra o arquivo **zabbix_server.conf**

		> sudo vim /etc/zabbix/zabbix_server.conf
		> Procure por ExternalScripts
		> É necessário adicionar a linha que está abaixo caso não exista no arquivo 
			ExternalScripts=/usr/lib/zabbix/externalscripts
		> Se não existir, adicione e salve o arquivo
			> $sudo systemctl restart zabbix-server

