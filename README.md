
# Toto Logger

This library standardizes the way that toto microservices will log information.

Logs in toto have the following structure:
```
> [correlationID] - [logType] - [logLevel] - Message
```
Where:
* `correlationID`   should be always present for apis and reactive microservices and is the identifier that can be used to track the flow of data through sync and async calls
* `logType`         is the type of log. The following log types are accepted:
   * `api-in`    - **reserved** - to be used only when receiving an API call. This log type **must** be used **only once** and only **at the moment the API call is received**: it shouldn't be used for subsequent log entries. It is only used to **record the fact that an API call has been received**!
   * `api-out`   - **reserved** - to be used only when making an outbound API call.
   * `event-in`  - **reserved** - to be used only when receiving an Event. Same logic applies as for the `api-*` log type.
   * `event-out` - **reserved** - to be used only when publishing an Event. Same logic applies as for the `api-*` log type.
   * `compute`   - can be used for any log happening during the computation that results from the receiving an event or an api call.
* `logLevel`        is the level of the log. Should only be:
   * `debug`    - only used for debugging purposes
   * `info`     - used for standard info logging
   * `warn`     - used to log warnings
   * `error`    - used to log errors

## How to use it
Instantiate it:
```
from toto_logger.logger import TotoLogger

logger = TotoLogger()
```

Log, based on the type of log
```
logger.api_in(correlation_id, method, path);
logger.api_out(correlation_id, microservice, method, path);
logger.event_in(correlation_id, topic);
logger.event_out(correlation_id, topic);
logger.compute(correlation_id, message, log_level);

```
