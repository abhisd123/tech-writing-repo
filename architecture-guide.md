# Microsystem Integration Architecture

This guide outlines the event-driven architecture used to synchronize data across our primary microsystems: the User Service, the Billing Service, and the Notification Service.

## Overview

To prevent tight coupling between distinct domains, our backend relies on an asynchronous, event-driven architecture using Apache Kafka as the central message broker. This ensures that a failure in the Notification Service does not impact the critical path of the Billing Service.

## Core Components

1. **API Gateway:** The single entry point for all client requests. It handles rate limiting, authentication, and request routing.
2. **User Service:** Manages identity, profile data, and access control. 
3. **Billing Service:** Processes transactions and generates invoices.
4. **Kafka Event Bus:** The centralized streaming platform that routes domain events (e.g., `user.created`, `invoice.paid`) to subscribed services.

## Event Flow: Account Creation

When a new user registers, the system executes the following flow:

1. The client sends a `POST /register` request to the API Gateway.
2. The Gateway routes the payload to the **User Service**.
3. The User Service commits the new user record to its dedicated database.
4. The User Service publishes a `user.created` event to the **Kafka Event Bus**.
5. The **Billing Service** consumes the event and provisions a billing profile for the user.
6. The **Notification Service** consumes the event and dispatches a welcome email.

## Design Considerations

* **Eventual Consistency:** Because services operate asynchronously, there is a slight delay (typically under 50ms) before the Billing Service recognizes a newly created user. Client applications must be designed to handle this brief propagation window.
* **Database per Service:** Each microsystem maintains its own independent database schema. Direct cross-database queries are strictly prohibited to maintain domain isolation.
