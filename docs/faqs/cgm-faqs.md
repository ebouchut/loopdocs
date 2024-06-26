## Which CGMs are supported by the *Loop* app?

The next release of the *Loop* app and the current [Loop-dev branch](../version/build-dev.md) includes Libre support in addition to the CGM listed below.

The *Loop* app supports G5, G6, G7, Dexcom ONE, Dexcom Share, Nightscout and the Medtronic CGM systems compatible with Looping pumps.

Libre Support (for some Libre sensors):

* [Loop dev](../version/build-dev.md) adds [LibreTransmitter](https://github.com/dabear/LibreTransmitter#libretransmitter-for-loop){: target="_blank" }
* [Loop and Learn: Customization](https://www.loopandlearn.org/custom-code){: target="_blank" }

There are more details on the [Compatible CGM](../build/cgm.md) page.

## Do I need wait for a new sensor session to start Loop?

No, you can start Looping mid-sensor session. There's no need to do anything special with regards to your CGM session when starting or ending the *Loop* app.

## What do I do when sensor is in warm-up?

The *Loop* app will stop automatically adjusting insulin when the most recent glucose value is older than 15 minutes.  This is indicated by seeing three dashes in place of the glucose reading on the HUD.

* A HUD status row message of `No Recent Glucose` is displayed, making it easier to add the fingerstick value directly in Loop, which also saves it in Apple Health

With no recent glucose readings, your pump returns to the scheduled basal delivery (within 30 min or less).

Loop continues to accept carb entries and manual bolus commands. [Manual Temp Basal](../loop-3/omnipod.md#manual-temp-basal) can also be commanded.

### Dexcom G7 Warmup

The Dexcom G7 begins warming up as soon as you insert the device and completes in less than half an hour. Many Loopers use the combination of this warmup upon insertion and the 12-hour grace period offered by the G7 to have continuous CGM readings with no gap.

* During the 12-hour grace period, start the next sensor but do not connect it to your G7 app on your Looping phone
* After waiting for the sensor to settle, stop the old sensor and connect to the new sensor
    * The G7 app will show both traces as shown in the graphic below with about 9 hours of settle time
        * The new sensor data is added to the graph along with old sensor readings
        * You cannot see the new sensor until you transition to using it

    ![overlay of 2 g7 sensors after transition to new](img/dexcom-g7-overlay.jpg){width="400"}
    {align="center"}

    * By looking at the trace overlap, you can decide how much you trust the new sensor

## What do I do when I switch Dexcom transmitters?

When you change transmitters (prior to Dexcom G7), you will need to update the transmitter ID in your *Loop*settings. The instructions for Dexcom are provided below:

* In Loop, select the `Delete CGM` button at the very bottom of the CGM info page
    * You cannot just edit the line with your old transmitter ID
* It's a good idea to go into your phone Bluetooth settings and delete the old Dexcom transmitter
    * The transmitter starts with Dexcom and ends with the last 2 characters of your old transmitter ID
    * Tap on the (i) next to `Not Connected` and select `Forget This Device`
* Follow the Dexcom instructions for pairing the new transmitter
* After pairing completes with Dexcom:
    * In Loop, add CGM and select the Dexcom system again
    * Enter the new transmitter ID
    * If you're unsure where to find your transmitter ID, see [Where to get the Transmitter ID for Dexcom G6?](../loop-3/add-cgm.md#where-to-get-the-transmitter-id-for-dexcom-g6)

![img/delete-cgm.jpg](img/delete-cgm.jpg){width="400"}
{align="center"}

If you don't update your transmitter ID when you change active transmitters, and you included your Dexcom share credentials, then the *Loop* app uses your Dexcom Share server to get your CGM data and will not work without cell or wifi connection. When the *Loop* app is using data from Dexcom Share servers, a small cloud will appear above the BG reading in the *Loop* app and should tip you off that maybe you forgot to update your transmitter ID. It's best not to enter Share Credentials. This makes it really obvious that you need to update the CGM settings in the *Loop* app at transmitter change time.

### Dexcom G7

With Dexcom G7, the *Loop* app automatically picks up the active sensor/transmitter pair from the Dexcom G7 app on the phone. Once Dexcom G7 is added to the *Loop* app as the CGM, the Looper does not need to do anything to the *Loop* app after selecting the new sensor/transmitter pair in the Dexcom G7 app.

### Dexcom G5, G6 and ONE

The diagram below illustrates the steps needed to **switch transmitters on Dexcom G5, G6, and ONE** (for the version of ONE based on G6). This typically needs to be done every three months when a new transmitter is started.

```mermaid
sequenceDiagram
    actor       user     as User
    participant dexcom   as Dexcom App
    participant loop_app as Loop App

    autonumber
    user     ->>  loop_app: Delete CGM
    user     ->>  dexcom:   Stop old Sensor
    activate      dexcom
    Note over     dexcom:   Switching sensors and transmitters... ⏱️
    user     -->> user:     Remove old Sensor and old Transmitter
    user     ->>  dexcom:   Enter/Scan new Transmitter ID
    user     ->>  dexcom:   Enter/Scan new Sensor Code
    user     -->> user:     Insert new Sensor then attach new transmitter
    user     ->>  dexcom:   Pair then Start new Sensor
    deactivate    dexcom
    dexcom   -->> user:     New Sensor warming up... 
    activate      dexcom
    Note over     dexcom:   New sensor warmup... ⏱️
    user     ->>  loop_app: Add CGM
    user     ->>  loop_app: Enter new Transmitter Serial Number
    user     ->>  loop_app: Enable Remote Upload
    dexcom   -->> user:     New Sensor operational
    deactivate dexcom
```


## Can I use Libre sensors with a reader like Miao Miao?

If you use *Loop* dev code, then any Libre sensor supported by [LibreTransmitter](https://github.com/dabear/LibreTransmitter#libretransmitter-for-loop){: target="_blank" } can be used with the *Loop* app.

See [Which CGMs are supported by the *Loop* app?](#which-cgms-are-supported-by-the-loop-app).

## Can I use Eversense?

There is a method to upload Eversense to Nightscout using an Android phone, but there is no method to read an Eversense directly with an iPhone at this time.

You can use Nightscout as a CGM with Eversense, but that requires internet access.

## Can the *Loop* app read CGM data from Nightscout?

Yes.

## What other CGM apps can be used with Loop?

If you are willing to build a development version of Loop, the dev branch incorporates [LibreTransmitter](https://github.com/dabear/LibreTransmitter/blob/main/readme.md){: target="_blank" } into the *Loop* app itself. Please read about [Loop Development](../version/development.md) before [building dev](../version/build-dev.md) and using the dev app.

You can add xDrip4iOS and GlucoseDirect as a CGM option to the *Loop* app by applying a [code customization](https://www.loopandlearn.org/custom-code){: target="_blank" }.

Please read the docs for [xDrip4iOS](https://xdrip4ios.readthedocs.io/en/latest/){: target="_blank" } and [Glucose Direct](https://github.com/creepymonster/GlucoseDirect#readme){: target="_blank" }. You must build these apps yourself to Loop; you cannot use the TestFlight pre-built versions.
