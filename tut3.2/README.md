# Installing a Firewall and Backend Server on Nginx
## To Install the Firewall:
To install ufw use:\
`sudo pacman -Syu ufw`

To start the service:\
`sudo systemctl enable --now ufw.service`\
WARNING DO NOT ENABLE FIREWALL IF USING SSH:
`sudo ufw enable`\

To allow SSH through firewall:\
`sudo ufw allow ssh`\
To allow ssh to block if more than 6 requests are made:\
`sudo ufw limit ssh`\
To allow HTTP:\
`sudo ufw allow http`\
To enable the firewall:\
`sudo ufw enable`\
To check the status of the firewall:\
`sudo ufw status verbose`\

## Configuring the backend:
Using sftp get the downloaded `hello-server` file on your droplet\
Make the binary file executable with: \
`chmod +x hello-server`\
If you file is not already there create a new folder in your nginx folder\
This is where we have our sites-enabled folders\
`sudo mkdir sites-backend`\
and move it there with\
`sudo mv hello-server /etc/nginx/sites-backend `

In your `/etc/systemd/system` folder do \
`sudo touch backend.service `
and \
`sudo vim backend.service`

In this file make the new service file to run the hello-server backend

```plaintext
    [Unit]
    Description=Http Hello-Server script

    [Service]
    Type=oneshot
    ExecStart=/etc/nginx/sites-backend/hello-server 

    [Install]
    WantedBy=multi-user.target
```
Make sure to reload the services\
`sudo systemctl daemon-reload`\
To start the backend do:\
`sudo systemctl start backend.service`

## Adding the reverse proxy
server {
    listen 80;
    listen [::]:80;
    server_name 64.23.154.72;
    root /web/html/nginx-2420;
    location / {
    index index.php index.html index.htm;
    }

location /hey {
        # Define the reverse proxy settings
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

location /echo {
        # Define the reverse proxy settings
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}


sudo systemctl restart nginx