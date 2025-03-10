# Creme Dela Creme

## Project timeline and Requirements

### Phase 1: Core Platform APIs

- **Movie/Series Inventory**: Core APIs for fetching movies and series.
- **Customer Services**: User management, profiles, preferences
- **API Gateway & Auth**: Security foundation first to ensure all services have proper authentication
- **Actor/Actress Services**: Core APIs for fetching actors and actresses.

#### Key Components:

1. cdlc-inventory
2. cdlc-actor
3. cdlc-customer-services
4. cdlc-configurations-server
5. cdlc-gateway
6. cdlc-authorization-server

### Phase 2: Social Interactions & Discovery

- **Social Network Features**: Lists, reviews, ratings, user connections
- **Recommendation Engine**: Initial version based on user behaviour and preferences
- **Feeds & Content Discovery**: Social activity feeds

#### Key Components:

1. cdlc-feed
2. cdlc-recommendation
3. cdlc-analytics
4. cdlc-datalake-workflows

### Phase 3: Booking System

- **Theatre Booking Service**: Seat selection, venue management
- **Order Management**: Cart, checkout flows
- **Payment Processing**: Payment gateway integration, subscription management

#### Key Components:

- cdlc-booking
- cdlc-order
- cdlc-payment
- cdlc-dispatched-service

### Phase 4: Streaming Platform

- **Media Storage Services**: Optimized image and video storage systems
- **Video Processing Pipeline**: Transcoding, streaming, format optimization
- **Content Delivery Optimization**: Caching, CDN integration

#### Key Components:

- cdlc-metadata-storage (Golang)
- cdlc-video-processors (C++/Golang)
- Streaming infrastructure setup

### Phase 5: Integration & Enhancement

- **Advanced Analytics & AI**: Enhanced recommendation system with AI/ML
- **Platform Performance Optimization**: Caching strategies, scalability testing
- **End-to-End Testing**: Integration tests, performance benchmarks
- **Final Deployment**: Production readiness review, launch preparation

#### Key Components:

- cdlc-e2e (Selenium, JUnit5)
- cdlc-deployment (Docker, K8s)


## Architecture

### Database Strategy 

#### Tiered Database Approach:

1. **OLTP Layer**: MySQL for transactional data (users, orders, bookings)
2. **Caching Layer**: Redis for frequently accessed data and sessions
3. **NoSQL Layer**: ScyllaDB for high-throughput use cases (streaming metadata)
4. **OLAP Layer**: Add a proper analytical database (consider ClickHouse or BigQuery)
5. **Graph Layer**: Neo4j for social relationships


#### Data Flow Optimization:

1. Implement CDC (Change Data Capture) from OLTP to OLAP
2. Use Kafka as the backbone for event-driven architecture
3. Develop data pipelines for analytics to reduce load on operational systems


### Service Boundary Recommendations

#### Bounded Contexts:

1. **Content Domain**: Movies, series, actors (content metadata)
2. **User Domain**: Profiles, preferences, social interactions
3. **Commerce Domain**: Bookings, orders, payments
4. **Streaming Domain**: Media processing, streaming, consumption analytics


### API Design:

1. REST for standard CRUD operations
2. GraphQL for social features (better fits complex relationships)
3. gRPC for high-performance internal service communication


## Technical Optimizations

### Performance Considerations:

1. Implement read replicas for high-traffic services
2. Use CQRS pattern to separate read and write operations
3. Deploy CDN for static assets and streaming content


### Scalability Strategy:

1. Design horizontal scaling for all services
2. Implement proper sharding strategy for databases
3. Use autoscaling based on traffic patterns


### Resilience Patterns:

1. Circuit breakers between services
2. Retry mechanisms with exponential backoff
3. Proper fallback mechanisms for critical services

### Key Risks & Mitigations

#### Integration Complexity:

* Risk: Many services with complex interactions
* Mitigation: Clear API contracts, comprehensive integration tests, service mesh


#### Streaming Performance:

* Risk: High demands on video processing
* Mitigation: Early load testing, C++ optimization for critical paths, CDN integration


#### Data Consistency:

* Risk: Distributed data across multiple databases
* Mitigation: Event sourcing pattern, saga pattern for distributed transactions


#### Development Timeline:

* Risk: Ambitious schedule with dependencies
* Mitigation: Modular approach allowing parallel development, clear MVP definition
