

# Django Notes App

This repository contains a Dockerized Django notes application with Nginx and MySQL.

## Dockerfile Tasks

- **Base Image**: Use Python 3.9.
- **Working Directory**: Set to `/app/backend`.
- **Dependencies**: Install system and Python dependencies.
- **Application Code**: Copy application code to the container.
- **Expose Port**: Expose port 8000.

## Build the App

```bash
docker build --no-cache -t notes-app .
```

## Docker Compose Tasks

This Docker Compose file sets up a multi-container application with Nginx, Django, and MySQL.

### Nginx Service
- **Build**: From `./nginx` directory.
- **Image**: `nginx`.
- **Ports**: Map port 80.
- **Restart Policy**: Always restart.
- **Depends On**: Start after `django_app`.
- **Network**: Connect to `notes-app`.

### Django App Service
- **Build**: From the current directory.
- **Image**: `django_app`.
- **Ports**: Map port 8000.
- **Command**: Run migrations and start Gunicorn server.
- **Environment File**: Load from `.env`.
- **Depends On**: Start after `db`.
- **Restart Policy**: Always restart.
- **Healthcheck**: Check if the Django app is running.
- **Network**: Connect to `notes-app`.

### MySQL Database Service
- **Image**: `mysql`.
- **Environment**: Set root password and database name.
- **Volumes**: Persist data to `./data/mysql/db`.
- **Healthcheck**: Check if MySQL is running.
- **Network**: Connect to `notes-app`.

### Networks
- **notes-app**: Custom network for the application.

Here's the revised section:

---

## Credits

<h2>Credits</h2>

<p style="font-size: 16px;">
While we built the Dockerfile and Docker Compose configurations from scratch to learn and apply Docker skills, the original credit for the application goes to Londhe Shubham.
</p>


**The original source code for the Django notes application was inspired by [LondheShubham153's repository](https://github.com/LondheShubham153/django-notes-app).**


```
https://github.com/LondheShubham153/django-notes-app
```