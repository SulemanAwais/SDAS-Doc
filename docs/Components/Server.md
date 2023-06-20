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

