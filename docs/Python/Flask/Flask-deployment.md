Flask- Live deployment (GPT-undeited)

### 1. **Use a WSGI Server (e.g., Gunicorn or uWSGI)**
Flask, in production, should be served using a WSGI server like **Gunicorn** or **uWSGI**, not the built-in Flask server. This server will handle the requests and responses efficiently, allowing you to serve multiple clients and handle more traffic.

#### Install Gunicorn:
```bash
(venv) $ pip install gunicorn
```

You can then run your app using Gunicorn:
```bash
(venv) $ gunicorn -w 4 -b 127.0.0.1:8000 microblog:app
```
Here:
- `-w 4` tells Gunicorn to run 4 worker processes.
- `-b 127.0.0.1:8000` binds the server to the specified IP and port.
- `microblog:app` specifies the entry point for the WSGI app (the `app` object from `microblog.py`).

### 2. **Configure Nginx**
Nginx will serve as a reverse proxy, forwarding requests from the outside world to your Flask app running on Gunicorn. It will also handle static files efficiently.

#### Nginx Configuration:
1. **Install Nginx** on your server:
   ```bash
   $ sudo apt install nginx
   ```

2. **Create an Nginx server block** configuration file for your app:
   Create a file in `/etc/nginx/sites-available/`:
   ```bash
   $ sudo nano /etc/nginx/sites-available/microblog
   ```

   Add the following configuration:
   ```nginx
   server {
       listen 80;
       server_name your_domain_or_IP;

       location / {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }

       location /static {
           alias /path/to/microblog/app/static;
       }
   }
   ```

   Replace `your_domain_or_IP` with your server’s IP address or domain name. Also, update the path for `/static` to point to where your static files are located in your Flask app.

3. **Enable the site** by creating a symlink in the `sites-enabled` directory:
   ```bash
   $ sudo ln -s /etc/nginx/sites-available/microblog /etc/nginx/sites-enabled
   ```

4. **Restart Nginx** to apply the changes:
   ```bash
   $ sudo systemctl restart nginx
   ```

### 3. **Use Environment Variables**
In production, you’ll likely need to switch from the `.env` file to actual system environment variables for security. Instead of using `python-dotenv`, you can set environment variables directly on the server.

#### Set environment variables (example for Linux):
```bash
$ export FLASK_APP=microblog.py
$ export FLASK_ENV=production
```

Alternatively, add them to `/etc/environment` or create a systemd service file for running the application, which would automatically set the environment variables when starting the app.

### 4. **Configure Gunicorn as a Service**
To ensure your app starts on boot and is always running, you can set Gunicorn to run as a service using **systemd**.

1. Create a **systemd service file**:
   ```bash
   $ sudo nano /etc/systemd/system/microblog.service
   ```

   Add the following:
   ```ini
   [Unit]
   Description=Gunicorn instance to serve microblog
   After=network.target

   [Service]
   User=your_user
   Group=www-data
   WorkingDirectory=/path/to/microblog
   Environment="PATH=/path/to/microblog/venv/bin"
   ExecStart=/path/to/microblog/venv/bin/gunicorn --workers 4 --bind 127.0.0.1:8000 microblog:app

   [Install]
   WantedBy=multi-user.target
   ```

2. **Start and enable the service**:
   ```bash
   $ sudo systemctl start microblog
   $ sudo systemctl enable microblog
   ```

### 5. **Security Considerations**
- Make sure your Flask app runs in `production` mode (`FLASK_ENV=production`).
- Set up a firewall to only allow HTTP/HTTPS traffic.
- Use HTTPS with Nginx by setting up SSL certificates (e.g., via **Let’s Encrypt**).

---

### Summary of Steps:
1. Install Gunicorn or uWSGI to serve your Flask app.
2. Configure Nginx as a reverse proxy to forward requests to your WSGI server.
3. Set up environment variables properly.
4. Optionally configure systemd to ensure the app runs on boot.

This setup allows your Flask app to handle real-world traffic efficiently and securely on a Linux server with Nginx.
