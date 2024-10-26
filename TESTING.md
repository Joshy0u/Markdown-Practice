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

**NOTE**: You can either write the mock code in *python file(send_data.py)* or in the *test-json file*.

 Metrics is a list, therefore you have the option to write multiple data entries and send it as send_data.py,make sure to seperate data by comma.

Session data is not in a list, thereofre only one of each can be sent, no commas. however you have 3 models that pydantic will verify for you prior to sending(if you come accross an error, then make sure your following the appropriate schema since session has 3 models to follow).

```json
{
    "event": {
        "event_type": "event_type_value",  // Type of the event (e.g., "metrics")
        "data": [
            {
                "time": "time_placeholder",   // Unix timestamp (e.g., 1672839482.123)
                "sensor_id": "sensor_id_placeholder",  // Unique sensor identifier
                "data": "data_value_placeholder"  // Numeric data from the sensor
            }
        ]
    }
}