# Extensible Thread-Safe Logging Framework

This project is a simple Java-based logging framework that records application
messages and errors and writes them to different output destinations such as
console, files, or a database.  
It is designed to demonstrate clean low-level design, thread safety, and
extensibility.

---

## What This Project Does

- Accepts log messages from an application
- Filters messages based on log level (DEBUG, INFO, WARNING, ERROR, FATAL)
- Formats log messages into readable text
- Writes logs to one or more destinations at the same time
- Works safely when multiple threads log messages together

---

## Features

- Five log levels with priority-based filtering  
  (Only messages with required severity are logged)
- Multiple output destinations
  - Console logging
  - File logging
  - Database logging
- Customizable log message formatting
- Support for multiple filters (level-based, source-based)
- Thread-safe logging for concurrent applications
- Runtime configuration changes
- Easy to extend without changing existing code

---

## Core Design

The framework is built using small, focused components:

- **Logger**  
  Receives log requests from the application and coordinates the logging process.

- **LogAppender**  
  Decides where the log message is written (console, file, database).

- **LogFormatter**  
  Converts a log message into a formatted string.

- **LogFilter**  
  Decides whether a log message should be written or ignored.

- **LogMessage**  
  An immutable object that contains log details such as timestamp, level, message,
  and source.

Each component has a single responsibility, making the system easy to understand
and extend.

---

## Sample Usage

```java
Logger logger = new LoggerImpl();

// Set minimum log level
logger.setLevel(LogLevel.WARNING);

// Add output destinations
logger.addAppender(new ConsoleAppender(new SimpleFormatter()));
logger.addAppender(new FileAppender("app.log", new DetailedFormatter()));

// Log messages
logger.info("This message will not be logged");
logger.error("Payment failed for user {}", userId);
