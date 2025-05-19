# Django App Containerization

## Description
A repository with a step-by-step guide on how to dockerize a Django app and deploy it to a V-Server. This README guides you on how to serve the app, install dependencies, create a Docker container, and deploy it to a V-Server.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Quick start](#quick-start)
3. [Usage](#usage)
    - [Create a docker container](#create-a-docker-container)
    - [Deploy the app to a V-Server](#deploy-the-app-to-a-v-server)
    - [Create a superuser](#create-a-superuser)

4. [Project Checklist](#project-checklist)

## Prerequisites

Before starting the dockerization of this app, make sure you have `Docker` installed, access to a V-Server for deployment, and the corresponding `ip_address`, `user_name`, and `password` or `SSH Keys` to log in.

- A user with `sudo` rights
- Docker installed in your V-Server
- GitHub account to connect via `SSH keys`
- Connection from your V-Server to GitHub with `SSH Keys`

## Quick start

Clone this repository to your local machine and follow the README.md instructions.

Open your command line and type the following commands:

```
# With SSH configured (if SSH Keys are provided to GitHub)

    git clone git@github.com:MarcosChavez09/baby-tools-shop.git

# Classic HTTPS (if no SSH Keys are provided to GitHub)

    git clone https://github.com/MarcosChavez09/baby-tools-shop.git
```
After cloning the repository, navigate to:

```
    cd baby-tools-shop/babyshop_app
```

Create you virtual environment:

```
# /baby-tools-shop/babyshop_app

# On macOS
    python3 -m venv .venv

# On Linux
    python -m venv .venv
```

Activate your venv:
```
    source .venv/bin/activate
```

FYI: To deactivate your venv, just type `deactivate` in the command line.

Install dependencies:
```
    pip install -r requirements.txt
```
Run migrations:
```
# On macOS
   python3 manage.py migrate

# On Linux
   python manage.py migrate
```
Start the development server:
```
   python manage.py runserver
```

Open the link http://localhost/

## Usage

### Create a docker container

To create a docker container follow the next steps under `baby-tools-shop/babyshop_app`.

1. Create the docker image: 

```
    docker build -t babyshop_app .
```

2. Run the docker container:
```
    docker run -p 8025:8025 babyshop_app                                        
```

3. Open the container in your browser by visiting http://localhost:8025

### Deploy the app to a V-Server

1. Navigate to `babyshop/settings.py`, find `ALLOWED_HOSTS` and add your `<ip_server_address>`

```
# settings.py

    ALLOWED_HOSTS = ['ip_server_address', 'localhost', '127.0.0.1']
```
2. Loging to your V-Server
```
    ssh -i ~/.ssh/<name_of_your_key25519> <your_user_name>@<ip_server_address>
```
3. Create a new folder in your `home` directory and clone this repository there
```
      mkdir -p ~/projects
    cd ~/projects
    git clone git@github.com:MarcosChavez09/baby-tools-shop.git
```

3. Install docker on your V-Server if you haven't done so yet. 

4. Repeat the steps listed in "Create a docker container"

5. Visit the link `http://<ip_server_address>:8025`

### Create a superuser

With your `container` running, type the following in your command line:

Note: You will need the `<container_id_or_name>` to create a superuser. Type `docker ps` in your command line and copy the `<container_id_or_name>`.

```
    docker exec -it <container_id_or_name> python manage.py createsuperuser
```

When prompted, provide your `<user_mname>`, `<user_email>` and a `<password>`.

After successfully adding your superuser, open your browser at http://localhost:8025/admin. You will be redirected to the admin page. Log in with the given information.

## Project Checklist

- 📄 [Checklist (PDF)](../baby-tools-shop/docs/checklist.pdf)