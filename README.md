# Ex_No_11_Thread-Synchronization
Develop a program to perform Thread Synchronization using Android Studio
## AIM:
To Develop a program to perform Thread Synchronization using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)


## ALGORITHM:
Step 1: Open Android Studio and then click on File -> New -> New project.

Step 2: Then type the Application name as SMSIntent and click Next.

Step 3: Select the Minimum SDK below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally, click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Thread Synchronization processing is done in MainActivity.java

Step 7: Save and run the application.


## Program:
 ```
/*
Program to create an Option Menu
Developed by: shyamnaveen raj M
RegisterNumber:  212221230099
*/
```

## MainActivity.java:

```
package com.example.threadsyn;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Bundle;
import android.os.Handler;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.concurrent.Semaphore;
public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MainActivity";

    // Object used for synchronizing access to counter
    private static final Object lock = new Object();

    // Maximum number of concurrent threads
    // that can access the counter
    private static final int MAX_THREADS = 5;

    // Semaphore to limit concurrent access to the counter
    private static final Semaphore semaphore = new Semaphore(MAX_THREADS);

    // Counter to store the
    // number of button clicks
    private int counter = 0;

    // Reference to the text view to
    // display the number of button clicks
    private TextView textView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.text_view);
    }
    public void incrementCounter(View view) {
        // Start a new thread to increment the counter
        new Thread(() -> {
            try {
                // Acquire the semaphore
                semaphore.acquire();
                // Synchronized block to update the counter
                synchronized (lock) {
                    counter++;
                }
            } catch (InterruptedException e) {
                // Log an error if the thread is interrupted
                Log.e(TAG, "Thread interrupted", e);
            } finally {
                // Release the semaphore
                semaphore.release();
            }
            // Update the text view on the main thread
            updateTextView();
        }).start();
    }

    // Method to update the text view on the main thread
    private void updateTextView() {
        // Post the update to the main thread's message queue
        new Handler(getMainLooper()).post(() -> textView.setText(String.valueOf(counter)));
    }

}


```

## activity_main.xml:
```
package com.example.threadsyn;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Bundle;
import android.os.Handler;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.concurrent.Semaphore;
public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MainActivity";

    // Object used for synchronizing access to counter
    private static final Object lock = new Object();

    // Maximum number of concurrent threads
    // that can access the counter
    private static final int MAX_THREADS = 5;

    // Semaphore to limit concurrent access to the counter
    private static final Semaphore semaphore = new Semaphore(MAX_THREADS);

    // Counter to store the
    // number of button clicks
    private int counter = 0;

    // Reference to the text view to
    // display the number of button clicks
    private TextView textView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.text_view);
    }
    public void incrementCounter(View view) {
        // Start a new thread to increment the counter
        new Thread(() -> {
            try {
                // Acquire the semaphore
                semaphore.acquire();
                // Synchronized block to update the counter
                synchronized (lock) {
                    counter++;
                }
            } catch (InterruptedException e) {
                // Log an error if the thread is interrupted
                Log.e(TAG, "Thread interrupted", e);
            } finally {
                // Release the semaphore
                semaphore.release();
            }
            // Update the text view on the main thread
            updateTextView();
        }).start();
    }

    // Method to update the text view on the main thread
    private void updateTextView() {
        // Post the update to the main thread's message queue
        new Handler(getMainLooper()).post(() -> textView.setText(String.valueOf(counter)));
    }

}
```


## AndroidMainfest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.Threadsyn"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
## Output

![output](https://github.com/jithendra2004/Ex_No_11_Thread-Synchronization/blob/main/j11%201.png)

![output](https://github.com/jithendra2004/Ex_No_11_Thread-Synchronization/blob/main/j11%202.png)


## Result:
Thus a Simple Android Application to create an Thread synchronization using Android Studio was developed and executed successfully.
