# Design considerations

The Wifisensor Android test application collects Wifi network readings whether the app is in Foreground or Background.
These readings are done using the WifiManager class. We had a choice between using:
- a WifiManager.ScanResultsCallback that would listen to network changes.
- a repeating alarm that will get readings every X number of milliseconds.
We opted for the later as the requirements specified that periodic readings were necessary. This approach also provides better tracking of the network environment state.
The design pattern we opted for is MVVM as recommended by Google for Android development.
Permissions are handled on the UI layer along with starting or stopping the background service.
Data collection is done by using a Handler class that gets triggered (via a BroadcastReceiver) every X number of milliseconds and sent to the backend via the Repository. Note that we did not implement a caching mechanism as the focus was to send data to the backend.

# Using the Application

After granting required permissions, the user will have to click on the **Start readings** to start data collection service. After a couple of seconds, the first readings will appear in the App and in the notification tray. When the app is closed, a notification will show every time a new reading is sent to the backend.
To stop the service, open the app and click on **Stop readings**.

# Automated Testing
Testing for this project is done using Github Actions.
We setup the repository to run tests every time a code is pushed to the main branch. Alternatively you can manually start the process by clicking on the Actions tab in Github and starting the Workflow by clicking on Re-run jobs.
Alternatively, you can use Android Studio to run the tests in the terminal: 

On Windows:
``` gradlew connectedAndroidTest ```

On Linux/MacOS
``` ./gradlew connectedAndroidTest ```

Make sure that a device is plugged-in or that an emulator is running before starting this task.



 




