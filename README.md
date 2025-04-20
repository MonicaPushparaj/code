**Motor Insurance Management System**

A comprehensive Java-based web application for managing motor insurance policies with secure user authentication and policy management features.

**Table of Contents**
Overview
Features
Prerequisites
Technology Stack
Installation & Setup
Configuration
Security
API Endpoints
Database Schema

**Overview**
This Motor Insurance Management System provides a platform for users to register, manage their motor insurance policies, and handle policy renewals. The system includes OTP-based authentication for enhanced security and a comprehensive dashboard for policy management.

**Features**
User Authentication (Login/Register) with OTP verification
Email-based OTP verification
JWT-based secure authentication
Motor Insurance Policy Management
Policy Renewal Processing
Admin Dashboard
User Dashboard
PostgreSQL Database Integration
Prerequisites
Java JDK 17 or higher
PostgreSQL 12 or higher
Maven 3.6 or higher
SMTP server access for email notifications
Git (for version control)

**Technology Stack**
Spring Boot 3.2.3
Spring Security
Spring Data JPA
PostgreSQL
Thymeleaf
JWT (JSON Web Tokens)
Lombok
Maven

**Installation & Setup**
Clone the Repository

git clone [repository-url]
cd motor-insurance
Database Setup

CREATE DATABASE motor_insurance;
Build the Project

mvn clean install
Run the Application

mvn spring-boot:run
Configuration
1. Database Configuration
Update src/main/resources/application.properties:

spring.datasource.url=jdbc:postgresql://localhost:5432/motor_insurance
spring.datasource.username=your_username
spring.datasource.password=your_password

2. Email Configuration
Update SMTP settings in application.properties:

spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=your_email@gmail.com
spring.mail.password=your_app_specific_password
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true

3. JWT Configuration
Update JWT settings in application.properties:

jwt.secret=your_jwt_secret_key
jwt.expiration=86400000
Security
The application implements several security measures:

JWT Authentication

Token-based authentication for API endpoints
Configurable token expiration
OTP Verification

Email-based OTP for user registration
OTP expiration time: 5 minutes
Password Security

BCrypt password encryption
Configurable password policies
API Endpoints
Authentication
POST /api/auth/register - User registration
POST /api/auth/verify-otp - OTP verification
POST /api/auth/login - User login
Policy Management
GET /api/policies - List user's policies
POST /api/policies - Create new policy
PUT /api/policies/{id} - Update policy
GET /api/policies/{id} - Get policy details
POST /api/policies/{id}/renew - Renew policy
Database Schema
Users Table
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    phone_number VARCHAR(20),
    enabled BOOLEAN DEFAULT FALSE,
    otp VARCHAR(6),
    otp_expiry_time TIMESTAMP
);
Motor Policies Table
CREATE TABLE motor_policies (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT REFERENCES users(id),
    vehicle_number VARCHAR(20) NOT NULL,
    vehicle_model VARCHAR(100) NOT NULL,
    vehicle_type VARCHAR(50) NOT NULL,
    manufacturing_year INTEGER NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    premium_amount DECIMAL(10,2) NOT NULL,
    policy_number VARCHAR(50) UNIQUE NOT NULL,
    status VARCHAR(20) NOT NULL
);
Deployment Checklist
When deploying to a new system, ensure the following:

Environment Setup

Install JDK 17 or higher
Install PostgreSQL
Configure JAVA_HOME environment variable
Set up required system environment variables
Database Configuration

Create new PostgreSQL database
Update database credentials in application.properties
Run database migrations/schema setup
Email Configuration

Configure SMTP server details
Update email credentials
Test email functionality
Security Configuration

Generate new JWT secret key
Update JWT configuration
Configure SSL/TLS if required
Update CORS settings if required
Application Properties

Update server port if required
Configure logging settings
Set appropriate profile (dev/prod)
Production Considerations

Configure proper logging
Set up monitoring
Configure backup strategy
Set up SSL certificate
Configure firewall rules
Support and Contact
For any queries or support, please contact: Monica
