# Fetch data

Data is fetched based on addresses and meters. These a cached in the database to avoid fetching the same data multiple times. If the data is not cached, the data is fetched from the connectors and cached in the database.
It should be possible for the user to force a refresh of cached data.

The user can then fetch data from an address/meter. The system will then fetch the connector for the address/meter and then fetch the data from the connector. This avoids varmeoverblik having to ask all connectors for data.

```mermaid
sequenceDiagram

actor user as User
participant vo as Varmeoverblik.dk
participant db as Database
participant c as Specific Connector
participant cs as All Connectors

user->>+vo: Get addresses
vo->>+db: Get cached addresses
db-->>-vo: Return addresses
alt No cached addresses
    vo->>+cs: Get addresses
    cs-->>-vo: Return addresses
    vo->>+db: Cache addresses
end
vo-->>-user: Return addresses
user->>+vo: Get data for address
vo->>+db: Get connector for address
db-->>-vo: Return connector
vo->>+c: Get data for address
c-->>-vo: Return data
vo-->>-user: Return data

```