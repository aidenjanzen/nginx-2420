# Installing Nginx and running a webpage.
On your new droplet, (ssh into it)
1. Install Vim and Nginx.
    First update your system.\
        `sudo pacman -Syu`\
    Then install vim, vim is a text editor used to edit files in your terminal.\
        `sudo pacman -S vim` \
    Last install nginx, this is what will be running your webpage.\
        `sudo pacman -S nginx`

2. Create a web page directory.\
    Use `cd` to go into your home directory\
    Run the command `sudo mkdir -p /web/html/nginx-2420`\
    This will create the folder `nginx-2420` in your root directory.\
    `-p` creates the parent folders\
    Use `cd /web/html/nginx-2420` to enter the folder for your html.

3. Add HTML.\
    Use sftp or `sudo touch index.html` to create your own html template.\
    Use `sudo vim index.html` to access the file\
    An example html page is shown below:
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

4. Enable HTML\
    To enable your html you need to create two folders:\
    `sudo  mkdir /etc/nginx/sites-available`\
    `sudo  mkdir /etc/nginx/sites-enabled`\
    This allows you to easily create websites and enable them or disable them.\
    `cd /etc/nginx/sites-available`\
    This is where you create your server block to listen for your port and run your page.\
    `sudo touch nginx-2420.conf` \
    This creates your server block file.\
    **NOTE:** you can name nginx-2420 to your server name.\
    To enter the file: `sudo vim nginx-2420.conf`\
    An example server block is shown below:

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

5. Enable the server block \
    You need allow nginx to see your server block:\
    Use `sudo vim /etc/nginx/nginx.conf`\
    Include `include sites-enabled/*;` at the end of your http block in the nginx.conf file.
```nginx
http {
    ...
    include sites-enabled/*;
}
```
You will also need to remove the default server block.
```nginx
server { #remove this
    listen       80;
    server_name  localhost;
    ...
}
```
6. Enable your site.\
    Using the name of your conf file run this command to create a symlink.
    `sudo ln -s /etc/nginx/sites-available/nginx-2420.conf /etc/nginx/sites-enabled/nginx-2420.conf`\
    **NOTE:** to disable a site, unlink the active symlink using:
    `sudo unlink /etc/nginx/sites-enabled/nginx-2420.conf`


7. Restart your service\
    `sudo systemctl restart nginx.service`\
    or use sudo systemctl start nginx.service` if you haven't started it yet.

8. Go to your webpage
    `ip a`
    and use port `:80`

systemd components, systemctl commands.


