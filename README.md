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
    `sudo mkdir -p /web/html/nginx-2420`\
    this will create the folders in your root directory, `-p` creates the parent folders\
    and\
    `cd /web/html/nginx-2420`
    This is where your website html will go.
    
3. Adding html
    Usee sftp or `touch index.html` to create your own html template.
    An example is shown below:
    ```
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

4. Start your service\
    `sudo systemctl start nginx.service`

4. Go to your webpage
    `ip a`
    and use port `:80`






Nginx configuration, including setting up a separate server block
systemd components, systemctl commands.


```
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
