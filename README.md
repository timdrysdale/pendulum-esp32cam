# pendulum-esp32cam
Pendulum experiment based around esp32cam

## Background

We want a simple experiment for sharing with new users. A blinking light is _probably_ what we want for simplicity, but ideally I'd still like something that moves about a bit.

The original design of the ppendulum experiment](https://github.com/practable/penduino) was based on a design that dangled a magnet from a thread. This saves the cost and faff of encoder. But we want a sensor of sorts, so we are probably looking at adding a second coil, orientation and size to be determined.

## Convenience for the user

Connecting up a remote lab gets exponentially harder if you bury configuration information into a microcontroller - but it appears you can use WPS with an ESP32, according to the code [here](https://github.com/espressif/arduino-esp32/blob/master/libraries/WiFi/examples/WPS/WPS.ino) So we could imagine adding a button to trigger connection to whatever wifi is offering WPS connectivity at the time. And then using a serial terminal as a back up option (e.g. add SSID and password)

Then we just need to figure out how to port the relay connection code into C++, and find a way to set the configuration information for persistent usage. It might be the case that we hardcode the connection credential into the device .... although this has the potential to be frustrating for users who want to modify the code. Having to have a computer connection over USB just to make it work seems a bit of a faff too - so perhaps we hard code an access token for 12 months (and put a QR code on the device that includes the expiry date and link to go to get a new credential).

It's likely we can use the [preferences library](https://randomnerdtutorials.com/esp32-save-data-permanently-preferences/) to store the credential.

It's also possible that a motivated user could attempt to read out this information and re-use it on another device. So we might consider whether we rate limit the video and data relay at some point to minimise and unanticipated load this would introduce. But theoretically, if someone pays for a relay account then no harm in changing which device uses it (unless we say something in our Ts&Cs for a good and fair reason which has not occurred to me just yet!).

