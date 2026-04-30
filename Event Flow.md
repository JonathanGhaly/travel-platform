```
Client → API Gateway → Booking Service
Booking Service → Save booking
Booking Service → Publish "booking-created" event
Kafka → Notification Service
Notification Service → Send email/push
```