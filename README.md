# HyperBus

A bus ticket booking application built with the MERN stack (MongoDB, Express, React, Node.js). Passengers search trips and book seats, operators manage their buses and trips, and admins moderate users and operators.

## Features

- **Roles**: `user`, `operator` and `admin`, with JWT authentication and role-based route protection.
- **Passengers**: register and log in, search trips (`/trips/search`), book seats, view and cancel bookings, rate completed trips, and edit their profile.
- **Operators**: create, update and delete buses and trips. Operators must be verified by an admin first.
- **Admins**: list users and operators, block and unblock users, verify operators, view all trips and bookings, and cancel trips.
- **Seat booking checks**: seat numbers must be within the bus capacity and unique. Seats of expired bookings are released.
- **Operations**: request rate limiting, Winston and Morgan logging, a Filebeat, Logstash and Elasticsearch setup for logs, and Docker Compose.

## Tech stack

| Part | Technology |
|---|---|
| Client (`client/`) | React 19, React Router, Axios, react-datepicker, Vite |
| Server (`server/`) | Node.js, Express 4, Mongoose (MongoDB), JSON Web Tokens, bcrypt, express-rate-limit, Winston |
| Tests | Jest unit tests and load tests under `server/src/tests` |

## API routes

| Prefix | Routes |
|---|---|
| `/users` | `POST /register`, `POST /login`, `POST /logout`, `GET /profile`, `PUT /profile` |
| `/buses` | `POST /`, `GET /`, `PUT /:busId`, `DELETE /:busId` (operator) |
| `/trips` | `GET /search`, `POST /`, `GET /`, `PUT /:tripId`, `DELETE /:tripId` |
| `/bookings` | `POST /`, `GET /`, `POST /:id/cancel` |
| `/ratings` | `POST /bookings/:bookingId`, `GET /`, `GET /trips/:tripId`, `PUT /:ratingId`, `DELETE /:ratingId` |
| `/admin` | `GET /users`, `GET /operators`, `PUT /block/:userId`, `PUT /unblock/:userId`, `PUT /verify-operator/:userId`, `GET /trips`, `GET /bookings`, `PUT /trips/:tripId/cancel` |

## Run locally

**Server**

```bash
cd server
npm install
cp .env.example .env     # set PORT, MONGO_URI and JWT_SECRET
npm run server
npm test                 # unit tests
```

**Client**

```bash
cd client
npm install
npm run dev
```

**Docker**: `server/docker-compose.yml` starts the server (port 5001, image `jvishwa06/hyperbus`) together with Elasticsearch 8.12 for logs.
