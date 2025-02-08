# Flutter API and Flutter App Setup Guide

## Overview

This guide helps you set up a Laravel REST API and connect it to a Flutter application.

## Prerequisites

- **Laravel**: PHP and Composer installed.
- **Flutter**: Flutter SDK installed.
- **Database**: MySQL or SQLite.

## Laravel API Setup

### 1. Create Laravel Project

```bash
cd C:\laragon\www
composer create-project --prefer-dist laravel/laravel flutter_api
cd flutter_api
```

### 2. Set Up Database

1. Create a database named `flutter_api_db` in SQLyog.
2. Update `.env` file:

   ```env
   DB_CONNECTION=mysql
   DB_DATABASE=flutter_api_db
   DB_USERNAME=root
   DB_PASSWORD=
   ```

### 3. Install Sanctum

```bash
composer require laravel/sanctum
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
php artisan migrate
```

### 4. Set Up API Routes

In `routes/api.php`, add:

```php
Route::post('register', [AuthController::class, 'register']);
Route::post('login', [AuthController::class, 'login']);
Route::middleware('auth:sanctum')->group(function () {
    Route::get('user', [AuthController::class, 'getUser']);
    Route::put('user', [AuthController::class, 'updateUser']);
    Route::delete('user', [AuthController::class, 'deleteUser']);
});
```

### 5. Create AuthController

Implement user registration, login, and management functions.

### 6. Test API

Use Postman to test endpoints.

## Flutter App Setup

### 1. Create Flutter Project

```bash
flutter create flutter_app
cd flutter_app
```

### 2. Add Dependencies

In `pubspec.yaml`, add:

```yaml
dependencies:
  http: ^0.13.3
  shared_preferences: ^2.0.6
```

Run:

```bash
flutter pub get
```

### 3. Create API Service

In `lib/api_service.dart`, implement methods for login, registration, user retrieval, updating, and deletion.

### 4. Create UI

- `lib/login_page.dart`: Login screen.
- `lib/register_page.dart`: Registration screen.
- `lib/profile_page.dart`: User profile management.

### 5. Run Applications

1. Start Laravel server:

   ```bash
   php artisan serve
   ```

2. Run Flutter app:

   ```bash
   flutter run
   ```

## Conclusion

You now have a Flutter app connected to a Laravel API for user authentication and profile management.
