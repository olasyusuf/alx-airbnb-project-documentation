<div align="center">
  <br>
  <h1><b>Backend Feature Requirement Specifications</b></h1>
</div>

<br />

---
## Table of Contents

- [Table of Contents](#table-of-contents)
    - [Objectives](#objectives)
    - [User Authentication](#user-authentication)
    - [API Endpoints](#api-endpoints)
    - [Input/Output](#inputoutput)
    - [Validation Rules](#validation-rules)
    - [Performance Criteria](#performance-criteria)
    - [Property Management](#property-management)
    - [API Endpoints](#api-endpoints-1)
    - [Input / Output](#input--output)
    - [Validation Rules](#validation-rules-1)
    - [Performance Criteria](#performance-criteria-1)
    - [Booking System](#booking-system)
    - [API Endpoints](#api-endpoints-2)
    - [Input / Output](#input--output-1)
    - [Validation Rules](#validation-rules-2)
    - [Performance Criteria](#performance-criteria-2)
    - [Security \& Compliance (Applies to All Features)](#security--compliance-applies-to-all-features)


<br />


#### Objectives

This document details the functional and technical requirements for three core Airbnb Clone backend features: 
- **User Authentication**
- **Property Management** 
- **Booking System**.

---

#### User Authentication

#### API Endpoints
- `POST /api/register` – Register a new user
- `POST /api/login` – Authenticate a user
- `GET /api/profile` – Retrieve current user profile
- `PUT /api/profile` – Update user profile

#### Input/Output
**Registration Input:**
- name: string
- email: string (unique)
- password: string (min 8 characters, must contain at least 1 digit, 1 special character, 1 digit, mixed-case)
- role: string (guest or host)

**Login Input:**
- email: string
- password: string
- or OAuth  

**Output:**
- Success: User info + JWT token
- Failure: Error message (e.g., invalid login details)

#### Validation Rules
- Role must be either `guest` or `host`.
- All required fields must be supplied.
- A valid, unique email is required.
- Password requires minimum length and complexity.

#### Performance Criteria
- JWT expires in 24 hours.
- Limit login attempts to 5 per minute per IP.

---

#### Property Management

#### API Endpoints
- `POST /api/properties` – Create a new listing (Host only)
- `GET /api/properties` – List all properties
- `GET /api/properties/:id` – Retrieve single property
- `PUT /api/properties/:id` – Update listing (Host only)
- `DELETE /api/properties/:id` – Delete listing (Host only)

#### Input / Output
**Create/Edit Input:**
- title: string
- description: string
- location: string
- price: decimal

**Output:**
- Success: Confirmation + property ID
- Failure: Invalid or unauthorized access.
  
#### Validation Rules
- Authentication and host authorization are required for the user.
- Mandatory fields: title, location, availability.
- Price must be a positive decimal number.
- Prevent duplicate listings (based on host, title, and location).

#### Performance Criteria
- Image uploads for listings are limited to 5 per listing, with a 2MB maximum per image.
- Support for pagination for queries returning over 50 records.

---

#### Booking System

#### API Endpoints
- `POST /api/bookings` – Create a booking
- `GET /api/bookings` – List user’s bookings
- `DELETE /api/bookings/:id` – Cancel booking
- `GET /api/bookings/:id` – View booking details

#### Input / Output
**Booking Input:**
- property_id: string uuid
- start_date: date
- end_date: date

**Output:**
- Success: Booking confirmation details including ID and status.
- Failure: Date unavailable / policy violation

#### Validation Rules
- Users cannot book their own properties.
- End date cannot be earlier than Start date for any booking.
- Dates must adhere to ISO 8601 format (YYYY-MM-DD)

#### Performance Criteria
- Booking confirmation in under 10 mins.
- Implement database-level constraints for double-booking prevention.
  

---

#### Security & Compliance (Applies to All Features)
- JWT + OAuth and role-based access govern data access.
- Protect sensitive fields (passwords, tokens) from exposure
- Secure HTTPS communication is mandatory for all endpoints.
- All Errors are standardized to JSON format and error codes.

---
