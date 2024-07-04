<h1 align="center">Pass In - DevOps</h1>

## About this Project

pass.in is an application for **managing participants in in-person events**.

The tool allows the organizer to register an event and open a public registration page. Registered participants can issue a credential for check-in on the day of the event.
The system will scan the participant's credentials to allow entry to the event.

## Functionalities

### Functional requirements

- [x] The organizer must be able to register a new event;
- [x] The organizer must be able to view event data;
- [x] The organizer must be able to view the list of participants;
- [x] The participant must be able to register for an event;
- [x] The participant must be able to view their registration badge;
- [x] The participant must be able to check-in at the event;

### Business rules

- [x] The participant can only register for an event once;
- [x] Participants can only register for events with available places;
- [x] The participant can only check-in to an event once;

### Non-functional requirements

- [x] Check-in at the event will be carried out using a QRCode;

## API Documentation (Swagger)

For API documentation, visit the [link](https://nlw-unite-nodejs.onrender.com/docs).

## Database

In this application we will use a relational database (SQL). For the development environment, we will continue with SQLite due to the ease of the environment.

During the deployment process, the database will be changed to Postgresql.

### ERD Diagram

<img src=".github/erd.svg" width="600" alt="Database ERD Diagram" />

### Database structure (SQL)

```sql
-- CreateTable
CREATE TABLE "events" (
    "id" TEXT NOT NULL PRIMARY KEY,
    "title" TEXT NOT NULL,
    "details" TEXT,
    "slug" TEXT NOT NULL,
    "maximum_attendees" INTEGER
);

-- CreateTable
CREATE TABLE "attendees" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "event_id" TEXT NOT NULL,
    "created_at" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT "attendees_event_id_fkey" FOREIGN KEY ("event_id") REFERENCES "events" ("id") ON DELETE RESTRICT ON UPDATE CASCADE
);

-- CreateTable
CREATE TABLE "check_ins" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "created_at" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    "attendeeId" INTEGER NOT NULL,
    CONSTRAINT "check_ins_attendeeId_fkey" FOREIGN KEY ("attendeeId") REFERENCES "attendees" ("id") ON DELETE RESTRICT ON UPDATE CASCADE
);

-- CreateIndex
CREATE UNIQUE INDEX "events_slug_key" ON "events"("slug");

-- CreateIndex
CREATE UNIQUE INDEX "attendees_event_id_email_key" ON "attendees"("event_id", "email");

-- CreateIndex
CREATE UNIQUE INDEX "check_ins_attendeeId_key" ON "check_ins"("attendeeId");
```

## Used Techs

<!-- - Tech 1: Enim sunt minim officia esse elit. -->

# How to run the project

Node version used: v20.9.0

<!-- ## Application

```bash
# To install project dependencies
yarn
```

```bash
# Run the application on localhost -> http://localhost:5173
yarn dev
``` -->

# Author

Made with 💚 by Guilherme Bafica 👋

[![LinkedIn Badge](https://img.shields.io/badge/-GuilhermeBafica-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/guilhermebafica/)](https://www.linkedin.com/in/guilhermebafica/)
