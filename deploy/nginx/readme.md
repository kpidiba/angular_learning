# Angular Deployment with Nginx on Windows

This guide provides a step-by-step approach to deploying an Angular application using Nginx on a Windows server.

## Prerequisites

- An Angular application built and ready for deployment.
- Nginx installed on a Windows server.
- Basic understanding of the command line and Nginx configuration.

## Step 1: Build the Angular Application

Before deploying, ensure that your Angular application is built for production.

1. Open the command prompt and navigate to your Angular project directory:

```bash
cd C:\path\to\your\angular\project
```

2. Build the project using the Angular CLI:

```prod
ng build --prod
```

1. This command will compile your Angular application into a set of static files optimized for production, typically located in the `dist/your-project-name` directory.

## Step 2: Install Nginx on Windows

If you haven't already installed Nginx on your Windows server, follow these steps:

1. Download the Nginx Windows binaries. ([nginx: download](https://nginx.org/en/download.html)) -stable version

2. Extract the downloaded ZIP file to a directory, e.g., `C:\nginx`.

3. add the folder to environment variable PATH

4. Open a command prompt and navigate to the Nginx directory:

```bash
cd C:\nginx; start nginx
```

## Step 3: Configure Nginx for Angular

To configure Nginx to serve your Angular application:

1. Open the `nginx.conf` file located in the `C:\nginx\conf` directory with a text editor.

2. Modify the `nginx.conf` file to include the following configuration:

```nginx
server {
    listen 80;
    server_name your_domain_or_ip;

    root C:/p`ath/to/your/angular/project/dist/your-project-name;

    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # Optional: Configure logging
    access_log C:/nginx/logs/access.log;
    error_log C:/nginx/logs/error.log;
}
```

1. - Replace `your_domain_or_ip` with your server's domain name or IP address.
   - Update the `root` directive to point to the directory where your Angular application was built.
2. Save the changes and exit the text editor.

another config

```nginx
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  www.faisceaux.tg;

        location / {
            root   C:/Faisceau/web;
            index  index.html;
            try_files $uri $uri/ /index.html;
        }

        # Proxy requests to /api to the backend server
        location /api/ {
            proxy_pass http://localhost:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }

        # Redirect server error pages to the static page /50x.html
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   C:/Faisceau/web;
        }
    }
}


```

## Step 4: Start/Restart Nginx

After configuring Nginx, you need to start or restart the server to apply the changes.

1. If Nginx is already running, restart it by running the following command in the command prompt:

```bash
nginx -s reload
```

2. If Nginx is not running, start it using:

```bash
start nginx
```

## Step 5: Access Your Angular Application

Once Nginx is running with the correct configuration, you can access your Angular application by navigating to your server's IP address or domain name in a web browser:

```arduino
http://your_domain_or_ip
```

## TEST CONFIG FILE

```bash
nginx -t
```

## **How to Install SSL on NGINX Locally:**

1. **Generate a Self-Signed SSL Certificate:**

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/selfsigned.key \
-out /etc/ssl/certs/selfsigned.crt
```

Follow the prompts for certificate details.

2. **Configure NGINX:**  
   Edit your NGINX config (e.g., `/etc/nginx/sites-available/angular-app`):

```nginx
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate /etc/ssl/certs/selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/selfsigned.key;

    root /var/www/angular-app/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}

server {
    listen 80;
    server_name localhost;
    return 301 https://$host$request_uri;
}

```

**Restart NGINX:**

```bash
sudo nginx -t
sudo systemctl restart nginx
```

4. **Access the App:**  
   Visit `https://localhost` (you’ll likely get a browser warning due to the self-signed certificate).



## Troubleshooting

- **Nginx not starting:** Check the error logs located in `C:\nginx\logs\error.log` for details on what might be causing the issue.
- **404 Not Found Errors:** Ensure that the `root` path in your Nginx configuration is correct and points to the directory containing the `index.html` file.

## Conclusion

You have successfully deployed an Angular application using Nginx on a Windows server. This setup allows your Angular application to be served efficiently with Nginx handling the static content.
