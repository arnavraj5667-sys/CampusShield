# CampusShield — Java GUI Cyber Safety Scanner

CampusShield is a student-focused Java Swing desktop application that performs **rule-based, heuristic checks** on URLs and user-provided messages. It returns a risk score (0–100), a SAFE / SUSPICIOUS / DANGEROUS label, and reasons for the result.

## Features
- Login screen (demo credentials: `student` / `1234`)
- URL scanning: HTTPS check, IP-address host check, `@` symbol, suspicious keywords, long URLs and repeated hyphens
- Message scanning: scam-related words, links, urgency language and money-related terms
- Risk scoring: 0–39 SAFE, 40–69 SUSPICIOUS, 70–100 DANGEROUS
- SQLite database using JDBC to save scan history
- History table and CSV report export
- Background scanning using `ExecutorService`; synchronized in-memory session history
- OOP: interface, abstract class, inheritance, polymorphism, encapsulation and custom exceptions

## Requirements
- JDK 17 or newer
- Apache Maven
- VS Code with Extension Pack for Java (recommended)

## Run in VS Code / terminal
1. Extract the project ZIP and open the `CampusShield` folder in VS Code.
2. Confirm Java 17+ and Maven are installed (`java -version`, `mvn -version`).
3. In the VS Code terminal, run:

```bash
mvn clean compile
mvn exec:java
```

Maven downloads the SQLite JDBC dependency on first run. The database file `campusshield.db` is created in the project working directory.

## Project structure
```text
CampusShield/
├── pom.xml
├── README.md
└── src/main/java/com/campusshield/
    ├── CampusShieldApp.java
    ├── User.java
    ├── AuthenticationException.java
    ├── ScannerStrategy.java
    ├── AbstractScanner.java
    ├── UrlScanner.java
    ├── MessageScanner.java
    ├── ScanResult.java
    ├── InvalidScanInputException.java
    ├── ScanHistoryRepository.java
    └── JdbcScanHistoryRepository.java
```

## Test cases
| Input | Expected behaviour |
|---|---|
| `https://www.example.com` | Usually SAFE under the implemented rules |
| `http://192.168.1.10/login` | Risk increases due to HTTP, IP host and login keyword |
| `https://secure-example.com/verify` | Risk increases due to keyword and hyphen rules |
| `Congratulations! You won a prize. Verify your account immediately: http://example.com` | High risk due to multiple scam indicators |
| Empty input | Validation message is shown |

## Rubric mapping
- OOP (inheritance, polymorphism, interface, encapsulation): `ScannerStrategy`, `AbstractScanner`, `UrlScanner`, `MessageScanner`, `ScanResult`, `User`
- Collections & Generics: `List<ScanResult>`, `List<String>`, `List<String[]>`
- Multithreading & synchronization: `ExecutorService`, `SwingUtilities.invokeLater`, synchronized list and synchronized JDBC repository methods
- Database operations & JDBC: `JdbcScanHistoryRepository`, SQLite table, prepared statements and result sets

## Limitations and responsible use
This is an educational prototype using simple patterns, not a production anti-phishing engine. It does not query live threat-intelligence feeds, verify domain ownership, inspect website content, or decode QR codes. A low score does **not** prove a URL or message is safe. Do not enter real passwords, OTPs or private information. The demo login credentials are hard-coded and must not be used for real accounts.
