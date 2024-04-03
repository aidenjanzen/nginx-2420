# Installing Nginx and running a webpage.
On your new droplet, (ssh into it)
1. Install Vim and Nginx
    First update your system.\
        `sudo pacman -Syu`\
    Then install vim, vim is a text editor used to edit files in your terminal.\
        `sudo pacman -S vim` \
    Last install nginx, this is what will be running your webpage.\
        `sudo pacman -S nginx`

2. Create a webpage directory\
    Use `cd` to go into your home directory\
    Run the command `sudo mkdir -p /web/html/nginx-2420`\
    This will create the folder `nginx-2420` in your root directory\
    `-p` creates the parent folders\
    and\
    `cd /web/html/nginx-2420`
    This is where your website html will go.

3. Adding html
    Usee sftp or `sudo touch index.html` to create your own html template.
    use `sudo vim index.html` to access the file
    An example is shown below:
```html
<!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>2420</title>
        <style>
            * {
                color: #db4b4b;
                background: #16161e;
            }
            body {
                display: flex;
                align-items: center;
                justify-content: center;
                height: 100vh;
                margin: 0;
            }
            h1 {
                text-align: center;
                font-family: sans-serif;
            }
        </style>
    </head>
    <body>
        <h1>All your base are belong to us</h1>
    </body>
    </html>
```

5. To enable your html you need to create two folders:
`sudo  mkdir /etc/nginx/sites-available`
`sudo  mkdir /etc/nginx/sites-enabled`
`cd /etc/nginx/sites-available`
this is where to create your server block to listen for your port and run your server
`sudo touch nginx-2420.conf` NOTE: you can name nginx-2420 to your server name
1sudo vim nginx-2420.conf`

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name 64.23.154.72;
    root /web/html/nginx-2420;
    location / {
        index index.php index.html index.htm;
    }
}
```

6. `sudo vim /etc/nginx/nginx.conf`
at the end of your 

http {
    ...
    include sites-enabled/*;
}
you will also need to remove the default server block
```
server {
    listen       80;
    server_name  localhost;
    ...
}
```
To enable a site, simply create a symlink:

sudo ln -s /etc/nginx/sites-available/nginx-2420.conf /etc/nginx/sites-enabled/nginx-2420.conf

To disable a site, unlink the active symlink:

sudo unlink /etc/nginx/sites-enabled/nginx-2420.conf


4. Restart your service\
    `sudo systemctl restart nginx.service`

4. Go to your webpage
    `ip a`
    and use port `:80`

systemd components, systemctl commands.


