# Gatling Performance Testing Framework

## Project Details
- **Java Version:** 11
- **Gatling Version:** 3.14.9
- **Gatling Maven Plugin:** 4.20.8
- **Test Duration:** 10 minutes (600 seconds)
- **Load Pattern:** 2 users per second (with ramp-up/ramp-down)

## Project Structure
```
gatling-project/
├── pom.xml
├── src/
│   └── test/
│       ├── java/
│       │   └── perf/
│       │       ├── config/
│       │       │   └── HttpConfig.java          # HTTP protocol configuration
│       │       ├── requests/
│       │       │   └── UserRequests.java        # API request definitions
│       │       ├── scenarios/
│       │       │   └── UserScenario.java        # Test scenario with groups
│       │       └── simulations/
│       │           └── DummyJsonSimulation.java # Main simulation
│       └── resources/
│           └── data/
│               └── users.csv                    # Test data
└── README.md
```

## Features Implemented

### ✅ Multiple API Calls
- **GET /users** - Retrieve all users
- **GET /users/{id}** - Retrieve single user
- **POST /users/add** - Add new user
- **PUT /users/{id}** - Update user
- **DELETE /users/{id}** - Delete user
- **GET /products** - Retrieve products
- **GET /products/search** - Search products

### ✅ Groups
- **Read Operations** - GET requests grouped together
- **Write Operations** - POST/PUT requests grouped together
- **Product Operations** - Product-related requests
- **Delete Operations** - DELETE requests

### ✅ Logging
- Console logs for each API call
- Session-level logging for user data
- Visual test start/end markers
- Request status logging

### ✅ Assertions
- **Response Time:**
  - Max response time < 5 seconds
  - Mean response time < 2 seconds
  - 95th percentile < 3 seconds
- **Success Rate:**
  - Success rate > 95%
  - Failure rate < 5%
- **Group-specific:**
  - Read Operations < 2s
  - Write Operations < 3s
  - Product Operations < 2.5s

### ✅ Dataset
- CSV file with user data (10 users)
- Circular feeder for data reuse
- Dynamic data injection into requests

## Load Pattern
```
Ramp Up:   1 → 2 users/sec (30 seconds)
Steady:    2 users/sec     (540 seconds / 9 minutes)
Ramp Down: 2 → 0 users/sec (30 seconds)
────────────────────────────────────────
Total:     600 seconds (10 minutes)
```

## How to Run

### Prerequisites
- Java 11 installed
- Maven installed

### Commands

1. **Compile the project:**
   ```bash
   mvn clean compile
   ```

2. **Run the test:**
   ```bash
   mvn gatling:test
   ```

3. **Run with custom base URL:**
   ```bash
   mvn gatling:test -DbaseUrl=https://your-api.com
   ```

4. **Run specific simulation:**
   ```bash
   mvn gatling:test -Dgatling.simulationClass=perf.simulations.DummyJsonSimulation
   ```

## Test Reports

After test execution, Gatling generates HTML reports:
- Location: `target/gatling/`
- Open `index.html` in your browser for detailed results

## Customization

### Modify Load Pattern
Edit `DummyJsonSimulation.java`:
```java
constantUsersPerSec(2).during(600)  // Change 2 to desired users/sec
                                     // Change 600 to desired duration
```

### Add More Test Data
Edit `src/test/resources/data/users.csv` and add more rows

### Change Base URL
Either:
- Modify `HttpConfig.java`
- Or use: `-DbaseUrl=https://your-url.com`

### Adjust Assertions
Edit the `.assertions()` section in `DummyJsonSimulation.java`

## API Endpoint
Default: `https://dummyjson.com`
- Free fake REST API for testing
- No authentication required
- Rate limits may apply

## Troubleshooting

**Compilation errors:**
```bash
mvn clean install -U
```

**Port already in use:**
```bash
# Gatling uses random ports for reports
# No action needed
```

**Test fails assertions:**
- Check network connectivity
- Review Gatling HTML report for details
- Adjust assertion thresholds if needed

## Sample Output
```
╔════════════════════════════════════════════════════════════╗
║          GATLING PERFORMANCE TEST - STARTING               ║
║  Duration: 10 minutes | Users: 2 per second               ║
╚════════════════════════════════════════════════════════════╝

========================================
Starting test for user: John Doe
========================================
✓ GET /users - Status: 200
✓ GET /users/1 - Status: 200
✓ POST /users/add - Created user: John
✓ PUT /users/1 - User updated
✓ GET /products - Total products: 100
✓ GET /products/search - Search completed
✓ DELETE /users/1 - User deleted
========================================
Test completed for user: John
========================================
```

## Support
For issues or questions:
1. Check Gatling documentation: https://gatling.io/docs/
2. Review Maven output for compilation errors
3. Check `target/gatling/` for detailed test reports

## License
This is a sample performance testing framework for educational purposes.
