# Create sharing agreement

The service provider creates a link which data owners can use to create a sharing agreement with the service provider. When using the link, the owner will be present with the terms and conditions of the sharing agreement. The owner can then sign the agreement, and the service provider will be notified.

```mermaid	
sequenceDiagram

actor sp as Service Provider
participant vo as Varmeoverblik.dk
actor o as Owner

sp ->>+vo: Create link
vo-->>-sp: Return link
sp->>+o: Share link
o->>-vo: Sign agreement based on link
vo->>sp: Notify agreement signed
```