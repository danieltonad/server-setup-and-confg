
# Setting Up FastAPI on an EC2 Instance

## Prerequisites
- SSH access to your server

## Steps

### 1. Update APT and Install Required Packages

First, update the package lists and install Python 3.12 and Nginx:

```sh
sudo apt-get update
sudo apt install python3.12-venv nginx -y
```

### 2. Configure Nginx Server

Next, configure Nginx to serve your FastAPI application. Open the Nginx configuration file for editing:

```sh
sudo vim /etc/nginx/sites-enabled/fastapi_nginx
```

Add the following configuration to the file:

```nginx
server {
    listen 80;
    server_name 0.0.0.0; # Replace with your server's public IP address or domain name

    location / {
        proxy_pass http://127.0.0.1:8000; # Replace with your FastAPI server's internal IP and port if different
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### 3. Restart Nginx Service

Finally, restart the Nginx service to apply the changes:

```sh
sudo service nginx restart
```

### 4. Clone FastApi Project 

Clone your project 

```sh
git clone <project_url>
cd <project_path>
```

### 4. Setting Up Environment and Installing Dependecies

Setup environment and activate

```sh
python3 -m venv env
source ./env/bin/activate
```

Install requirements

```sh
pip3 install -r requirements.txt
```


### 4. Start Uvicorn Server

Start Uvicorn Server

```sh
uvicorn <main_file>:<app> 
```

## Extra Info
You can use `screen` to keep your application running even after your terminate your ssh connection
```sh
    screen -S <screen_name> #new screen
    #ctrl + A then D to detach screen
    screen -r <screen_name> #resume screen
```

---