Our team 7 integrated its call center services and Vehicle Rentals microservice with team16's visa services and team18's cab services. For detailed api docs find it in these repos

https://github.com/Roshr2211/call_support_agent.git --> Call centre support microservice
https://github.com/sukiperumal/bookmytrip.git --> Vehicle rentals microservice

---

# Vehicle Rentals Management Microservice — BookMyTrip

This microservice powers vehicle rentals for the BookMyTrip platform, handling everything from vehicle listings and bookings to partner integrations and location-based availability. It also acts as a bridge between internal services and external cab APIs.

---

## Features

- Browse and filter rental vehicles by type, location, pricing, and availability
- Manage bookings and vehicle reviews
- Support for multiple pickup/drop-off locations
- Dynamic pricing estimates
- Integration with external cab partners for fare and partner data
- Webhook support for real-time updates from external systems

---

## Architecture Overview

Built with **Node.js + Express**, this microservice uses **MongoDB** for data persistence and **Axios** to communicate with external APIs. It uses a **proxy pattern** to abstract external service calls and expose them through internal endpoints, while also supporting event-driven updates via webhooks.

---

## API Endpoints

### Vehicle Management

- **GET `/api/vehicles`**: List vehicles with optional filters (type, location, price, seats, etc.)
- **GET `/api/vehicles/:id`**: Get details of a specific vehicle
- **GET `/api/vehicles/types`**: List all available vehicle types
- **GET `/api/vehicles/availability`**: Find available vehicles in a date/location range
- **GET `/api/vehicles/:id/pricing`**: Estimate pricing based on usage duration
- **POST `/api/vehicles/:id/reviews`**: Add a review for a vehicle (auth required)
- **GET `/api/vehicles/:id/reviews`**: View all reviews for a vehicle

---

### Booking Management

- **POST `/api/bookings`**: Create a new booking with required details
- **GET `/api/bookings/:id`**: View booking information
- **PUT `/api/bookings/:id`**: Update booking (e.g., dates, locations)
- **DELETE `/api/bookings/:id`**: Cancel a booking (status set to `cancelled`)

---

### Location Management

- **GET `/api/locations`**: List pickup/drop-off locations with filters
- **GET `/api/locations/:id`**: View specific location details
- **GET `/api/locations/:id/availability`**: Check vehicle availability at a location for a date range

---

## 🔌 Cab Partner Integration

The service integrates with external cab partner APIs via a **proxy pattern**. Using Axios and environment-configured URLs, it exposes internal endpoints that forward requests for operations like listing, creating, updating, or deleting cab partners.

All cab-related logic is centralized in `cabController.js`, and external calls are gracefully handled with request validation, fallback to mock data, and detailed error forwarding when APIs are unavailable or fail.

---

## Error Handling & Fallbacks

- Input validation before external requests
- External API errors are transparently forwarded
- Mock data is returned if the external service is unavailable or in development mode

---

# Bookings API Documentation

This module handles the entire lifecycle of a booking, including creation, retrieval, modification, and integration with external visa services. It supports multiple booking types (e.g., flights, hotels), but visa features apply only to flight bookings.

---

## Overview

The **Bookings API** is designed to manage customer reservations and enhance travel workflows by integrating with an external **Visa Application System**. This enables seamless visa checking and application processes directly from the booking platform.

---

## Core Capabilities

- **Create and manage bookings** for various travel services.
- **Retrieve bookings** by ID or reference number.
- **Track and update booking status** throughout the journey.
- **Handle modification requests** for changes to existing bookings.
- **Integrate with an external visa system** for customers who require travel visas, triggered automatically for flight bookings.

---

##  Visa Integration Highlights

When a flight booking is created, the system can:

1. **Automatically check visa requirements** for the destination.
2. **Initiate a visa application** for the customer, using booking details.
3. **Retrieve all visa applications** submitted for a given booking.

This integration connects to an external visa service to provide up-to-date visa status and approval details, enhancing customer experience and reducing manual overhead.

---

## External Services

The system communicates with:

- A **Visa Application Endpoint** (`/apply`) to submit visa applications.
- A **Visa Status Endpoint** (`/my-applications/:userId`) to fetch application history.

These services are expected to be running externally and accessible via standard REST calls through docker.

---


## Use Case Example

A user books an international flight. The system:

1. Creates the booking.
2. Detects that the service type is "flight."
3. Sends a request to the visa system with the customer's details.
4. Retrieves the visa status and attaches it to the booking record.
5. Allows the user to view all past visa applications linked to their account.

---

##  Outcome

The integration ensures that visa-related logistics are handled behind the scenes, giving both customers and admins a smooth and efficient experience.
