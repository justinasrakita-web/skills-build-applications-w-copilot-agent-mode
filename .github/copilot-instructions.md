# GitHub Copilot Instructions for Octofit Tracker

## Overview
This repository contains the Octofit Tracker application, a multi-tier fitness tracker built with a Django backend and React frontend. The app includes features like user authentication, activity tracking, team management, leaderboards, and personalized workout suggestions.

## Repository Structure
```
octofit-tracker/
├── backend/  # Django backend
│   ├── venv/  # Python virtual environment
│   ├── octofit_tracker/  # Main backend app
└── frontend/  # React frontend
```

## Key Guidelines for AI Agents

### General
- **Never change directories**: Always point to the directory when issuing commands.
- **Forwarded ports**: Use the following ports:
  - 8000: public (backend)
  - 3000: public (frontend)
  - 27017: private (MongoDB)

### Backend (Django)
- **Environment Variables**:
  - Use `CODESPACE_NAME` to configure `ALLOWED_HOSTS` in `settings.py`.
  - Example:
    ```python
    import os
    ALLOWED_HOSTS = ['localhost', '127.0.0.1']
    if os.environ.get('CODESPACE_NAME'):
        ALLOWED_HOSTS.append(f"{os.environ.get('CODESPACE_NAME')}-8000.app.github.dev")
    ```
- **Serializers**:
  - Convert `ObjectId` fields to strings.
- **URLs**:
  - Use `CODESPACE_NAME` to dynamically generate the base URL.
  - Example:
    ```python
    import os
    codespace_name = os.environ.get('CODESPACE_NAME')
    if codespace_name:
        base_url = f"https://{codespace_name}-8000.app.github.dev"
    else:
        base_url = "http://localhost:8000"
    ```
- **Testing**:
  - Use `curl` to test REST API endpoints.

### Frontend (React)
- **Setup**:
  - Use the following commands to initialize the frontend:
    ```bash
    npx create-react-app octofit-tracker/frontend --template cra-template --use-npm
    npm install bootstrap --prefix octofit-tracker/frontend
    sed -i "1iimport 'bootstrap/dist/css/bootstrap.min.css';" octofit-tracker/frontend/src/index.js
    npm install react-router-dom --prefix octofit-tracker/frontend
    ```
- **Images**:
  - Use the app image located at `docs/octofitapp-small.png`.

### MongoDB
- **Service Management**:
  - Use `ps aux | grep mongod` to check if MongoDB is running.
  - Use `mongosh` as the official client tool.
- **Database Management**:
  - Always use Django's ORM for database structure and data creation.

## Developer Workflows

### Backend Setup
1. Create a Python virtual environment:
   ```bash
   python3 -m venv octofit-tracker/backend/venv
   ```
2. Activate the virtual environment and install dependencies:
   ```bash
   source octofit-tracker/backend/venv/bin/activate
   pip install -r octofit-tracker/backend/requirements.txt
   ```

### Frontend Setup
1. Navigate to the `frontend` directory and run the setup commands listed above.

### Testing
- Use `curl` for backend API testing.
- Use React Developer Tools for frontend debugging.

### Deployment
- Ensure `CODESPACE_NAME` is set for dynamic URL and host configuration.

## External Dependencies
- **Backend**:
  - Django, Django REST Framework, djongo (MongoDB connector)
- **Frontend**:
  - React, Bootstrap, React Router
- **Database**:
  - MongoDB

## Notes
- Follow the structure and guidelines strictly to ensure compatibility and maintainability.
- Refer to the `README.md` and `docs/` folder for additional context.