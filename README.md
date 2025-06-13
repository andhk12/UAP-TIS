# UAP TIS TI-D
dikerjakan oleh:

1. 235150707111046 - Andhika Pratama Putra

2. 235150707111057 - Bagus Setiawan 

3. 225150707111070 - Davy Julian Ibrahim 

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
   php artisan db:seed
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
![Screenshot 2025-06-12 204136](https://github.com/user-attachments/assets/de553b94-2a66-4088-ab9a-2cb3665802c5)

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
![Screenshot 2025-06-12 204915](https://github.com/user-attachments/assets/58575062-5fb6-45af-bca2-91cc3cf0c226)

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
![Screenshot 2025-06-12 204939](https://github.com/user-attachments/assets/78f9e286-5f6d-4e86-a3ba-5f2a79237488)

#### 2. Filter Students by Program
- **URL**: `/uap/mahasiswa/prodi/{id}`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```
![Screenshot 2025-06-12 205029](https://github.com/user-attachments/assets/479d28ce-8c79-498f-acd0-82faadc20790)

#### 3. Get All Programs
- **URL**: `/uap/prodi`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```
![Screenshot 2025-06-12 205112](https://github.com/user-attachments/assets/a693017e-9a5b-4e16-91d1-5d89c49fdba4)

#### 4. Get All Courses
- **URL**: `/uap/matkul`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```
![Screenshot 2025-06-12 205139](https://github.com/user-attachments/assets/5c991c05-670e-4762-91f4-34017dc4b85f)

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
![Screenshot 2025-06-12 205343](https://github.com/user-attachments/assets/2ba259ef-b22c-4a84-9036-241b2d9004cb)

#### 6. View My Courses
- **URL**: `/uap/matkul/saya`
- **Method**: `GET`
- **Auth Required**: Yes
- **Headers**: 
  ```
  Authorization: Bearer <your_jwt_token>
  ```
![Screenshot 2025-06-12 205409](https://github.com/user-attachments/assets/cc59bc88-906c-42ad-86ed-49151a939e00)

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

## ERD
![ERD](https://github.com/user-attachments/assets/baa5d86c-06b5-4880-9fb7-ccdaa238f839)

Tabel:

o	mahasiswas: Menyimpan data mahasiswa dengan nim sebagai primary key dan prodi_id sebagai foreign key.

o	prodis: Tabel master untuk program studi.

o	matakuliahs: Tabel master untuk mata kuliah.

o	mahasiswa_matakuliah: Tabel pivot yang menghubungkan mahasiswa_nim.


o	Model Mahasiswa: 

 - Memiliki relasi belongsTo(Prodi::class) (satu mahasiswa punya satu prodi).
 - Memiliki relasi belongsToMany(Matakuliah::class) (satu mahasiswa bisa mengambil banyak matkul).
   
o	Model Matakuliah: 

 - Juga memiliki relasi belongsToMany(Mahasiswa::class).
