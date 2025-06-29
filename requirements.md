# Technical & Functional Requirements – Airbnb Clone Backend

This document outlines the **technical** and **functional** specifications for three core backend features in the Airbnb Clone project:

- User Authentication  
- Property Management  
- Booking System  

---

## 1. User Authentication

### Functional Requirements
- Users should be able to register, log in, and log out.
- Passwords must be securely hashed before storage.
- JWT tokens will be issued for session authentication.

### API Endpoints
- `POST /api/auth/register` – Register a new user  
- `POST /api/auth/login` – Authenticate a user  
- `POST /api/auth/logout` – Log out an authenticated user

### Input / Output Specifications

**Register Endpoint**

**Request:**
- `name`: string (required)  
- `email`: string (required, must be unique and in valid format)  
- `password`: string (required, minimum 8 characters, must include upper/lowercase and numbers)  

**Response (Success):**
- `message`: Registration successful  
- `token`: JWT token for session  

---

**Login Endpoint**

**Request:**
- `email`: string (required)  
- `password`: string (required)

**Response (Success):**
- `message`: Login successful  
- `token`: JWT token for session  

---

### Validation Rules
- Email must be unique and follow proper email format.
- Passwords must meet minimum security standards.

### Performance Criteria
- All responses should be returned in under 500ms.
- Implement rate-limiting for login attempts (e.g., 5 requests per minute).

---

## 2. Property Management

### Functional Requirements
- Hosts can create, view, update, and delete property listings.
- Each listing must contain a title, description, location, price per night, and availability status.

### API Endpoints
- `POST /api/properties` – Create a new property listing  
- `GET /api/properties/:id` – View details of a specific property  
- `PUT /api/properties/:id` – Update an existing property  
- `DELETE /api/properties/:id` – Delete a property  
- `GET /api/properties` – Retrieve all available properties (with pagination)

### Input / Output Specifications

**Create Property Endpoint**

**Request:**
- `title`: string (required)  
- `description`: string (optional)  
- `location`: string (required)  
- `price_per_night`: number (required, must be positive)  
- `availability`: boolean (required)

**Response (Success):**
- `message`: Property created successfully  
- `property_id`: Unique ID of the newly created property

---

### Validation Rules
- `title`, `location`, and `price_per_night` are mandatory.
- `price_per_night` must be a positive number.
- Ensure no duplicate property entries (e.g., same host, title, and location).

### Performance Criteria
- All property-related operations should return in under 700ms.
- Pagination must be implemented for listing endpoints.

---

## 3. Booking System

### Functional Requirements
- Guests can book properties for specific date ranges.
- System must prevent double bookings.
- Bookings must be linked to both user and property records.

### API Endpoints
- `POST /api/bookings` – Create a new booking  
- `GET /api/bookings/:id` – View a specific booking  
- `GET /api/bookings/user/:userId` – Retrieve all bookings for a user

### Input / Output Specifications

**Create Booking Endpoint**

**Request:**
- `property_id`: string (required)  
- `check_in`: date (required)  
- `check_out`: date (required)

**Response (Success):**
- `message`: Booking confirmed  
- `booking_id`: Unique ID for the booking  

---

### Validation Rules
- `check_out` date must be after `check_in`.
- The selected property must be available for the given dates.
- Prevent double bookings using atomic database transactions.

### Performance Criteria
- Booking creation should complete in under 800ms.
- Handle concurrent booking requests without race conditions.

---

## Common Rules for All Endpoints

### Authentication
- All protected endpoints require the `Authorization: Bearer <JWT>` header.

### Error Response Format
- All errors should return a standardized structure:
  - `error`: A descriptive error message

**Example:**
- `error`: Invalid email or password

---

