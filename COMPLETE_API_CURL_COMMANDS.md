# Complete API cURL Commands for Airline Management System

## 🚀 **API Gateway Base URL**
```
http://localhost:3004
```

## 📋 **Service Ports**
- **API Gateway:** 3004
- **Auth Service:** 3000
- **Flight Search Service:** 3001
- **Booking Service:** 3002
- **Reminder Service:** 3003

---

## 🔐 **AUTH SERVICE ENDPOINTS**

### 1. User Signup
```bash
curl -X POST http://localhost:3004/authservice/api/v1/signup \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "password123"
  }'
```

### 2. User Signin
```bash
curl -X GET "http://localhost:3004/authservice/api/v1/signin" \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "password123"
  }'
```

### 3. Check Authentication
```bash
curl -X GET "http://localhost:3004/authservice/api/v1/isAuthenticated" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

### 4. Check Admin Status
```bash
curl -X GET "http://localhost:3004/authservice/api/v1/isAdmin" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "id": 1
  }'
```

---

## ✈️ **FLIGHT SEARCH SERVICE ENDPOINTS**

### **City Management**

#### 1. Create City
```bash
curl -X POST "http://localhost:3004/flightsearchservice/api/v1/city" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "name": "Mumbai"
  }'
```

#### 2. Get All Cities
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/city" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

#### 3. Get City by ID
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/city/1" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

#### 4. Update City
```bash
curl -X PATCH "http://localhost:3004/flightsearchservice/api/v1/city/1" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "name": "New Mumbai"
  }'
```

#### 5. Delete City
```bash
curl -X DELETE "http://localhost:3004/flightsearchservice/api/v1/city/1" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

#### 6. Create Multiple Cities
```bash
curl -X POST "http://localhost:3004/flightsearchservice/api/v1/cityMultiple" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "cities": [
      {"name": "Delhi"},
      {"name": "Bangalore"},
      {"name": "Chennai"}
    ]
  }'
```

#### 7. Get Airports by City
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/cityAirport/1" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

### **Airport Management**

#### 1. Create Airport
```bash
curl -X POST "http://localhost:3004/flightsearchservice/api/v1/airports" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "name": "Chhatrapati Shivaji International Airport",
    "address": "Mumbai, Maharashtra",
    "cityId": 1
  }'
```

### **Flight Management**

#### 1. Create Flight
```bash
curl -X POST "http://localhost:3004/flightsearchservice/api/v1/flights" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "flightNumber": "AI101",
    "airplaneId": "AIR001",
    "departureAirportId": "DEL",
    "arrivalAirportId": "BOM",
    "arrivalTime": "2024-01-15T10:30:00",
    "departureTime": "2024-01-15T08:00:00",
    "price": "12000",
    "boardingGate": "A1"
  }'
```

#### 2. Get All Flights (with filters)
```bash
# Get all flights
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"

# Get flights with filters
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights?departureAirportId=DEL&arrivalAirportId=BOM&minPrice=5000&maxPrice=15000" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

#### 3. Get Flight by ID
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights/1" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

#### 4. Update Flight
```bash
curl -X PATCH "http://localhost:3004/flightsearchservice/api/v1/flights/1" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "price": "15000",
    "boardingGate": "A2"
  }'
```

---

## 🎫 **BOOKING SERVICE ENDPOINTS**

### 1. Create Booking
```bash
curl -X POST "http://localhost:3004/bookingservice/api/v1/bookings" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "flightId": 1,
    "userId": 1,
    "noOfSeats": 2,
    "totalCost": 24000
  }'
```

### 2. Update Booking
```bash
curl -X PATCH "http://localhost:3004/bookingservice/api/v1/bookings/1" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "status": "Booked",
    "noOfSeats": 3,
    "totalCost": 36000
  }'
```

### 3. Publish Message to Queue
```bash
curl -X POST "http://localhost:3004/bookingservice/api/v1/publish" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

---

## 📧 **REMINDER SERVICE ENDPOINTS**

### 1. Create Notification Ticket
```bash
curl -X POST "http://localhost:3004/reminderservice/api/v1/tickets" \
  -H "Content-Type: application/json" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE" \
  -d '{
    "subject": "Flight Reminder",
    "content": "Your flight is scheduled in 2 hours",
    "recepientEmail": "user@example.com",
    "notificationTime": "2024-06-23T06:38:41"
  }'
```

---

## 🔍 **FLIGHT SEARCH EXAMPLES**

### Search by Route
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights?departureAirportId=DEL&arrivalAirportId=BOM" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

### Search by Price Range
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights?minPrice=5000&maxPrice=15000" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

### Search by Date
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights?departureDate=2024-01-15" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

### Search by Flight Number
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights?flightNumber=AI101" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

### Combined Search
```bash
curl -X GET "http://localhost:3004/flightsearchservice/api/v1/flights?departureAirportId=DEL&arrivalAirportId=BOM&departureDate=2024-01-15&minPrice=5000&maxPrice=15000" \
  -H "x-access-token: YOUR_JWT_TOKEN_HERE"
```

---

## 📝 **SAMPLE DATA FOR TESTING**

### Sample Cities
```json
{
  "name": "Mumbai"
}
```

### Sample Airports
```json
{
  "name": "Chhatrapati Shivaji International Airport",
  "address": "Mumbai, Maharashtra",
  "cityId": 1
}
```

### Sample Flights
```json
{
  "flightNumber": "AI101",
  "airplaneId": "AIR001",
  "departureAirportId": "DEL",
  "arrivalAirportId": "BOM",
  "arrivalTime": "2024-01-15T10:30:00",
  "departureTime": "2024-01-15T08:00:00",
  "price": "12000",
  "boardingGate": "A1"
}
```

### Sample Bookings
```json
{
  "flightId": 1,
  "userId": 1,
  "noOfSeats": 2,
  "totalCost": 24000
}
```

### Sample Notification Tickets
```json
{
  "subject": "Flight Reminder",
  "content": "Your flight is scheduled in 2 hours",
  "recepientEmail": "user@example.com",
  "notificationTime": "2024-06-23T06:38:41"
}
```

---

## ⚠️ **IMPORTANT NOTES**

1. **Authentication Required:** Most endpoints require the `x-access-token` header with a valid JWT token
2. **Service Dependencies:** Ensure all services are running on their respective ports
3. **Database Setup:** Make sure the database is properly configured and migrations are run
4. **Error Handling:** All endpoints return standardized error responses
5. **Rate Limiting:** API Gateway has rate limiting (5 requests per 2 minutes)

## 🔧 **TROUBLESHOOTING**

### Common Issues:
1. **401 Unauthorized:** Check if JWT token is valid and included in headers
2. **404 Not Found:** Verify the service is running on the correct port
3. **500 Internal Server Error:** Check database connection and service logs
4. **429 Too Many Requests:** Wait before making more requests (rate limiting)

### Testing Sequence:
1. Start all services
2. Create a user account (signup)
3. Get authentication token (signin)
4. Use the token for subsequent API calls
5. Test other endpoints with the token 