# 🏥 Medical Vending Machine System

A comprehensive IoT-based medical vending machine management system built with .NET 8, featuring real-time monitoring, secure authentication, and automated inventory management.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Security Features](#security-features)
- [IoT Integration](#iot-integration)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

The Medical Vending Machine System is a graduation project that demonstrates a complete IoT solution for managing medical vending machines. The system provides secure access to medical supplies, real-time inventory tracking, and automated dispensing capabilities through a modern web API.

### Key Capabilities:
- **Secure Authentication**: JWT-based authentication with role-based access control
- **Real-time Monitoring**: IoT integration for live machine status and inventory tracking
- **Inventory Management**: Automated stock management with low-stock alerts
- **User Management**: Separate interfaces for customers and administrators
- **Payment Integration**: Secure payment processing for medical supplies
- **Email Notifications**: Automated email verification and password reset functionality

## ✨ Features

### 🔐 Authentication & Security
- JWT token-based authentication
- Role-based access control (Admin/Customer)
- Password hashing with BCrypt
- Email verification system
- Password reset functionality
- Google OAuth integration

### 🏪 Vending Machine Management
- Real-time machine status monitoring
- Inventory tracking and alerts
- Automated dispensing control
- Machine location management
- Maintenance scheduling

### 💊 Medical Inventory
- Medicine categorization and management
- Stock level monitoring
- Expiry date tracking
- Price management
- Favorites system for customers

### 👥 User Management
- Customer registration and profiles
- Admin dashboard and controls
- Purchase history tracking
- User preferences and settings

### 📧 Communication
- Email verification for new accounts
- Password reset via email
- Low stock notifications
- System alerts and updates

## 🏗️ Architecture

The project follows **Clean Architecture** principles with a layered structure:

```
MedicalVending/
├── MedicalVending.API/          # Presentation Layer
├── MedicalVending.Application/   # Application Layer
├── MedicalVending.Domain/        # Domain Layer
└── MedicalVending.Infrastructure/# Infrastructure Layer
```

### Architecture Layers:

1. **Domain Layer**: Contains business entities, interfaces, and domain logic
2. **Application Layer**: Contains business use cases and application services
3. **Infrastructure Layer**: Contains data access, external services, and implementations
4. **API Layer**: Contains controllers, middleware, and API endpoints

## 🛠️ Technology Stack

### Backend
- **.NET 8** - Modern, high-performance framework
- **Entity Framework Core** - ORM for database operations
- **SQL Server** - Primary database
- **AutoMapper** - Object mapping
- **BCrypt.Net-Next** - Password hashing
- **JWT Bearer** - Authentication tokens

### Cloud Services
- **Azure IoT Hub** - IoT device management
- **Azure Storage** - File and blob storage
- **Azure SQL Database** - Cloud database hosting

### External Integrations
- **Gmail SMTP** - Email services
- **Google OAuth** - Social authentication
- **Swagger/OpenAPI** - API documentation

## 📋 Prerequisites

Before running this project, ensure you have:

- **.NET 8 SDK** installed
- **SQL Server** (Local or Azure)
- **Visual Studio 2022** or **VS Code**
- **Azure Account** (for cloud services)
- **Gmail Account** (for SMTP)

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone <your-repository-url>
cd Medical-vending-machine-system
```

### 2. Navigate to Backend
```bash
cd backend
```

### 3. Restore Dependencies
```bash
dotnet restore
```

### 4. Update Database
```bash
dotnet ef database update --project MedicalVending.Infrastructure --startup-project MedicalVending.API
```

### 5. Run the Application
```bash
dotnet run --project MedicalVending.API
```

## ⚙️ Configuration

### 1. Database Connection
Update `appsettings.json` with your database connection string:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=YOUR_SERVER;Database=YOUR_DATABASE;User ID=YOUR_USERNAME;Password=YOUR_PASSWORD;"
}
```

### 2. JWT Configuration
Set your JWT secret key and issuer details:

```json
"Jwt": {
  "Key": "YOUR_SUPER_SECURE_SECRET_KEY_WITH_AT_LEAST_32_BYTES_LENGTH_HERE_12345",
  "Issuer": "YOUR_ISSUER",
  "Audience": "YOUR_AUDIENCE"
}
```

### 3. Email Configuration
Configure SMTP settings for email functionality:

```json
"Smtp": {
  "Host": "smtp.gmail.com",
  "Port": 587,
  "Email": "YOUR_EMAIL@gmail.com",
  "Password": "YOUR_APP_PASSWORD"
}
```

### 4. Azure Services
Configure Azure IoT Hub and Storage:

```json
"AzureIoTHub": {
  "ConnectionString": "HostName=YOUR_IOT_HUB_HOSTNAME;SharedAccessKeyName=YOUR_SHARED_ACCESS_KEY_NAME;SharedAccessKey=YOUR_SHARED_ACCESS_KEY"
},
"AzureStorage": {
  "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=YOUR_STORAGE_ACCOUNT;AccountKey=YOUR_STORAGE_ACCOUNT_KEY;EndpointSuffix=core.windows.net"
}
```

## 📚 API Documentation

Once the application is running, access the Swagger documentation at:
```
https://localhost:7001/swagger
```

### Key API Endpoints:

#### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/refresh` - Refresh JWT token
- `POST /api/auth/logout` - User logout

#### Vending Machines
- `GET /api/vendingmachines` - Get all machines
- `GET /api/vendingmachines/{id}` - Get specific machine
- `POST /api/vendingmachines` - Create new machine
- `PUT /api/vendingmachines/{id}` - Update machine

#### Medicines
- `GET /api/medicines` - Get all medicines
- `GET /api/medicines/{id}` - Get specific medicine
- `POST /api/medicines` - Add new medicine
- `PUT /api/medicines/{id}` - Update medicine

#### Purchases
- `GET /api/purchases` - Get purchase history
- `POST /api/purchases` - Create new purchase
- `GET /api/purchases/{id}` - Get specific purchase

## 🗄️ Database Schema

The system uses the following main entities:

### Core Entities
- **Customers** - User accounts and profiles
- **Admins** - Administrative users
- **VendingMachines** - IoT-enabled vending machines
- **Medicines** - Medical products and inventory
- **Categories** - Medicine categorization
- **Purchases** - Transaction records
- **MachineMedicines** - Inventory mapping

### Supporting Entities
- **RefreshTokens** - JWT refresh token management
- **EmailVerificationCodes** - Email verification system
- **FavoritesMedicine** - User favorites

## 🔒 Security Features

### Authentication & Authorization
- **JWT Tokens**: Secure token-based authentication
- **Role-Based Access**: Admin and Customer roles
- **Password Security**: BCrypt hashing with salt
- **Token Refresh**: Automatic token renewal
- **Session Management**: Secure logout and token invalidation

### Data Protection
- **Input Validation**: Comprehensive request validation
- **SQL Injection Prevention**: Parameterized queries
- **XSS Protection**: Input sanitization
- **HTTPS Enforcement**: Secure communication

### IoT Security
- **Azure IoT Hub**: Secure device communication
- **Shared Access Keys**: Secure device authentication
- **Device Twins**: Secure device state management

## 🌐 IoT Integration

### Azure IoT Hub Features
- **Device Registration**: Secure device onboarding
- **Real-time Monitoring**: Live machine status updates
- **Remote Control**: Automated dispensing control
- **Data Analytics**: Usage patterns and insights

### Machine Communication
- **Device Twins**: Synchronized device state
- **Direct Methods**: Remote machine control
- **Telemetry**: Real-time data streaming
- **Alerts**: Automated notifications

## 🤝 Contributing

This is a graduation project. For academic purposes, contributions are welcome:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is created for educational purposes as a graduation project. All rights reserved.

---

## 👨‍🎓 About the Developer

**Student Name**: [Your Name]  
**University**: [Your University]  
**Department**: [Your Department]  
**Graduation Year**: 2024

### Contact Information
- **Email**: [your.email@university.edu]
- **LinkedIn**: [Your LinkedIn Profile]
- **GitHub**: [Your GitHub Profile]

---

**Note**: This project demonstrates advanced software engineering concepts including Clean Architecture, IoT integration, cloud services, and modern web development practices. It serves as a comprehensive example of building scalable, secure, and maintainable software systems. 