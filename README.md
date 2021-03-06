# Monografia

#### 1. Primeiro passo faça o backup do ambiente 
#### 2. Instalação do NMAP
	
	Para sistemas operacionais DEB
		
```console
host@host:~$ sudo apt-get update
host@host:~$ sudo apt-get install nmap -y
```
	Para sistemas operacionais RPM
		
```console
host@host:~$ sudo yum update
host@host:~$ sudo yum install nmap -y
```

#### 3. O arquivo tcp-port-scan-lld.sh deve ser enviado para o servidor Zabbix
	
	Deve ser enviado para o seguinte diretório:
		
		/usr/lib/zabbix/externalscripts

		Depois de adicionar o arquivo no diretório dê permissões de execução:
		
```console
host@host:~$ sudo chmod +x tcp-port-scan-lld.sh
```
		
		**Para fazer um teste digite o seguinte comando:**
			
```console
host@host:~$ sudo ./tcp-port-scan-lld.sh IP-HOST
```

#### 4. É necessário validar o Zabbix está com  permissões para executar scripts externos

	Abra o arquivo zabbix_server.conf
		
```console
host@host:~$ sudo vim /etc/zabbix/zabbix_server.conf
```
		Procure por ExternalScripts no arquivo
		É necessário adicionar a linha que está abaixo caso não exista no arquivo 
			
			ExternalScripts=/usr/lib/zabbix/externalscripts

		Se não existir, adicione e salve o arquivo
		
```console
host@host:~$ sudo systemctl restart zabbix-serve
```

#### 5. Importe o template para o zabbix
		
		O arquivo template_tcp_port_scan_lld.xml deve ser importado para o Zabbix.
		Após isso adicione no host a ser monitorado.
![monogafia-exemplo](https://user-images.githubusercontent.com/12739791/97092364-e19ba700-1619-11eb-97ab-712ec0fb7bb2.png)

### Erros

#### Não compativel em sistemas operacinais Windows

![monografia-erro](https://user-images.githubusercontent.com/12739791/97092567-5c18f680-161b-11eb-9919-1a8a6255a324.png)

	Correção

	Nesse caso, é necessário alterar o TimeOut do Zabbix
	Acesse o arquivo:
```console
host@host:~$ /etc/zabbix/zabbix_server.conf
```
	Procure por Timeout e altera o valor para 30
	Timeout=30

```console
host@host:~$ systemctl restart zabbix-server
```
	
	Depois disso, disassocie e limpe o template do host atualize e importe novamente.
