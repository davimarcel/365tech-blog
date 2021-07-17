#Instalando Haproxy em Amazon Linux

## Verifique se o `Yum` está atualizado:

```bash
yum check-update
```

## Instalando updates via `Yum`
```bash
yum update
```

## Instale o repository EPEL para HAProxy
```bash
yum install --enablerepo=epel haproxy
```


## Backup das configurações 

```bash
cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg_orig
cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg_backup
```

## Mudar as permissoões do haproxy.cfg_orig
```bash
chown ec2-user:ec2-user /etc/haproxy/haproxy.cfg_orig
```

## Editando as configurações do HAProxy
```bash
vim /etc/haproxy/haproxy.cfg_orig
```

## Exemplo das configurações HAProxy 
Isso permite o acesso via SSL e redireciona todo o HTTP para HTTPS. Ele também tem uma verificação de integridade nos rvidores com balanceamento de carga. E uma página de status útil do HAProxy.

```bash

global
    log         127.0.0.1 local2
 
    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     50000
    user        haproxy
    group       haproxy
    daemon
	 
	    # turn on stats unix socket
	    stats socket /var/lib/haproxy/stats
	 
	defaults
	    mode                    tcp
	    log                     global
	    option                  dontlognull
	    retries                 9999
	    timeout queue           1m
	    timeout connect         10s
	    timeout client          1m
	    timeout server          1m
	    timeout check           5s
	    maxconn                 15000
	 
	 
	#-----------------------------------
	# status page.
	#-----------------------------------
	listen stats 0.0.0.0:8000
	    mode http
	    stats enable
	    stats uri /haproxy
	    stats realm HAProxy
	 
	#-----------------------------------
	# Incoming HTTP / port 80
	#-----------------------------------
	listen IncomingHTTP
	    mode http
	    bind :80
	    redirect location https://www.example.com code 301
	 
	#-----------------------------------
	# Incoming HTTPS / port 443
	#-----------------------------------
	listen IncomingHTTPS
	    mode tcp
	    bind :443
	    option ssl-hello-chk
	    balance source
	    option httpchk GET /healthcheck HTTP/1.1\r\nHost:\ www.example.com
	    server ec2-server-1 ec2-xxx-xxx-xxx-xxx.eu-west-1.compute.amazonaws.com:443 check port 80 maxconn 5000
	    server ec2-server-2 ec2-xxx-xxx-xxx-xxx.eu-west-1.compute.amazonaws.com:443 check port 80 maxconn 5000
```

## Colocando em produção
```
cp /etc/haproxy/haproxy.cfg_orig /etc/haproxy/haproxy.cfg
```

## Iniciando HAProxy
```sh
service haproxy start
```
## Verificar Status
```sh
service haproxy status
```
## Parando HAProxy
```sh
service haproxy stop
```


## Security Groups
A configuração acima exigiria um `security group` 

* Allow port 22 from your office IP e.g. XXX.XXX.XXX.XXX/32
* Allow 8000 access from your office IP
* Allow HTTP (port 80) access from everyone e.g. 0.0.0.0/0
8 Allow HTTPS (port 443) access from everyone

!!! Nota
    *Sua configuração HAProxy exigirá uma configuração de grupos de segurança diferente*
