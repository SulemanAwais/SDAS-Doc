---
sidebar_position: 5
---

# Backend Server 
The server of this system is build using [Python](https://www.python.org/) which is a high-level, interpreted programming language known for its simplicity, readability, and versatility. Python emphasizes code readability and uses a clean and easy-to-understand syntax, making it suitable for beginners and experienced developers alike. 

## Working:
- **User Input**: It prompts the user to enter a URL, username, activity name, and the number of examples.
- **API Interaction:** It uses the requests library to send HTTP requests to the specified API URL.
- **Set Record:** It sends a POST request to the API to set the record, providing the username, activity name, and number of examples as JSON data.
- **Start Recording:** It sends GET requests to the API to initiate the recording process for each example. It waits for 5 seconds between each start request.
- **Stop Recording:** It sends GET requests to the API to stop the recording process for each example. It waits for 5 seconds between each stop request.
- **Get Data:** It sends a GET request to the API to retrieve the recorded data for each example.
- **Data Processing:** It processes the retrieved data by converting the string representation into a list of floats using the strToList() function.
- **Data Saving:** It saves the processed data into CSV files based on different sensor categories (e.g., accelerometer, gyroscope) and example numbers.
- **Data Clearing:** It sends a GET request to the API to clear the data queue.
- **Processing Completed:** It displays a message indicating the completion of each example's processing.

## Sub modules: 
**Importing Libraries:** The code imports necessary libraries such as requests, `csv`, `time`, `os`, and `IPython.display.Audio` for making HTTP requests, working with CSV files, handling time-related operations, managing directories, and audio playback.

**User Input:** The code prompts the user to enter a URL, username, activity name, and number of examples.

**API URL Setup:** The code constructs the API URL by appending the provided URL with the necessary endpoint path.

**Set Record:** The code sends a POST request to the server's API URL with the user's input data (username, activity name, and examples) to set the record. The response from the server is printed.

**Initialization:** The code initializes empty lists for `startList`, `stopList`, and `activitiesQueue` to store timestamps and data.

**String to List Conversion:** The code defines a helper function, `strToList`, which converts a string representation of data into a list of floats. It splits the string, removes curly braces and converts the values into floats.

**CSV Data Saving:** The code defines the `saveCsv` function, which takes data, user, activity, and example number as input. It organizes the data into separate lists based on different sensor types (Accelerometer, GyroScope, Magnetometer, LinearAccelerometer, Gravity). It creates directories if they don't exist and saves each sensor data into separate CSV files.

**Data Processing:** The code defines the `processData` function to process the collected data. It iterates over the `activitiesQueue` and converts each data string to a list using `strToList`. The processed data is then saved into CSV format using the `saveCsv` function.

**Example Iteration:** The code clears the `activitiesQueue` list and starts a loop for the specified number of examples. For each example, it waits for 5 seconds, sends a request to start recording, waits for another 5 seconds, sends a request to stop recording, retrieves the recorded data, clears the server's data queue, and appends the data to the activitiesQueue list.

**Data Processing:** Finally, the code calls the `processData` function to process the collected data.
