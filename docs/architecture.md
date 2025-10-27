# Architecture

## End-to-End Flow

SkyTrack follows an event-driven architecture designed for real-time flight operations.

### Flight Search & Booking Flow

1. **Search**: User searches for flights via GraphQL query → Spring Boot backend queries flight data
2. **Book**: User selects and books a flight via GraphQL mutation → Backend creates booking and publishes `booking.created` event to Kafka
3. **Check-in**: User checks in via GraphQL mutation → Backend updates booking status and publishes `checkin.completed` event

### Real-Time Updates Flow

1. **Aviation Data Feed**: External aviation data source publishes flight updates to Kafka topics
2. **Event Processing**: Spring Boot consumes Kafka events (`flight.updates`, `gate.changes`, `delays`)
3. **Subscriptions**: Android app subscribes to GraphQL subscriptions for flight updates
4. **Live Sync**: GraphQL subscriptions push updates to connected clients in real-time

### AI Assistant Flow

1. **Chat**: User sends message via GraphQL mutation → Backend forwards to AI service
2. **Response**: AI generates response → Backend returns via GraphQL query response
3. **Context**: Conversation context maintained for booking-related queries

## Components

- **Android App**: Jetpack Compose UI consuming GraphQL API
- **Spring Boot Server**: GraphQL API gateway, business logic, Kafka producer/consumer
- **Kafka**: Event streaming platform for flight updates and booking events
- **AI Service**: Generative AI integration for travel assistance

## Data Flow

```
Aviation Data → Kafka Topics → Spring Boot Consumer → GraphQL Subscription → Android App
User Actions → Android App → GraphQL Mutation → Spring Boot → Kafka Topics → Other Services
```
