 ----------
  #Comandos
 ----------

# Generacion de clusters


	> pm2 start ./src/server.js --name="8082" -i 2 -p 8082

	> pm2 start ./src/server.js --name="8082" -i 2 -p 8083 -f

	> pm2 start ./src/server.js --name="8082" -i 2 -p 8084 -f

	> pm2 start ./src/server.js --name="8082" -i 2 -p 8085 -f


# Listamos

	> pm2 list



# Editamos el archivo /nginx/nginx.conf

	http {

		include       mime.types;
		default_type  application/octet-stream;
	
		upstream backend {
			server 127.0.0.1:8082;
			server 127.0.0.1:8083;
			server 127.0.0.1:8084;
			server 127.0.0.1:8085;
		}
	
		server {
			listen 8080;
			server_name nginx_node;
			root  C:/Users/User/nginx_app/public;

			location /api/randoms/ {
				proxy_pass http://backend/api/randoms/;
			}
		}
	}

# Frenamos e iniciamos el servicio nginx

	> nginx -s stop | nginx -s quit | nginx -s reload

	> nginx

# Accedemos a la URL

	http://localhost:8080/api/randoms/

# Monitoreamos el Process List

	> pm2 monit

Logueamos en consola la frase "Lista generada" para identificar que puerto nos esta respondiendo
