# Blog API

A RESTful API for a blogging platform built with Django Rest Framework.

## Features

- User registration and authentication with JWT
- CRUD operations for blog posts
- Author-based permissions (only authors can edit/delete their posts)
- Image upload functionality for posts
- API pagination
- Dockerized application

## Technologies Used

- Django 3.x
- Django Rest Framework
- PostgreSQL
- JWT Authentication
- Docker & Docker Compose

## API Endpoints

### Authentication
- `POST /api/register/` - User registration
- `POST /api/token/` - User login (JWT token)
- `POST /api/token/refresh/` - Refresh JWT token

### Blog Posts
- `GET /api/posts/` - List all posts (paginated)
- `POST /api/posts/` - Create a new post (authenticated users only)
- `GET /api/posts/<id>/` - Retrieve a specific post
- `PUT /api/posts/<id>/` - Update a post (only by post author)
- `DELETE /api/posts/<id>/` - Delete a post (only by post author)

## Setup Instructions

### Using Docker (recommended)

1. Clone the repository:
```bash
git clone https://github.com/yourusername/blog-api.git
cd blog-api
```

2. Build and run the Docker containers:
```bash
docker-compose up --build
```

3. The API will be available at http://localhost:8000/api/

### Manual Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/blog-api.git
cd blog-api
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Configure PostgreSQL:
   - Create a PostgreSQL database named `blog_api`
   - Update the database configuration in `settings.py` if needed

5. Run migrations:
```bash
python manage.py migrate
```

6. Start the development server:
```bash
python manage.py runserver
```

7. The API will be available at http://localhost:8000/api/

## API Usage Examples

### Register a new user
```bash
curl -X POST http://localhost:8000/api/register/ \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser", "password":"TestPass123", "password2":"TestPass123", "email":"test@example.com", "first_name":"Test", "last_name":"User"}'
```

### Get JWT token (login)
```bash
curl -X POST http://localhost:8000/api/token/ \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser", "password":"TestPass123"}'
```

### Create a new post
```bash
curl -X POST http://localhost:8000/api/posts/ \
  -H "Authorization: Bearer <your_token>" \
  -H "Content-Type: application/json" \
  -d '{"title":"My First Post", "content":"This is the content of my first post"}'
```

### List all posts
```bash
curl -X GET http://localhost:8000/api/posts/
```

### Get a specific post
```bash
curl -X GET http://localhost:8000/api/posts/1/
```

### Update a post
```bash
curl -X PUT http://localhost:8000/api/posts/1/ \
  -H "Authorization: Bearer <your_token>" \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated Post Title", "content":"Updated content"}'
```

### Delete a post
```bash
curl -X DELETE http://localhost:8000/api/posts/1/ \
  -H "Authorization: Bearer <your_token>"
```