---
sidebar_position: 1
---

# Accelerometer
The accelerometer in smartphone measures the linear acceleration of the device. When at rest position in whatever orientation, the figure represents the force of gravity active on the device at the same time it also measures the acceleration on the X and Y axis which will be zero. It detects changes in the orientation and accordingly rotates the mobile screen. Basically, it helps your smartphone know up form down.The architecture of accelerometer is always **hardware based**
<!-- Add **Markdown or React** files to `src/pages` to create a **standalone page**: -->



## How to access the data ?

This sensor returns multi-dimensional array of sensor values for each `SensorEvent`. For example, during a single sensor event the accelerometer returns acceleration force data for the three coordinate axes. These data values are returned in a `float` array (`values`) along with other `SensorEvent` parameters.


### SensorEventListener
First implement the **SensorEventListener** class in your java file and create instences of **SensorManager** and **Sensor**.SensorManager lets you access the device's sensors


```jsx title="SensorActivity.java"
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;

public class SensorActivity extends Activity implements SensorEventListener {
    private SensorManager sensorManager;
    private Sensor accelerometer;
.
.
.
}
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
<!-- A new page is now available at [http://localhost:3000/my-react-page](http://localhost:3000/my-react-page).

## Create your first Markdown Page

Create a file at `src/pages/my-markdown-page.md`:

```mdx title="src/pages/my-markdown-page.md"
# My Markdown page

This is a Markdown page
```

A new page is now available at [http://localhost:3000/my-markdown-page](http://localhost:3000/my-markdown-page).
- `src/pages/index.js` → `localhost:3000/`
- `src/pages/foo.md` → `localhost:3000/foo`
- `src/pages/foo/bar.js` → `localhost:3000/foo/bar` -->