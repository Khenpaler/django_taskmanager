# Django Task Manager API

A Django REST API for task management.

## Deployment to Render

This project is configured for deployment on [Render](https://render.com/).

### Prerequisites

- A Render account
- Git repository with your code

### Deployment Steps

1. **Push your code to a Git repository** (GitHub, GitLab, etc.)

2. **Create a new Web Service on Render**:
   - Log in to your Render account
   - Click "New +" and select "Web Service"
   - Connect your Git repository
   - Fill in the details:
     - Name: `django-taskmanager-api` (or your preferred name)
     - Environment: `Python`
     - Region: Choose the one closest to your users
     - Branch: `main` (or your deployment branch)
     - Build Command: `./build.sh`
     - Start Command: `gunicorn django_taskmanager_api.wsgi:application`

3. **Configure Environment Variables**:
   - Set the following environment variables in the Render dashboard:
     - `SECRET_KEY`: A secure random string
     - `DEBUG`: False
     - `ALLOWED_HOSTS`: Your render domain, e.g., `your-app-name.onrender.com`
     - `CORS_ALLOWED_ORIGINS`: The URL of your frontend, e.g., `https://your-frontend-app.onrender.com`

4. **Set up a PostgreSQL Database**:
   - In the Render dashboard, go to "New +" and select "PostgreSQL"
   - Configure your database with a name, user, and password
   - Once created, get the "Internal Database URL" from the database info page
   - Add it as the `DATABASE_URL` environment variable to your web service

5. **Deploy**:
   - Click "Create Web Service" and wait for the deployment to complete

### Automatic Deployment with render.yaml

Alternatively, you can use the included `render.yaml` file for Blueprint deployment:

1. In the Render dashboard, go to "Blueprints" and click "New Blueprint Instance"
2. Connect your Git repository
3. Render will automatically detect the `render.yaml` file and configure all services
4. Review the settings and deploy

## Local Development

To run the project locally:

1. Create a virtual environment:
   ```
   python -m venv env
   source env/bin/activate  # On Windows: env\Scripts\activate
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Create a `.env` file based on `.env.example` and update values

4. Run migrations:
   ```
   python manage.py migrate
   ```

5. Start the development server:
   ```
   python manage.py runserver
   ```

## API Documentation

Access the API documentation at `/swagger/` or `/redoc/` when running the application. 