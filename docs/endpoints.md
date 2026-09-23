# RaceDay API Endpoint Plan

This document outlines the API specifications and requirements mapping for the RaceDay backend system.

Requirements Mapping

Endpoint Specifications

1. Authentication
Handles user account creation and session tokens for Organisers and Participants.

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new user account | Public | `{ "firstName": "Nathan", "lastName": "Jayanath", "email": "nathan@example.com", "password": "Password123!", "role": "Participant" }` | `201 Created` - `{ "message": "User registered", "userId": 1 }` |
| `POST` | `/api/auth/login` | Authenticate user credentials | Public | `{ "email": "nathan@example.com", "password": "Password123!" }` | `200 OK` - `{ "token": "eyJhbGci...", "role": "Participant" }` |

2. User Profiles
Allows users to view and update their personal profile information.

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `GET` | `/api/users/profile` | Retrieve profile details | Organiser, Participant | None | `200 OK` - `{ "userId": 1, "firstName": "Nathan", "lastName": "Jayanath", "email": "nathan@example.com", "role": "Participant" }` |
| `PUT` | `/api/users/profile` | Update account details | Organiser, Participant | `{ "firstName": "Nathan", "lastName": "Jayanath" }` | `200 OK` - `{ "message": "Profile updated" }` |

3. Events
Allows Organisers to manage race events and allows participants to view available events.

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `GET` | `/api/events` | List all upcoming events | Public | None | `200 OK` - `[ { "eventId": 1, "eventName": "Soweto Half Marathon", "eventDate": "2026-11-01", "location": "Soweto", "eventType": "Run" } ]` |
| `GET` | `/api/events/{id}` | Get event details by ID | Public | None | `200 OK` - `{ "eventId": 1, "eventName": "Soweto Half Marathon", "description": "Annual road race", "location": "Soweto" }` |
| `POST` | `/api/events` | Create a new race event | Organiser | `{ "eventName": "Pretoria Capital Classic", "eventDate": "2026-12-05", "location": "Pretoria", "description": "City circuit", "eventType": "Cycle" }` | `201 Created` - `{ "eventId": 2, "message": "Event created" }` |
| `PUT` | `/api/events/{id}` | Update existing event | Organiser | `{ "eventName": "Pretoria Capital Classic 2026", "location": "Pretoria Central" }` | `200 OK` - `{ "message": "Event updated" }` |
| `DELETE` | `/api/events/{id}` | Remove a race event | Organiser | None | `200 OK` - `{ "message": "Event deleted" }` |

4. Categories
Defines race distances and entry criteria for individual events.

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `GET` | `/api/events/{eventId}/categories` | Fetch categories for an event | Public | None | `200 OK` - `[ { "categoryId": 1, "categoryName": "21km Half Marathon", "distanceKM": 21.10, "entryFee": 280.00 } ]` |
| `POST` | `/api/events/{eventId}/categories` | Add a category to an event | Organiser | `{ "categoryName": "10km Fun Run", "distanceKM": 10.00, "entryFee": 150.00 }` | `201 Created` - `{ "categoryId": 2, "message": "Category added" }` |

5. Event Enrolments
Tracks participant registrations for specific event categories.

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `POST` | `/api/enrolments` | Register for an event category | Participant | `{ "categoryId": 1 }` | `201 Created` - `{ "enrolmentId": 10, "status": "Paid" }` |
| `GET` | `/api/enrolments/my-races` | View registered events | Participant | None | `200 OK` - `[ { "enrolmentId": 10, "eventName": "Soweto Half Marathon", "categoryName": "21km" } ]` |
| `GET` | `/api/events/{eventId}/enrolments` | View enrolments for an event | Organiser | None | `200 OK` - `[ { "enrolmentId": 10, "participantName": "Nathan Jayanath", "categoryName": "21km" } ]` |

6. Results
Manages finish times and rankings for completed events.

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `POST` | `/api/results` | Record completion time | Organiser | `{ "enrolmentId": 10, "finishTime": "01:42:15", "overallPosition": 14, "categoryPosition": 4 }` | `201 Created` - `{ "resultId": 100, "message": "Result recorded" }` |
| `GET` | `/api/results/my-results` | View user results | Participant | None | `200 OK` - `[ { "eventName": "Soweto Half Marathon", "finishTime": "01:42:15", "overallPosition": 14 } ]` |
| `GET` | `/api/events/{eventId}/results` | View full event leaderboard | Public | None | `200 OK` - `[ { "participantName": "Nathan Jayanath", "finishTime": "01:42:15", "overallPosition": 14 } ]` |
