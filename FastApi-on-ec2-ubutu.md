provided you've ssh acccess to your server

<!-- Update Apt and install required pkg -->
sudo apt-get update
sudo apt install python3.12-venv nginx -y 

<!-- configure nginx server  -->
sudo vim /etc/nginx/sites-enabled/fastapi_nginx

<!--config template -->
server{ 
	listen 80;
	server_name 204.236.222.95;
        location / {
                proxy_pass [SEREVR_PUBLIC_IP];
		        proxy_set_header Host $host;
       		    proxy_set_header X-Real-IP $remote_addr;
        	    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        	    proxy_set_header X-Forwarded-Proto $scheme;
        }
}


<!-- restart ngix service -->
sudo service nginx restart