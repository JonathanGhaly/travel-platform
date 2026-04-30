```
                           +---------------------------+
                           |        Web / Mobile       |
                           |        Frontend App       |
                           +-------------+-------------+
                                         |
                                         |
                                   HTTPS / REST
                                         |
                                         v
                              +-------------------+
                              |     API Gateway    |
                              | (Routing, Auth,    |
                              |  Rate limiting)    |
                              +---------+----------+
                                        |
        -----------------------------------------------------------------------------------------
        |                       |                      |               |                        | 
        v                       v                      v               v                        v

+---------------+      +---------------+      +---------------+   +----------------+      +---------------+
|   Auth        |      |   Booking     |      |   Itinerary   |   |  Notification  |      |   User        |
|   Service     |      |   Service     |      |   Service     |   |   Service      |      |   Service     |
|---------------|      |---------------|      |---------------|   |----------------|      |---------------|
| JWT/Auth      |      | Booking logic |      | Trip planning |   | Send alerts    |      |Register logic |
| User accounts |      | Reservation   |      | POI schedule  |   | Email / Push   |      |               |
+-------+-------+      +-------+-------+      +-------+-------+   +--------+-------+      +-------+-------+
        |                      |                      |                    |                      |
        |                      |                      |                    |                      |
        v                      v                      v                    v                      v 
 +-------------+        +-------------+        +-------------+      +-------------+        +-------------+
 | Auth DB     |        | Booking DB  |        | Itinerary DB|      |Notify DB    |        | Users DB    |
 | Auth        |        | bookings    |        | itineraries |      |notifications|        | users       |
 +-------------+        +-------------+        | items       |      +-------------+        +-------------+
                                               +-------------+

                         -------- Event Driven Communication --------

                                   +-------------------+
                                   |                   |                                                     +---------------+                    
                                   |       Kafka       | --------------------------------------------------->| Data Pipeline |
                                   |   Event Broker    |                                                     +---------------+
                                   |                   |                                                              |
                                   +---------+---------+                                                              v        
                                             |                                                                +---------------+
               -----------------------------------------------------------                                    | ML Training   |
               |                         |                               |                                    +---------------+
               v                         v                               v                                            |
                                                                                                                      v
        user-created             booking-created                 itinerary-updated                          +---------------------+
          (User)                   (Booking)                        (Itinerary)                             | recommendation-API  |
                                                                                                            |  (FastAPI + ML)     |          
               |                         |                               |                                  +---------------------+
               +-------------------------+-------------------------------+
                                         |
                                         v
                                Notification Service
                                sends email / push
```