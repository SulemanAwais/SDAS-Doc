---
sidebar_position: 1
---

# Mobile App 
The mobile application is developed in [Android](https://developer.android.com/)

## Sensor Data Acquiring :
- It retreives the data of listed sensors of the mobile device i.e., Accelerometer etc.
- Timestamps are also recorded here
- It takes input from the user about IP Address*
- It shows the data of sensors of smartphone. 
## How to access the data ?

This sensor returns multi-dimensional array of sensor values for each `SensorEvent`. For example, during a single sensor event the accelerometer returns acceleration force data for the three coordinate axes. These data values are returned in a `float` array (`values`) along with other `SensorEvent` parameters.


### SensorEventListener
First implement the **SensorEventListener** class in your java file and create instences of **SensorManager** and **Sensor**.SensorManager lets you access the device's sensors


```jsx title="SensorActivity.java" {6,7,8}showLineNumbers
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;

public class SensorActivity extends Activity implements SensorEventListener {
    private SensorManager sensorManager;
    private Sensor accelerometer;

```
### TYPE_ACCELEROMETER:
Now the data coming from accelerometer can be accessed using SensorManager.
```jsx title="SensorActivity.java"

sensorManager = (SensorManager) getSystemService(Context.SENSOR_SERVICE);
accelerometer = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);

```

When any motion is detected in the smartphone, the accelerometer will detect change in acceleration and will return three values:
- values[0]: Acceleration on the x-axis
- values[1]: Acceleration on the y-axis
- values[2]: Acceleration on the z-axis
Any of these values can be accessed with the instance of SensorEvent.

```jsx title="SensorActivity.java"
public final void onSensorChanged(SensorEvent event) {
        float x_axis = event.values[0];
        txt.setText(String.valueOf(x_axis));
    }

```
## Data Sending :
**sendData()** method is invoked here and HTTP request is generated which sends the acquired data to the given IP address

``` jsx title="SensorActivity.java" showLineNumbers
public void sendData() {
        try {
            String url = "http://192.168.10.11:5000/sensors";;
            StringRequest request = new StringRequest(Request.Method.POST,url,
                    response -> Toast.makeText(this, "Success", Toast.LENGTH_SHORT).show(),
                    error -> Toast.makeText(this, "Error", Toast.LENGTH_SHORT).show())
```
 ### Detailed Explanation:
  
The code starts by importing various required packages such as android.annotation.SuppressLint, android.hardware.Sensor, android.hardware.SensorEvent, android.hardware.SensorEventListener, android.hardware.SensorManager, android.os.Bundle, android.widget.Button, android.widget.TextView, and android.widget.Toast. The code also imports various Volley packages for handling HTTP requests.

The class **MainActivity** extends AppCompatActivity and implements the SensorEventListener interface. This class contains various instance variables such as SensorManager object, List **Sensor** object, RequestQueue object, and various TextView objects to display the values of each sensor. The class also contains various float variables to store the values of each sensor.

The onCreate method is the first method that is called when the activity is launched. In this method, the content view of the activity is set using the setContentView method. The method then initializes the sensor manager using getSystemService method and creates a list of sensors. It checks if each of the required sensors is available and adds them to the list. It then displays the names of all sensors available in the device. The code then registers each of the sensors in the list using the registerListener method of the sensor manager.

The code then initializes various TextView objects for each sensor and sets the references to their respective XML elements. It also initializes a Button object for start and stop buttons. The startButton is used to start the sensors and the stopButton is used to stop the sensors.

The onSensorChanged method is called every time the values of the sensor change. In this method, the values of each sensor are updated and displayed in their respective TextView objects.

The code also includes methods for handling HTTP requests such as sendRequest and onResponse. These methods are used to send the sensor values to a remote server and handle the response from the server. The code includes a Toast to display a message when the data is sent to the server successfully.

## References
To learn more about the sensors in android device, please visit the detailed documentation of Android regarding [sensors](https://developer.android.com/reference/android/hardware/Sensor)