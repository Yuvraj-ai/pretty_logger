# Pretty Logger

A colorful, feature-rich Python logging utility with automatic file/line detection, daily log rotation, and console color coding.

## Features

- 🎨 **Color-coded console output** by log level
- 📁 **Automatic file & line number detection** - no need to specify logger name
- 📅 **Daily log rotation** - creates new log files automatically
- 🗑️ **Auto cleanup** - removes old logs after configurable days
- 📝 **Exception tracebacks** - full stack traces with `logger.exception()`

## Color Scheme

| Level    | Color         |
|----------|---------------|
| DEBUG    | Cyan          |
| INFO     | Green         |
| WARNING  | Yellow        |
| ERROR    | Red           |
| CRITICAL | Bold Magenta  |
| Date     | Yellow        |
| Location | Gray          |

## Installation

Simply copy `pretty_logger.py` to your project directory.

## Quick Start

```python
from pretty_logger import get_logger

logger = get_logger()

logger.info("Application started")
logger.debug("Debug information")
logger.warning("Something to watch out for")
logger.error("Something went wrong")
logger.critical("System failure!")
```

## Output Example

### Console (Colored)
```
2026-02-04 23:00:44 [app.py:5] INFO     - Application started
2026-02-04 23:00:44 [app.py:6] DEBUG    - Debug information
2026-02-04 23:00:44 [app.py:7] WARNING  - Something to watch out for
2026-02-04 23:00:44 [app.py:8] ERROR    - Something went wrong
2026-02-04 23:00:44 [app.py:9] CRITICAL - System failure!
```

### Log File (`logs/applog.log`)
```
2026-02-04 23:00:44 [app.py:5] INFO     - Application started
2026-02-04 23:00:44 [app.py:6] DEBUG    - Debug information
...
```

## Configuration Options

```python
from pretty_logger import get_logger

# Basic usage - uses defaults
logger = get_logger()

# Custom log directory
logger = get_logger(log_dir="my_logs")

# Custom retention period (keep logs for 7 days instead of 30)
logger = get_logger(backup_count=7)

# Both options
logger = get_logger(log_dir="my_logs", backup_count=7)
```

### Parameters

| Parameter     | Default | Description                              |
|---------------|---------|------------------------------------------|
| `log_dir`     | `logs`  | Directory to store log files             |
| `backup_count`| `30`    | Number of days to keep old log files     |

## Logging Exceptions

Use `logger.exception()` inside an `except` block to log the full stack trace:

```python
try:
    result = 1 / 0
except Exception:
    logger.exception("Division failed!")
```

Output:
```
2026-02-04 23:00:44 [app.py:5] ERROR    - Division failed!
Traceback (most recent call last):
  File "app.py", line 3, in <module>
    result = 1 / 0
ZeroDivisionError: division by zero
```

## Log File Structure

```
your_project/
├── pretty_logger.py
├── your_app.py
└── logs/
    ├── applog.log              # Current day's log
    ├── applog.log.2026-02-03   # Yesterday's log
    ├── applog.log.2026-02-02   # Day before
    └── ...
```

- Logs rotate automatically at midnight
- Old logs are deleted after `backup_count` days

## Using in Multiple Files

Each file gets its own logger that shows its filename:

**main.py**
```python
from pretty_logger import get_logger
logger = get_logger()

logger.info("Starting main")  # Shows [main.py:4]
```

**utils.py**
```python
from pretty_logger import get_logger
logger = get_logger()

def helper():
    logger.info("Helper called")  # Shows [utils.py:5]
```

All logs go to the same `logs/applog.log` file with their source location.

## Requirements

- Python 3.6+
- No external dependencies (uses only standard library)

## License

MIT License - Feel free to use and modify!
