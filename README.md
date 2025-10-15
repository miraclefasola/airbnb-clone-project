# Airbnb Clone Project

## 🚀 Objective

The backend for the Airbnb Clone project is designed to provide a robust and scalable foundation for managing user interactions, property listings, bookings, and payments. This backend will support various functionalities required to mimic the core features of Airbnb, ensuring a smooth experience for users and hosts.

## 🏆 Project Goals

- **User Management**: Implement a secure system for user registration, authentication, and profile management
- **Property Management**: Develop features for property listing creation, updates, and retrieval
- **Booking System**: Create a booking mechanism for users to reserve properties and manage booking details
- **Payment Processing**: Integrate a payment system to handle transactions and record payment details
- **Review System**: Allow users to leave reviews and ratings for properties
- **Data Optimization**: Ensure efficient data retrieval and storage through database optimizations

## 🛠️ Features Overview

### 1. API Documentation
- **OpenAPI Standard**: The backend APIs are documented using the OpenAPI standard to ensure clarity and ease of integration
- **Django REST Framework**: Provides a comprehensive RESTful API for handling CRUD operations on user and property data
- **GraphQL**: Offers a flexible and efficient query mechanism for interacting with the backend

### 2. User Authentication
- **Endpoints**: `/users/`, `/users/{user_id}/`
- **Features**: Register new users, authenticate, and manage user profiles

### 3. Property Management
- **Endpoints**: `/properties/`, `/properties/{property_id}/`
- **Features**: Create, update, retrieve, and delete property listings

### 4. Booking System
- **Endpoints**: `/bookings/`, `/bookings/{booking_id}/`
- **Features**: Make, update, and manage bookings, including check-in and check-out details

### 5. Payment Processing
- **Endpoints**: `/payments/`
- **Features**: Handle payment transactions related to bookings

### 6. Review System
- **Endpoints**: `/reviews/`, `/reviews/{review_id}/`
- **Features**: Post and manage reviews for properties

### 7. Database Optimizations
- **Indexing**: Implement indexes for fast retrieval of frequently accessed data
- **Caching**: Use caching strategies to reduce database load and improve performance

## ⚙️ Technology Stack

- **Django**: A high-level Python web framework used for building the RESTful API
- **Django REST Framework**: Provides tools for creating and managing RESTful APIs
- **PostgreSQL**: A powerful relational database used for data storage
- **GraphQL**: Allows for flexible and efficient querying of data
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments
- **Redis**: Used for caching and session management
- **Docker**: Containerization tool for consistent development and deployment environments
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes

## 👥 Team Roles

- **Backend Developer**: Responsible for implementing API endpoints, database schemas, and business logic
- **Database Administrator**: Manages database design, indexing, and optimizations
- **DevOps Engineer**: Handles deployment, monitoring, and scaling of the backend services
- **QA Engineer**: Ensures the backend functionalities are thoroughly tested and meet quality standards

## 📈 API Documentation Overview

- **REST API**: Detailed documentation available through the OpenAPI standard, including endpoints for users, properties, bookings, and payments
- **GraphQL API**: Provides a flexible query language for retrieving and manipulating data

## 🗄️ Database Design

### Key Entities

#### 1. Users
Manages user accounts for both guests and hosts.

**Key Fields:**
- `id` (Primary Key): Unique identifier for each user
- `email` (Unique): User's email address for authentication
- `first_name`: User's first name
- `last_name`: User's last name
- `phone_number`: Contact phone number
- `is_host`: Boolean flag indicating if user can list properties
- `date_joined`: Account creation timestamp
- `profile_picture`: URL to user's profile image

#### 2. Properties
Stores property listing information.

**Key Fields:**
- `id` (Primary Key): Unique identifier for each property
- `host_id` (Foreign Key): References Users table - property owner
- `title`: Property listing title
- `description`: Detailed property description
- `price`:  rate in decimal format
- `location`: Property address/location
- `max_guests`: Maximum number of guests allowed
- `amenities`: available amenities
- `is_available`: Boolean indicating current availability

#### 3. Bookings
Tracks reservation details between guests and properties.

**Key Fields:**
- `id` (Primary Key): Unique identifier for each booking
- `guest_id` (Foreign Key): References Users table - booking guest
- `property_id` (Foreign Key): References Properties table
- `check_in_date`: Reservation start date
- `check_out_date`: Reservation end date
- `total_price`: Final booking amount
- `status`: Booking status (pending, confirmed, cancelled, completed)
- `created_at`: Booking creation timestamp

#### 4. Reviews
Stores guest reviews and ratings for properties.

**Key Fields:**
- `id` (Primary Key): Unique identifier for each review
- `guest_id` (Foreign Key): References Users table - reviewer
- `property_id` (Foreign Key): References Properties table
- `booking_id` (Foreign Key): References Bookings table - ensures guest stayed
- `rating`: Numeric rating (1-5 stars)
- `comment`: Written review text
- `created_at`: Review submission timestamp

#### 5. Payments
Records payment transactions for bookings.

**Key Fields:**
- `id` (Primary Key): Unique identifier for each payment
- `booking_id` (Foreign Key): References Bookings table
- `amount`: Payment amount
- `payment_method`: Payment type (credit_card, transfer, etc.)
- `payment_status`: Status (pending, completed, failed, refunded)
- `transaction_id`: External payment processor reference
- `created_at`: Payment processing timestamp

### Entity Relationships

#### One-to-Many Relationships
- **Users → Properties**: A user (host) can own multiple properties
- **Users → Bookings**: A user (guest) can make multiple bookings
- **Properties → Bookings**: A property can have multiple bookings over time
- **Properties → Reviews**: A property can receive multiple reviews
- **Users → Reviews**: A user can write multiple reviews
- **Bookings → Payments**: A booking can have multiple payment records (partial payments, refunds)

#### One-to-One Relationships
- **Bookings → Reviews**: Each booking can have at most one review (guests can only review properties they've stayed at)


### Key Constraints
- Users must have unique email addresses
- Bookings cannot have check-out dates before check-in dates
- Reviews can only be created by guests who have completed bookings
- Payments are linked to valid bookings
- Properties can only be created by users with `is_host = True`

## 🔧 Feature Breakdown

### User Management
Provides comprehensive user account functionality including registration, authentication, and profile management for both guests and hosts. This feature serves as the foundation for the platform by enabling secure user identification and personalized experiences. Users can update their profiles, manage preferences, and maintain their account security through password management and profile verification.

### Property Management
Enables hosts to create, update, and manage their property listings with detailed information including descriptions, pricing, amenities, and availability calendars. This feature forms the core marketplace functionality by allowing hosts to showcase their properties effectively with photos, location details, and house rules.

### Booking System
Facilitates the complete reservation process between guests and hosts with real-time availability checking, booking confirmation, and status management. This feature handles the critical transaction flow from property search to booking completion, including date validation, pricing calculations, and conflict prevention. 

### Payment Processing
Integrates secure payment gateway functionality to handle financial transactions, including booking payments, security deposits, and host payouts. This feature ensures reliable payment processing with support for multiple payment methods, automatic calculations, and secure fund distribution. The system includes comprehensive payment tracking, refund processing, transaction history, and automated invoicing for complete financial transparency.

## 🔒 API Security

### JWT/SSO Authentication
Implements JSON Web Token (JWT) authentication with Single Sign-On (SSO) capabilities to ensure secure, stateless user sessions across the platform. This protects user accounts from unauthorized access and ensures that only authenticated users can perform sensitive operations like making bookings, processing payments, or managing property listings.

### Rate Limiting & Bot Protection
Deploys intelligent rate limiting mechanisms to prevent abuse from bots, scrapers, and malicious actors attempting to overwhelm the system or extract data illegally. This security measure protects against automated attacks, prevents API abuse, and ensures fair resource allocation among legitimate users. Rate limiting is particularly crucial for protecting booking endpoints from rapid-fire reservation attempts, search APIs from excessive scraping, and payment processing from fraudulent transaction floods.

### Virtual Firewall & DDoS Protection
Utilizes virtual firewall rules and distributed denial-of-service (DDoS) protection to safeguard the infrastructure from network-level attacks and traffic anomalies. This creates multiple layers of defense against malicious traffic patterns, IP-based attacks, and ensures service availability during peak usage or coordinated attack scenarios. The firewall prevents unauthorized network access while DDoS protection maintains platform stability and responsiveness for legitimate users during high-traffic periods.

### Principle of Least Privilege
Enforces strict role-based access control (RBAC) where users, API endpoints, and system components receive only the minimum permissions necessary for their specific functions. This security principle ensures that guests cannot access host-only management features, hosts cannot manipulate other users' properties or bookings, and system services operate with restricted database and resource permissions. This approach significantly minimizes the potential impact of security breaches, prevents privilege escalation attacks, and maintains clear separation of concerns across different user roles and system components.



## 📌 API Endpoints

### Users
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/users/` | List all users |
| POST | `/users/` | Create a new user |
| GET | `/users/{user_id}/` | Retrieve a specific user |
| PUT | `/users/{user_id}/` | Update a specific user |
| DELETE | `/users/{user_id}/` | Delete a specific user |

### Properties
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/properties/` | List all properties |
| POST | `/properties/` | Create a new property |
| GET | `/properties/{property_id}/` | Retrieve a specific property |
| PUT | `/properties/{property_id}/` | Update a specific property |
| DELETE | `/properties/{property_id}/` | Delete a specific property |

### Bookings
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/bookings/` | List all bookings |
| POST | `/bookings/` | Create a new booking |
| GET | `/bookings/{booking_id}/` | Retrieve a specific booking |
| PUT | `/bookings/{booking_id}/` | Update a specific booking |
| DELETE | `/bookings/{booking_id}/` | Delete a specific booking |

### Payments
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/payments/` | Process a payment |

### Reviews
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/reviews/` | List all reviews |
| POST | `/reviews/` | Create a new review |
| GET | `/reviews/{review_id}/` | Retrieve a specific review |
| PUT | `/reviews/{review_id}/` | Update a specific review |
| DELETE | `/reviews/{review_id}/` | Delete a specific review |

## 🚀 Getting Started

1. Clone the repository
2. Set up your virtual environment
3. Install dependencies: `pip install -r requirements.txt`
4. Configure your database settings
5. Run migrations: `python manage.py migrate`
6. Start the development server: `python manage.py runserver`
