This module implements a python `logging` formatter which produces well-formed RFC5424-compatible Syslog messages to a given socket.

## Usage

If you're configuring your loggers from code, you should use this formatter as below:

```python
import logging
import logging.handlers
from syslog_rfc5424_formatter import RFC5424Formatter


def set_up_logging():
    h = logging.handlers.SysLogHandler('/path/to/syslog_socket')
    h.setFormatter(RFC5424Formatter())
    logging.getLogger('').addHandler(h)
```


If you're using a more modern combination of a JSON/YAML config file and `logging.dictConfig`, your config file should look like the following (assuming YAML concrete syntax):

```yaml
formatters:
    syslog:
        (): syslog_rfc5424_formatter.RFC5424Formatter

handlers:
    syslog:
        formatter: syslog
        class: logging.handlers.SysLogHandler
        address: "/path/to/syslog/socket"
        facility: "ext://logging.handlers.SysLogHandler.LOG_USER"

root:
    level: INFO
    handlers:
        - syslog
```

## License

This work is licensed under the ISC license, the text of which can be found at [LICENSE.txt](LICENSE.txt).