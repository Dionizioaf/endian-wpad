# Configurar o Endian community para entregar um WPAD customizado

Criei esta implementação para que seja possível entregar um wpad customizado para os computadores que utilizam o proxy.

## Etapas

- Acessar o diretório do HTTPD
  - `cd /etc/httpd/conf.plain`

Iremos utilizar o diretório conf.plain, para que seja possível entregar o WPAD na porta 80 (HTTP)

- **copiar ou criar o arquivo custom.conf na pasta**
- Acessar o diretório do html

  - `cd /home/httpd/html`
- Criar um diretório

  - `mkdir custom`
- Entrar no diretório

  - `cd custom`
- Copiar/criar o wpad.dat para a pasta

  - **Alterar o ip de lan do endian**
- Reiniciar o httpd

  - `/etc/init.d/httpd restart`
- Acessar o arquivo

  - **http://[ip_do endiad]/custom/wpad.dat**

## Comando completo

```
echo "Alias /custom /home/httpd/html/custom" > /etc/httpd/conf.plain/custom.conf
echo "<Directory /home/httpd/html/ammo>" >> /etc/httpd/conf.plain/custom.conf
echo "    Order allow,deny" >> /etc/httpd/conf.plain/custom.conf
echo "    Allow from all" >> /etc/httpd/conf.plain/custom.conf
echo "</Directory>" >> /etc/httpd/conf.plain/custom.conf
mkdir /home/httpd/html/custom
echo "function FindProxyForURL(url, host) {return "PROXY [ip_do_endia]:8080";}" > /home/httpd/html/custom/wpad.dat
/etc/init.d/httpd restart
```

## Links adicionais

- https://help.endian.com/hc/en-us/articles/360011796214-How-to-use-WPAD-Web-Proxy-Auto-Discovery-Protocol-
- https://help.endian.com/hc/en-us/articles/224528707-How-to-customize-Endian-PAC-Proxy-Auto-Configuration-file
    - Exemplos de código para o arquivo wpad.dat
