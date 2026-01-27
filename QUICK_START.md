# QUICK START GUIDE

## ⚡ Fast Setup (5 minutes)

### Step 1: Extract the ZIP
Extract `gatling-project.zip` to your desired location

### Step 2: Verify Java & Maven
```bash
java -version    # Should show Java 11
mvn -version     # Should show Maven installed
```

### Step 3: Compile
```bash
cd gatling-project
mvn clean compile
```

### Step 4: Run the Test
```bash
mvn gatling:test
```

## 📊 What Happens?

The test will:
1. ✅ Run for 10 minutes
2. ✅ Execute 7 different API calls per user
3. ✅ Use 2 users per second
4. ✅ Read data from CSV file
5. ✅ Group operations logically
6. ✅ Log each request
7. ✅ Validate against assertions
8. ✅ Generate HTML report

## 📈 View Results

After test completes:
```bash
# Report location will be printed in console
# Open: target/gatling/dummyjsonsimulation-<timestamp>/index.html
```

## 🎯 Key Files to Know

| File | Purpose |
|------|---------|
| `DummyJsonSimulation.java` | Main test config & assertions |
| `UserScenario.java` | Test flow with groups |
| `UserRequests.java` | API call definitions |
| `users.csv` | Test data |
| `HttpConfig.java` | Base URL & headers |

## 🔧 Quick Customizations

### Change test duration:
**File:** `DummyJsonSimulation.java`
```java
constantUsersPerSec(2).during(600)  // 600 = 10 minutes
                                     // Change to 60 for 1 minute
```

### Change users per second:
```java
constantUsersPerSec(2)  // Change 2 to desired number
```

### Add more test users:
**File:** `src/test/resources/data/users.csv`
Add more rows with: firstName, lastName, age, email

### Change API endpoint:
**Option 1 - Command line:**
```bash
mvn gatling:test -DbaseUrl=https://your-api.com
```

**Option 2 - Config file:**
Edit `HttpConfig.java` → change `https://dummyjson.com`

## ✅ Success Criteria

Test passes if:
- ✓ Success rate > 95%
- ✓ Max response time < 5 seconds
- ✓ Mean response time < 2 seconds
- ✓ 95th percentile < 3 seconds

## 🐛 Troubleshooting

**Error: "Cannot find symbol"**
```bash
mvn clean install -U
```

**Error: "Port already in use"**
- This is normal, Gatling will find another port

**Test fails assertions**
- Check internet connection
- API might be slow/down
- Adjust thresholds in `DummyJsonSimulation.java`

**Maven not found**
- Install Maven: https://maven.apache.org/download.cgi
- Add to PATH

## 📞 Need Help?

1. Check `README.md` for detailed documentation
2. Review console output for specific errors
3. Check HTML report for failure details
4. Verify all files compiled: `mvn clean compile`

## 🚀 Ready?

```bash
mvn clean compile
mvn gatling:test
```

Enjoy your performance testing! 🎉
