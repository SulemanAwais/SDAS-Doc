---
sidebar_position: 2
---

# Website

The website is developed using the [Flask](https://flask.palletsprojects.com/en/2.2.x/) web framework. The code implements a [REST-API](https://aws.amazon.com/what-is/restful-api/)  to receive sensor data, store the data in memory, and write the data to files when the recording is stopped.

## Sub-modules

The following are the main components and technologies used in this code:

- **Flask:**A lightweight Python web framework that allows you to create web applications quickly and easily.

- **Flask-CORS:** A Flask extension that allows for cross-origin resource sharing, which allows resources to be requested from a different domain than the one that served the original request.

- **datetime**: A Python module that provides classes for working with dates and times.

- **csv:** A Python module that provides functionality for reading and writing CSV (Comma Separated Values) files.

- **os:** A Python module that provides a way of using operating system dependent functionality, such as reading and writing files, creating and removing directories, etc.

The code sets up a Flask application and enables CORS for it. It then defines several endpoint functions that can be accessed via HTTP requests. These functions include:

- hello(): A GET endpoint that returns a simple HTML page.

- sensors(): A POST endpoint that receives sensor data in JSON format, converts it to a list, and stores it in memory.

- startRecord(): A GET endpoint that sets a flag indicating that the sensor data should be saved.

- stopRecord(): A GET endpoint that stops the recording of sensor data and writes the data to files.

- getData(): A GET endpoint that returns the next item of sensor data stored in memory.

The code also defines a function, **SaveDataInCSV()**, that writes the sensor data stored in memory to multiple CSV files. The data is written to a directory that is created using the current date and time, and the name of the activity being recorded.

Finally, the code checks if the script is being run as the main program and starts the Flask application if that is the case.







- It takes number of iterations and the activity name that is to be performed.
- It displays the real-time graphs of the received data.
- It has start and stop buttons which starts receiving the data and plotting it and upon pressing the stop button it stores data in csv
- It uses flask for backend
- A custom API is also made


## Detailed Explanation


### Importing Libraries:
The following libraries are imported in the code:
- datetime: To work with dates and times
- Flask: To build the web application
- Flask_Cors: To handle Cross-Origin Resource Sharing (CORS)
- csv: To work with CSV files
- os: To handle file operations
- Application Initialization:

A Flask application is initialized with the following code:

 ```jsx title="App.py"

app = Flask(_name_)
CORS(app)
```

### Global Variables:
The following global variables are defined in the code:
- save_data: A flag to indicate whether data collection is in progress or not
- activityName: The name of the activity being performed
- examples: The number of examples recorded
- count: A counter
- dataQueue: A queue to store the incoming data from the sensors
Accelerometer, Gyroscope, Magnetometer, LinearAcceleration, Gravity: Lists to store data from different sensors
### Route Definitions:
The following routes are defined in the code:
- /: The default route which returns the index.html file.
- /sensors: A POST route to receive sensor data and append it to the dataQueue.
- /startRecord: A GET route to start data collection.
- /stopRecord: A GET route to stop data collection and save the data to a CSV file.
- /getData: A GET route to retrieve data from the dataQueue.
### Saving Data to a CSV file:
The SaveDataInCSV() function is used to save the data to a CSV file. The function creates a folder for the activity, with a subfolder for each example recorded. The data from each sensor is saved in a separate CSV file.