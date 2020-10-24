# Monografia

#### 1. Primeiro passo faça o backup do ambiente 
#### 2. Instalação do NMAP
	
	Para sistemas operacionais DEB
		
		```console
		host@host$sudo apt-get update
		host@host$sudo apt-get install nmap -y
		```
	Para sistemas operacionais RPM
		
		```console
		$sudo yum update
		$sudo yum install nmap -y
		```

#### 3. O arquivo tcp-port-scan-lld.sh deve ser enviado para o servidor Zabbix
	
	Deve ser enviado para o seguinte diretório:
		
		/usr/lib/zabbix/externalscripts

		Depois de adicionar o arquivo no diretório dê permissões de execução:
		
		```console
		host@host$sudo chmod +x tcp-port-scan-lld.sh
		```
		
		**Para fazer um teste digite o seguinte comando:**
			
		```console
		host@host$sudo ./tcp-port-scan-lld.sh IP-HOST
		```

#### 4. É necessário validar o Zabbix está com  permissões para executar scripts externos

	Abra o arquivo **zabbix_server.conf**
		
		```console
		sudo vim /etc/zabbix/zabbix_server.conf
		```
		Procure por ExternalScripts no arquivo
		É necessário adicionar a linha que está abaixo caso não exista no arquivo 
			
			ExternalScripts=/usr/lib/zabbix/externalscripts

		Se não existir, adicione e salve o arquivo
		
		```console
		$sudo systemctl restart zabbix-server
		```
#### 5. Importe o template para o zabbix
		
		O arquivo template_tcp_port_scan_lld.xml deve ser importado para o Zabbix

