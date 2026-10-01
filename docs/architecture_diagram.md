# High-Level Architecture Diagram

```mermaid
graph TD
    %% Clients
    MobileApp[Mobile App<br/>React Native]
    WebApp[Web App<br/>React]
    
    %% Authentication
    Auth[Authentication<br/>Firebase Auth]
    
    %% API Gateway / Backend
    APIGateway[Backend API<br/>Node.js / NestJS]
    
    %% Microservices
    AIService[AI Service<br/>Python / FastAPI]
    
    %% Databases & Caching
    PrimaryDB[(Primary Database<br/>PostgreSQL)]
    Cache[(Cache<br/>Redis)]
    
    %% External Services
    ExternalAPIs[External APIs<br/>Nutrition/Wearables]
    
    %% Connections
    MobileApp -->|HTTPS/WSS| APIGateway
    WebApp -->|HTTPS/WSS| APIGateway
    MobileApp -->|Auth Token| Auth
    WebApp -->|Auth Token| Auth
    
    APIGateway -->|Verify Token| Auth
    APIGateway -->|Read/Write| PrimaryDB
    APIGateway -->|Cache Data| Cache
    APIGateway -->|gRPC/HTTP| AIService
    APIGateway -->|Fetch Data| ExternalAPIs
    
    AIService -->|Read Models| PrimaryDB
```

## Data Flows
- **Personalized Workout Plans:** The Backend API requests the AI Service to generate a plan based on user metrics stored in PostgreSQL. The AI Service processes this and returns the plan to the Backend, which caches it in Redis and sends it to the Mobile App.
- **Social Sharing:** Users submit a workout completion payload to the Backend API. The API updates the user's feed in PostgreSQL and triggers a real-time event via WebSockets to connected friends.
- **Nutrition Tracking:** Users search for food items. The Backend API queries an External Nutrition API, returns the results, and upon selection, saves the nutritional data to the user's daily log in PostgreSQL.
