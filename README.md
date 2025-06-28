# Airbnb Clone Backend - Features & Functionalities

This document outlines the core features and system architecture for the backend of the Airbnb Clone.

---

##  User Management
- Sign up as guest or host
- Email/password login with JWT
- OAuth login (Google, Facebook)
- Profile photo and info updates

##  Property Listings
- Hosts can add, edit, delete listings
- Includes title, description, location, price, amenities, availability

##  Search & Filtering
- Filter listings by location, price, number of guests, and amenities
- Pagination for large results

##  Booking Management
- Guests can book listings
- Prevent double bookings
- Cancel bookings
- Track booking status (pending, confirmed, canceled)

##  Payment Integration
- Stripe/PayPal integration
- Guest upfront payment
- Host payouts
- Multiple currencies supported

##  Reviews & Ratings
- Guests review listings
- Hosts respond
- Reviews are tied to bookings

##  Notifications
- Email and in-app updates for:
  - Bookings
  - Cancellations
  - Payments

##  Admin Dashboard
- Manage users, listings, bookings, and payments

---

##  Technical Requirements

###  Database
- PostgreSQL / MySQL
- Tables: Users, Properties, Bookings, Reviews, Payments

###  API
- RESTful APIs with GET, POST, PUT, DELETE
- (Optional) GraphQL for advanced querying

###  Authentication & Authorization
- JWT tokens for session management
- Role-Based Access Control (RBAC)

###  File Storage
- Cloudinary for profile and listing images

###  Email Service
- SendGrid or Mailgun for transactional emails

###  Error Handling & Logging
- Global API error handling
- Structured logging

---

##  Non-Functional Requirements
- Scalable architecture with modular services
- Secure encryption and validation
- Redis caching for optimization
- Unit & integration tests using `pytest`
