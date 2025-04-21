Our team 7 integrated its call center services and Vehicle Rentals microservice with team16's visa services and team18's cab services. For detailed api docs find it in these repos

https://github.com/Roshr2211/call_support_agent.git --> Call centre support microservice
https://github.com/sukiperumal/bookmytrip.git --> Vehicle rentals microservice


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
