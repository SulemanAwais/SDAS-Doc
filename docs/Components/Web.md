---
sidebar_position: 4
---

# Web Application

The website is developed using the [Flask](https://flask.palletsprojects.com/en/2.2.x/) web framework. The code implements a [REST-API](https://aws.amazon.com/what-is/restful-api/)  to receive sensor data, store the data in memory, and write the data to files when the recording is stopped. 
Following is the role of this website:
- It takes a number of iterations and the activity name that is to be performed.
- It displays the real-time graphs of the received data using [chart.js](https://www.chartjs.org/docs/latest/)
- It has start and stop buttons which start receiving the data and plotting it and upon pressing the stop button it stores data in CSV
- A custom API is also made


## Flask API

The following are the main components and technologies used:

### Libraries

- **Flask:**A lightweight Python web framework that allows you to create web applications quickly and easily.

- **Flask-CORS:** A Flask extension that allows for cross-origin resource sharing, which allows resources to be requested from a different domain than the one that served the original request.

- **datetime**: A Python module that provides classes for working with dates and times.

- **csv:** A Python module that provides functionality for reading and writing CSV (Comma Separated Values) files.

- **os:** A Python module that provides a way of using operating system dependent functionality, such as reading and writing files, creating and removing directories, etc.

### EndPoints
The code sets up a Flask application and enables CORS for it. It then defines several endpoint functions that can be accessed via HTTP requests. These functions include:

- `hello()`: A GET endpoint that returns a simple HTML page.

- `sensors():` A POST endpoint that receives sensor data in JSON format, converts it to a list, and stores it in memory.

- `startRecord()`: A GET endpoint that sets a flag indicating that the sensor data should be saved.

- `stopRecord()`: A GET endpoint that stops the recording of sensor data and writes the data to files.

- `getData()`: A GET endpoint that returns the next item of sensor data stored in memory.

The code also defines a function,` SaveDataInCSV()`, that writes the sensor data stored in memory to multiple CSV files. The data is written to a directory that is created using the current date and time, and the name of the activity being recorded.


## Detailed Explanation

A Flask application is initialized with the following code:

 ```jsx title="app.py" showLineNumbers

app = Flask(_name_)
CORS(app)
```

## Global Variables:
The following global variables are defined in the code:
- `save_data`: A flag to indicate whether data collection is in progress or not
- `activityName`: The name of the activity being performed
- `examples`: The number of examples recorded
- `count`: A counter
- `dataQueue`: A queue to store the incoming data from the sensors
Accelerometer, Gyroscope, Magnetometer, LinearAcceleration, Gravity: Lists to store data from different sensors
## Route Definitions:
The following routes are defined in the code:
- `/`: handles GET requests and returns an HTML page rendered by the `render_template()` function.
- `/sensors`: A POST route to receive sensor data and adds sensor data to the `dataQueue` list.
- `/startRecord`: A GET route to start data collection adds "start" to the `recordingQueue` list.
- `/stopRecord`: A GET route to stop data collection and removes the first element of the `recordingQueue` list, saves the collected sensor data in CSV files, and clears the data lists.
- `/getData`: handles GET requests and returns the first element of the `dataQueue` list.

## Extracting data
`addData()` is used to extract the sensor data from the JSON request and add it to different data lists.
An empty list is initialized for each sensor and data of respective sensor is append to the the list.

``` jsx title="app.py" showLineNumbers
    acc = []
    acc.append(data[0])
    acc.append(data[1])
    acc.append(data[2])
    acc.append(data[15])
    Accelerometer.append(acc)
```
Following are the values of every index:
- data[0] will be having x-axis
- data[1] will be having y-axis
- data[2] will be having z-axis
- data[15] will be having the timestamp

## Saving Data
`SaveDataInCSV()` function creates folders for the activity and the example and saves the collected data in CSV files agains every sensor. 

```jsx title="app.py" showLineNumbers
 path = "Data/" + activityName + "/" + date
fileNames = ["Accelerometer", "GyroScope", "Magnetometer", "LinearAccelerometer", "Gravity"]
with open(path + "/" + fileNames[0] + ".csv", 'a') as csvfile:
        csvwriter = csv.writer(csvfile) //creating a csv writer object
        csvwriter.writerows(Accelerometer) //write all the data in the list to the csv file
        print("Document Inserted")
    csvfile.close()

```

Then the code checks if the script is running as the main program, and if so, it calls the run() method of the Flask application to start the web server.
