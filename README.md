# UAP TIS TI-D
dikerjakan oleh:
235150707111046 - Andhika Pratama Putra

235150707111057 - Bagus Setiawan 

225150707111070 - Davy Julian Ibrahim 

# Laravel Lumen Application

This is a Laravel Lumen-based application that requires several prerequisites and setup steps before it can be run.

## Prerequisites

- PHP >= 8.1
- Composer (PHP package manager)
- MySQL or another compatible database system
- Web server (Apache/Nginx) or PHP's built-in server

## Installation Steps

1. **Clone the repository**
   ```bash
   git clone [repository-url]
   cd [project-directory]
   ```

2. **Install PHP dependencies**
   ```bash
   composer install
   composer require fruitcake/laravel-cors
   ```

3. **Environment Setup**
   - Copy the `.env.example` file to `.env`
   ```bash
   cp .env.example .env
   ```
   - Configure your database settings in the `.env` file:
     ```
     DB_CONNECTION=mysql
     DB_HOST=127.0.0.1
     DB_PORT=3306
     DB_DATABASE=your_database_name
     DB_USERNAME=your_username
     DB_PASSWORD=your_password
     ```

4. **Database Setup**
   - Create a new database using your preferred database management tool
   - Run database migrations:
   ```bash
   php artisan migrate
   ```

5. **Storage Permissions**
   - Ensure the storage directory is writable:
   ```bash
   chmod -R 775 storage
   ```

## API Endpoints Documentation

### Authentication Endpoints

#### 1. Register
- **URL**: `/uap/register`
- **Method**: `POST`
- **Auth Required**: No
- **Request Body**:
  ```json
  {
    "nim": "2021001",
    "nama": "John Doe",
    "angkatan": 2021,
    "password": "password123",
    "prodi_id": 1
  }
  ```

#### 2. Login
- **URL**: `/uap/login`
- **Method**: `POST`
- **Auth Required**: No
- **Request Body**:
  ```json
  {
    "nim": "2021001",
    "password": "password123"
  }
  ```
- **Response**: Returns JWT token for authenticated requests

### Protected Endpoints (Require JWT Token)

#### 1. Get All Students
- **URL**: `/uap/mahasiswa`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```

#### 2. Filter Students by Program
- **URL**: `/uap/mahasiswa/prodi/{id}`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```

#### 3. Get All Programs
- **URL**: `/uap/prodi`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```

#### 4. Get All Courses
- **URL**: `/uap/matkul`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```

#### 5. Add Course
- **URL**: `/uap/matkul/tambah`
- **Method**: `POST`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```
- **Request Body**:
  ```json
  {
    "matakuliah_id": 1
  }
  ```

#### 6. View My Courses
- **URL**: `/uap/matkul/saya`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```

## Running the Application

### Using PHP's built-in server
```bash
php -S localhost:8000 -t public
```

### Using Apache/Nginx
- Configure your web server to point to the `public` directory
- Ensure the web server has proper permissions to access the application files

## Testing
```bash
php artisan test
```

## Additional Notes

- Make sure all required PHP extensions are installed:
  - BCMath PHP Extension
  - Ctype PHP Extension
  - JSON PHP Extension
  - Mbstring PHP Extension
  - OpenSSL PHP Extension
  - PDO PHP Extension
  - Tokenizer PHP Extension
  - XML PHP Extension

- For development, ensure you have the following tools installed:
  - Git
  - Composer
  - PHPUnit (for testing)

## Troubleshooting

If you encounter any issues:
1. Check if all prerequisites are met
2. Verify database connection settings
3. Ensure proper file permissions
4. Check PHP error logs for detailed error messages

## UAP v0.1
#### Endpoint Tanpa Otentikasi
- regis
POST /uap/register
- login
POST /uap/login

#### Endpoint yang Memerlukan Otentikasi (JWT)
- liat prodi
GET /uap/prodi
- liat mahasiswa
GET /uap/mahasiswa
- cek mahasiswa dari prodi id
GET /uap/mahasiswa/prodi/{id}
- liat matkul
GET /uap/matkul
- tambah matkul di akunmu
POST /uap/matkul/tambah
- liat matkul tambah
GET /uap/matkul/saya

