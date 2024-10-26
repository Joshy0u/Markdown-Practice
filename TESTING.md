### Function Usage/Debugging

Quick documentation on how to start and debug `star-stream` for future reference.

also for note, to view test data, datagrip or any SQL 
database alternative is needed(ask a lead for the postgreSQL key)

Before running any commands, start the Azurite service:

> Azurite start

## Commands

- `func start`
- `send_data.py`

---

### Mock Data Format

## metrics

**NOTE**: You can either write the mock code in *python file(send_data.py)* or in the *test-json file*.

 Metrics is a list, therefore you have the option to write multiple data entries and send it as send_data.py,make sure to seperate data by comma.

Session data is not in a list, thereofre only one of each can be sent, no commas. however you have 3 models that pydantic will verify for you prior to sending(if you come accross an error, then make sure your following the appropriate schema since session has 3 models to follow).

```json
{
    "event": {
        "event_type": "metrics",
        "data": [
            {
                "time": "datetime",   // Unix timestamp (e.g., 1672839482.123)
                "sensor_id": "int",  // Unique sensor identifier
                "data": "float"  // Numeric data from the sensor
            }
        ]
    }
}
```
**NOTE**: For testing metrics to work, you need to go into the database, locate the `sensor` table, and create a row with the following fields:

- **sensor_id**: A unique identifier for the sensor (ensure it is not a sensor already present in the table, as those are actual sensors).
- **car**: Set to a testing title, such as `"test_car"`.
- **driver**: Enter a descriptive value (optional).
- **metadata**: Add additional details as needed.

This setup ensures that when you send metric data, the sensor will work as expected.

**TO SEARCH FOR DATA**: Make sure in the "Order by" field, you use `"time DESC"` so that data is sorted by the most recent timestamp.

## session

Unlike metrics, with session, you have 2 options at the moment to write up the mockup data, either start or stop. however that data when written must be mocked up in 1 bracket and cannot add multiple within it. Make sure you follow schema otherwise the function will yell at you. 

```json
{
    "event": {
        "event_type": "session",
        "data": {
            "id": "test-2", // can be any test
            "status": "Closed", // CASE SENSITIVE
            "stop": "time.time()"
        }
    }

}