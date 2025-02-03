# Faculty Hours Broker Service

## Overview
The Faculty Hours Broker is a message broker service that facilitates communication between various components of the Faculty Hours system. It uses RabbitMQ as the message broker to enable reliable message queuing and routing between services.

## Tech Stack
- RabbitMQ (v3.13.4)
- Docker & Docker Compose
- Network Configuration:
  - Internal faculty network
  - External common network for cross-service communication

## Prerequisites
- Docker and Docker Compose installed
- Access to the common network infrastructure
- Environment variables configured

## Setup Instructions

### 1. Configuration
1. Copy `definitions_example.json` to `definitions.json`:
   ```bash
   cp definitions_example.json definitions.json
   ```

2. Update the following in `definitions.json`:
   - Set username and password in the users section
   - Configure vhost permissions as needed

3. Create `.docker/.env` file with required environment variables:
   ```
   RABBITMQ_USER=your-username
   RABBITMQ_PASSWORD=your-password
   ```

### 2. Running the Service
1. Navigate to the project directory:
   ```bash
   cd faculty-hours-broker
   ```

2. Start the service using Docker Compose:
   ```bash
   docker-compose -f .docker/docker-compose.yml up -d
   ```

3. Verify the service is running:
   ```bash
   docker-compose -f .docker/docker-compose.yml ps
   ```

The RabbitMQ management interface will be available at `http://localhost:15672`

## Service Connections

### Ports
- 5672: AMQP protocol port
- 15672: Management interface port

### Networks
- `faculty_network`: Internal network for faculty-related services
- `common_network`: External network for cross-service communication

### Connected Services
The broker service facilitates communication between:
- Faculty Hours API services
- Faculty management services
- Other related microservices in the ecosystem

## Monitoring and Management
- Access the RabbitMQ Management UI: `http://localhost:15672`
- Default credentials are configured in the `definitions.json` file
- Monitor queues, exchanges, and message flow through the management interface

## Troubleshooting
1. If the service fails to start, check:
   - Docker daemon is running
   - Required ports (5672, 15672) are available
   - Environment variables are properly set
   - Network connectivity

2. For connection issues:
   - Verify network configurations
   - Check service logs: `docker-compose -f .docker/docker-compose.yml logs`

## Security Notes
- Always change default credentials in production
- Use secure passwords and update them regularly
- Restrict access to management interface in production environments
- Keep RabbitMQ version updated for security patches