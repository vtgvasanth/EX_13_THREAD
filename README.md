# EX_13_THREAD
## AIM:
To develop a thread synchronization concept with the help of clicking the button in Android Studio.

## EQUIPMENTS REQUIRED:
Latest Version Android Studio

## ALGORITHM:
Step 1: Open Android Studio and then click on File -> New -> New project.# EX_13_THREAD
## AIM:
To develop a thread synchronization concept with the help of clicking the button in Android Studio.

## EQUIPMENTS REQUIRED:
Latest Version Android Studio

## ALGORITHM:
Step 1: Open Android Studio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next.

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display message give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:

```
Developed by: Challa Maheswar
Registeration Number : 212221040031
```


## MainActivity.java
```
package com.example.exp13;

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
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- A text view to display the count -->
    <TextView
        android:id="@+id/text_view"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="0"
        android:textSize="32sp"
        app:layout_constraintBottom_toTopOf="@+id/increment_button"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <!-- A button to increment the count -->
    <Button
        android:id="@+id/increment_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="incrementCounter"
        android:text="Increment"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
## OUTPUT

![384413860-8959ab62-39b5-4d81-b029-200b2f5ab089](https://github.com/user-attachments/assets/41bee703-6212-4879-8b00-ce8c31161c54)


## RESULT
The application is successfully displayed for thread synchronization concept with the help of clicking the button in Android Studio.




