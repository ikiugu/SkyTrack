# SkyTrack

SkyTrack is a polished end-to-end project that uses live aviation data, generative AI, and event-driven design to deliver a world-class travel experience. It demonstrates sophisticated backend and mobile engineering while remaining achievable for an MVP within four days.

## Overview

This system is designed around Emirates-like operations: users can search, book, and check-in for flights, receive live gate changes and delays, and chat with an AI assistant—all powered by Spring Boot, Kafka, GraphQL, and Jetpack Compose.

## Architecture

SkyTrack consists of two main components:

- **Android App** (`/android`) - A native Android application built with Jetpack Compose
- **Spring Boot Server** (`/server`) - A backend service powered by Spring Boot, Kafka, and GraphQL

## Key Features

- **Flight Search & Booking** - Search and book flights with real-time availability
- **Check-in** - Digital check-in capabilities
- **Live Updates** - Real-time gate changes and flight delays via event-driven architecture
- **AI Assistant** - Chat with an AI assistant for travel support
- **Event-Driven Design** - Powered by Apache Kafka for real-time data streaming

## Tech Stack

### Backend
- Spring Boot
- Apache Kafka
- GraphQL
- REST APIs

### Mobile
- Android (Kotlin)
- Jetpack Compose
- Modern Android Architecture Components

## Project Structure

```
SkyTrack/
├── android/          # Android application (Jetpack Compose)
├── server/           # Spring Boot backend service
└── docs/             # Project documentation
```

## Getting Started

### Prerequisites

- JDK 17 or higher
- Android Studio (latest stable version)
- Docker (for Kafka)
- Gradle 7.5+

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd SkyTrack
```

2. Start the backend services:
```bash
cd server
# Follow server-specific setup instructions
```

3. Set up the Android app:
```bash
cd android
# Follow Android-specific setup instructions
```

## Development

This project was built as an MVP demonstration of modern full-stack development practices, focusing on:
- Clean architecture
- Event-driven microservices
- Real-time data synchronization
- AI integration
- Mobile-first design

## License

[Specify license here]

## Contributing

[Contributing guidelines]
