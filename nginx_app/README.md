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
	
	┌─────┬─────────┬─────────────┬─────────┬─────────┬──────────┬────────┬──────┬───────────┬──────────┬──────────┬──────────┬──────────┐
	│ id  │ name    │ namespace   │ version │ mode    │ pid      │ uptime │ ↺    │ status    │ cpu      │ mem      │ user     │ watching │
	├─────┼─────────┼─────────────┼─────────┼─────────┼──────────┼────────┼──────┼───────────┼──────────┼──────────┼──────────┼──────────┤
	│ 0   │ 8082    │ default     │ 1.0.0   │ cluster │ 17504    │ 21s    │ 0    │ online    │ 0%       │ 29.2mb   │ User     │ disabled │
	│ 1   │ 8082    │ default     │ 1.0.0   │ cluster │ 8536     │ 21s    │ 0    │ online    │ 0%       │ 28.8mb   │ User     │ disabled │
	│ 2   │ 8083    │ default     │ 1.0.0   │ cluster │ 18372    │ 14s    │ 0    │ online    │ 0%       │ 28.6mb   │ User     │ disabled │
	│ 3   │ 8083    │ default     │ 1.0.0   │ cluster │ 4224     │ 13s    │ 0    │ online    │ 0%       │ 28.6mb   │ User     │ disabled │
	│ 4   │ 8084    │ default     │ 1.0.0   │ cluster │ 4072     │ 6s     │ 0    │ online    │ 0%       │ 32.8mb   │ User     │ disabled │
	│ 5   │ 8084    │ default     │ 1.0.0   │ cluster │ 13624    │ 5s     │ 0    │ online    │ 0%       │ 32.7mb   │ User     │ disabled │
	│ 6   │ 8085    │ default     │ 1.0.0   │ cluster │ 12332    │ 0s     │ 0    │ online    │ 0%       │ 32.4mb   │ User     │ disabled │
	│ 7   │ 8085    │ default     │ 1.0.0   │ cluster │ 1612     │ 0s     │ 0    │ online    │ 0%       │ 32.2mb   │ User     │ disabled │
	└─────┴─────────┴─────────────┴─────────┴─────────┴──────────┴────────┴──────┴───────────┴──────────┴──────────┴──────────┴──────────┘



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
