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

### API

- Faker-js: A JavaScript library for generating fake data for various data types like names, addresses, emails, and more. It is useful for testing and development purposes.
- Prisma: An open-source ORM (Object-Relational Mapping) tool for Node.js and TypeScript that simplifies database access and management with an auto-generated, type-safe query builder.
- Tsup: A zero-config TypeScript bundler for modern JavaScript applications.
- Tsx: A TypeScript execution environment for Node.js, allowing TypeScript files to be run directly without needing a separate compilation step.
- Fastify: A highly performant web framework for Node.js, designed for building fast and low-overhead HTTP services.
- Dayjs: A minimalist JavaScript library for parsing, validating, manipulating, and formatting dates.
- Zod: A TypeScript-first schema declaration and validation library for JavaScript.

### Deploy

- Docker: A platform that enables developers to automate the deployment of applications inside lightweight, portable containers.
- Docker Compose: A tool for defining and running multi-container Docker applications.
- Kubernetes (kubectl): Kubernetes is an open-source container orchestration platform for automating deployment, scaling, and management of containerized applications.
- K3D: A lightweight wrapper to run Kubernetes (K3s) in Docker.
- DigitalOcean: A cloud infrastructure provider offering scalable compute, storage, and networking solutions.
- GitHub Actions: A CI/CD platform integrated into GitHub, allowing users to automate workflows for building, testing, and deploying their code.
- CI/CD: Stands for Continuous Integration and Continuous Deployment/Delivery.
- IAC: The practice of managing and provisioning computing infrastructure through machine-readable configuration files, rather than through physical hardware configuration or interactive configuration tools.
- Lens: A Kubernetes integrated development environment (IDE) that provides a graphical user interface to manage and troubleshoot Kubernetes clusters.
- Helm: A package manager for Kubernetes that helps define, install, and upgrade complex Kubernetes applications.
- Terraform: An open-source infrastructure as code tool that allows users to define and provision data center infrastructure using a high-level configuration language.

# How to run the project

Node version used: v20.9.0

## Application

```bash
# To install project dependencies
yarn
```

- Create a .env file, using the .env.example as example.

- Create a local postgresql DB.

```bash
yarn prisma generate
```

```bash
yarn db:migrate
```

```bash
# Run the application on localhost -> http://localhost:3333
yarn dev
```

# Author

Made with 💚 by Guilherme Bafica 👋

[![LinkedIn Badge](https://img.shields.io/badge/-GuilhermeBafica-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/guilhermebafica/)](https://www.linkedin.com/in/guilhermebafica/)
