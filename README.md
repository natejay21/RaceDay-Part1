RaceDay-Part1
Prog6212 part 1 

RaceDay Platform - Part 1 Specification & Database Design

This repository contains the architecture, data model, API endpoint specifications, and database initialization scripts for the RaceDay event management system.



Repository Structure

text
RaceDay/
.github/
workflows/
validate-docs.yml     CI/CD documentation validation workflow
docs/
ERD.png                   Entity Relationship Diagram
endpoints.md              RESTful API Endpoint Specification Plan & Requirements Mapping
schema.sql                SQL DDL Script & Seed Data (Microsoft SQL Server)
└── README.md                     Project overview and setup documentation


Role-Based System Architecture
The RaceDay platform utilizes role-based access control to enforce separation of concerns between system stakeholders:

Organiser Role:
Manages race events (Create, Read, Update, Delete).
Configures event categories (distances, entry fees, age brackets).
Accesses event registration and participant enrolment lists.
Captures and records final race completion times and positions.

Participant Role:
Views upcoming race events and distance categories.
Enrols into event categories.
Views personal registration history (my-races).
Views personal race results and event leaderboards.


DB setup:
Launch Microsoft SQL Server Management Studio (SSMS) and connect to local SQL Server instance ((localdb)\MSSQLLocalDB).

Create a target database named RaceDayDB:

SQL
CREATE DATABASE RaceDayDB;
GO

Open and execute the initialization script located at docs/schema.sql.

Verify table creation (Users, Events, Categories, Routes, Enrolments, Results) and seeded test data.













