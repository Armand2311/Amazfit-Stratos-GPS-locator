# Android Wear Amazfit GPS Direction Finder & GPX reader
Simple &amp; effective GPS locator app for Amazfit Xiaomi android wear
------------------------------------------------------------------------------
Hello guys, after a long work and first experience with Android Studio, here is my third version of my simple GPS locator for Wear Android.
This app was tested on my Xiaomi Amazfit Stratos 2, on PACE... (but must be fine on many others !).
This app was designed with the idea of doing like a Golf Gps wear.
The second version allows you to :
- select a GPX file from your gpsdata directory,
- select a Waypoint and track the distance/direction/altitude (the compass follow the North or not)
- store your local position on a GPX file
- remove a waypoint from your GPX file.
- just to track a return direction to your start point (without GPX)...
- automatic suggestion of the next nearest GPX waypoint (the next Golf hole ?).

The last third version includes :
- many fix and checks in gpx files handling,
- little graphics animations, hour added in the radar screen.
- checkbox to enable or not to list the (gpx) waypoints by the distance (nearest point first) or not (in initial gpx order).

- a new CARTO screen displaying the waypoints and the actual position (white circle).
The altitude is also displayed with colors. Blue is for the deepest points, and red for the hightest points of the track.
Just tap on the screen, to switch beetween Radar & Carto. It ' s also possible to zoom in & out and to swipe the map.
When in magnetic compass mode, the map is turning !

Here's the first gps startup screen. This animation just appear for 15 seconds showing the number of satellites in view.

<center><img src="/1-startscreen.jpg" alt="gps startup fix"/></center>

The main menu appears even if the position is not ok. So it's possible to change the settings, or to find and select a waypoint to track.
From up left to right : first button start the settings, the second is for select a Gps waypoint from a gpx file.
Third (bottom) is to exit, and the arrow is to start the tracking radar. Storing the current position or not.

<center><img src="/2-main-screen.jpg" alt="gps main menu"/></center>

When you click on select waypoint, the listview shows all gpx points sorted by the distance to your position.
A 'Long Click' on a point allows you to remove the point. A 'simple click' select your destination.

<center><img src="/3-wpt-liste.jpg" alt="liste waypoint gps menu"/></center>

In radar operation - the time & distance & altitude are displayed on the center - the compass and direction rotates when you move.

<center><img src="/5-scann.jpg" alt="gps radar stratos 2"/></center>

The settings view, allows to change the gpx file.
To enable or not, the magnetic sensor and compass mooving (not good for the battery!).
To enable or not the automatic waypoint suggestion.
To sort the waypoints with the distance to actual position or not.

<center><img src="/4-settings.jpg" alt="gps radar stratos 2"/></center>

The settings view, allows to change the gpx file.
To enable or not, the magnetic sensor and compass mooving (not good for the battery!).
To enable or not the automatic waypoint suggestion.
To sort the waypoints with the distance to actual position or not.

And two examples of the map display. On left a sport run track with many waypoints recorded by the Wear. It is still possible to zoom in untill you see each points. On the right a simple gpx file with some golf holes. The zoom map scale is displayed on the + / - zoom buttons.

<center><img src="/6-carto2.jpg" alt="gps carto stratos"/></center>

How this workss
--------------
The first activity launches a service who assumes the background task of getting GPS location (with a locationManager and locationListener). This avoid to stop and re-run the gps updates between each activities, and assures that just ONE first fix delay is necessary when you start the app.
The lat & long are broadcasted to the other activities with 'sendBroadcast & broadcastReceiver'.
The first screen uses a 'nmealistener' to get & display a snapshot of the $GPGSV & GPGGA frames.
The location service and its broadcats is only stopped, when the app is destroyed (if not - your battery don't last so long)...
We use the 'magnetic orientation sensor type3' to rotate the compass graduations and map, with a sensorManager.registerListener.

Change log
----------
30/4/2020 First upload v1.

1/5/2020  Location & NMEA broadcasted in the same manner by Locservice. Many checks to do.
          Important Fix !!! Impossible to kill the entire process (sinking the battery). No explication. Find a solution with ' android.os.Process.killProcess(android.os.Process.myPid());' in OnDestroy().
          RMC speed added on the scan screen.
         
14/5/2020  Version 2 , with GPX file compatibility, and 'autonext' waypoint detection.

24/05/2020 Version 3 - many fix & Map
