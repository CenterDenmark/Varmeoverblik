# Token usage

The following sequence diagram shows how the refresh token is used to get an access token. The refresh token is created by the user and stored in the database. The user then requests an access token with the refresh token. The API checks if the token is enabled and if the user has access. If the user has access or sharing agreements grant access, the API returns an access token.


```mermaid	
sequenceDiagram

actor User
participant Varmeoverblik
participant API
participant database

User->>+Varmeoverblik: Create refresh token
Varmeoverblik->>+database: Store refresh token info (not the token itself) 
Varmeoverblik-->>-User: Return refresh token
User->>+API: Request access token with refresh token
API->>+database: Is token enabled?
database-->>-API: Yes
alt Owner requesting token
    API->>+Connectors: User has access
    Connectors-->>-API: true
else Service provider requesting token
    API->>database: Get owner id
    database-->>API: Return owner id
    API->>+Connectors: Owner has access
    Connectors-->>-API: true
end
API->>-User: Return access token
```