---
title: Loggers
---

## TarnishedEngine Logger
The logger is a utility provided alongside Tengine. Its headers are in `/include/tengine/util/logger`, and source files in `/src/tengine/util/logger/`.

### Structure:

#### Logger
The main logger class is implemented as a Meyers Singleton. This allows everything to call the logger, with everything being routed to a single instance internally.

Logs consist of three things:

- Log Level: States the importance of the log. Can be `DEBUG`, `INFO`, `WARNING`, `ERROR`, or `FATAL`.
- Sender: States the sender's name.
- Message: Contents of your log message.

#### Sinks
Sinks are implementations of a virtual class, and can be registered with the logger, alongside an optional filter. Logs that pass their filter's criteria are passed to the filter.

#### Filters
Filters tell the logger what messages to send to sinks.

### Usage:
Include the logger's main header with:
```cpp
#include <tengine/util/logger/Logger.hpp>
```

Optionally, you can include a set of helpful macros with:
```cpp
#include <tengine/util/logger/LoggerMacros.hpp>
```

Get an instance of the logger, with:
```cpp
// Get an instance manually
tengine::util::logger::Logger::getInstance()

// Get an instance using a macro:
TENGINE_GET_LOGGER
```

Register a sink with:
```cpp
// If no filter is specified, m_defaultFilter (specified in /include/tengine/util/logger/Logger.hpp) is used, which lets everything through
logger.addSink(sink);
logger.addSink(sink, filter);
```

Send a log message with:
```cpp
logger.log(level, sender, msg)
TENGINE_LOG(level sender, msg)

// Alternatively, LoggerMacros.hpp provides macros with the level field set for you
TENGINE_LOG_DEBUG(sender, msg)
TENGINE_LOG_INFO(sender, msg)
TENGINE_LOG_WARN(sender, msg)
TENGINE_LOG_ERROR(sender, msg)
TENGINE_LOG_FATAL(sender, msg)
```