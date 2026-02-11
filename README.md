# JagaKucing Backend

Backend API service for the JagaKucing application, built with Laravel and Docker.

## 🚀 Getting Started

### Prerequisites
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd jagakucing-backend
   ```

2. **Setup Environment Variables**
   ```bash
   cp .env.example .env
   ```
   *Note: The default `.env.example` is pre-configured for the Docker environment.*

3. **Start the Application**
   ```bash
   docker compose up -d --build
   ```

4. **Initialize Application**
   Run the following commands to generate the app key and run database migrations:
   ```bash
   docker compose exec jagakucing-app php artisan key:generate
   docker compose exec jagakucing-app php artisan migrate
   ```

## 🛠 Services & Ports

| Service | Internal Port | Host Port | URL / Access |
|---------|---------------|-----------|--------------|
| **API / Web** | 80 | **8010** | http://localhost:8010 |
| **PostgreSQL** | 5432 | **3320** | `localhost:3320` |
| **Redis** | 6379 | **6390** | `localhost:6390` |
| **Mailpit** | 8025 | **8040** | http://localhost:8040 |

### 🗄️ Database Credentials
You can connect using TablePlus, DBeaver, or any SQL client:
- **Host**: `127.0.0.1`
- **Port**: `3320`
- **Database**: `jagakucing`
- **Username**: `jagakucing`
- **Password**: `password`

## 📡 API Documentation

### Authentication

#### 1. Login
**POST** `/api/login`

**Body:**
```json
{
    "email": "user@example.com",
    "password": "password"
}
```

**Response:**
```json
{
    "access_token": "1|3Wpqu5cJ...",
    "token_type": "Bearer",
    "user": { ... }
}
```

#### 2. Get User Profile
**GET** `/api/user`
- **Headers**: `Authorization: Bearer <access_token>`

#### 3. Logout
**POST** `/api/logout`
- **Headers**: `Authorization: Bearer <access_token>`

## 🧪 Running Tests

To run the test suite:
```bash
docker compose exec jagakucing-app php artisan test
```

## 📝 Useful Commands

**Access the container shell:**
```bash
docker compose exec jagakucing-app bash
```

**Run Artisan commands:**
```bash
docker compose exec jagakucing-app php artisan <command>
```

**Create a test user:**
```bash
docker compose exec jagakucing-app php artisan tinker --execute="User::factory()->create(['email' => 'test@example.com', 'password' => 'password']);"
```
