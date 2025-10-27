# API Contract

## GraphQL Schema

### Queries

#### Search Flights
```graphql
query SearchFlights($from: String!, $to: String!, $date: String!) {
  searchFlights(from: $from, to: $to, date: $date) {
    id
    flightNumber
    airline
    departure {
      airport
      city
      time
      gate
    }
    arrival {
      airport
      city
      time
      gate
    }
    duration
    price
    availableSeats
  }
}
```

#### Get Booking
```graphql
query GetBooking($bookingId: ID!) {
  booking(id: $bookingId) {
    id
    flight {
      id
      flightNumber
      departure {
        airport
        time
        gate
      }
      arrival {
        airport
        time
        gate
      }
    }
    passenger {
      name
      email
    }
    status
    seatNumber
    checkInStatus
  }
}
```

#### Get User Bookings
```graphql
query GetUserBookings {
  myBookings {
    id
    flight {
      flightNumber
      departure {
        time
        gate
      }
    }
    status
    checkInStatus
  }
}
```

### Mutations

#### Book Flight
```graphql
mutation BookFlight($flightId: ID!, $passenger: PassengerInput!) {
  bookFlight(flightId: $flightId, passenger: $passenger) {
    id
    bookingNumber
    status
    flight {
      flightNumber
    }
  }
}
```

#### Check In
```graphql
mutation CheckIn($bookingId: ID!) {
  checkIn(bookingId: $bookingId) {
    id
    checkInStatus
    seatNumber
    boardingPass {
      qrCode
      gate
      boardingTime
    }
  }
}
```

#### Send Chat Message
```graphql
mutation SendChatMessage($message: String!, $bookingId: ID) {
  sendChatMessage(message: $message, bookingId: $bookingId) {
    id
    message
    response
    timestamp
  }
}
```

### Subscriptions

#### Flight Updates
```graphql
subscription FlightUpdates($bookingId: ID!) {
  flightUpdates(bookingId: $bookingId) {
    type
    flightNumber
    update {
      ... on GateChange {
        oldGate
        newGate
        updatedAt
      }
      ... on Delay {
        previousTime
        newTime
        reason
        updatedAt
      }
      ... on StatusChange {
        previousStatus
        newStatus
        updatedAt
      }
    }
  }
}
```

## Kafka Topics

### Topic: `flight.updates`
**Purpose**: Real-time flight status updates from aviation data sources

**Sample Payload**:
```json
{
  "flightNumber": "EK205",
  "airline": "Emirates",
  "type": "DELAY",
  "departure": {
    "airport": "DXB",
    "scheduledTime": "2024-01-15T14:30:00Z",
    "estimatedTime": "2024-01-15T15:00:00Z",
    "gate": "A12"
  },
  "arrival": {
    "airport": "JFK",
    "scheduledTime": "2024-01-15T18:45:00Z",
    "estimatedTime": "2024-01-15T19:15:00Z"
  },
  "delayReason": "Weather conditions",
  "timestamp": "2024-01-15T13:00:00Z"
}
```

### Topic: `gate.changes`
**Purpose**: Gate assignment changes for flights

**Sample Payload**:
```json
{
  "flightNumber": "EK205",
  "departureAirport": "DXB",
  "oldGate": "A10",
  "newGate": "A12",
  "scheduledDeparture": "2024-01-15T14:30:00Z",
  "timestamp": "2024-01-15T13:15:00Z"
}
```

### Topic: `booking.created`
**Purpose**: New booking events

**Sample Payload**:
```json
{
  "bookingId": "BK123456",
  "flightId": "FL789",
  "flightNumber": "EK205",
  "passengerEmail": "user@example.com",
  "bookingStatus": "CONFIRMED",
  "timestamp": "2024-01-15T10:00:00Z"
}
```

### Topic: `checkin.completed`
**Purpose**: Check-in completion events

**Sample Payload**:
```json
{
  "bookingId": "BK123456",
  "flightNumber": "EK205",
  "seatNumber": "12A",
  "gate": "A12",
  "boardingTime": "2024-01-15T14:00:00Z",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Input Types

### PassengerInput
```graphql
input PassengerInput {
  name: String!
  email: String!
  phone: String
  dateOfBirth: String
  passportNumber: String
}
```
