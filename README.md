# At-Home-Rubber-Ducky
Below is how you can create your own Rubber Ducky for just $3. 

## Gif Example
![HomemadeRubberDucky](https://user-images.githubusercontent.com/56332039/151614531-077adf95-5d0e-4024-a8e7-636cfa4494c1.gif)


## First thing first
This is for educational purposes ONLY! Do not use this to steal Wi-Fi passwords without permission. I am not liable for your misuse. 

### Now that that's out of the way

This is how you create your own Rubber Ducky for just $3. Hak5 is AMAZING, so please buy their stuff. If you can't afford it, here's how you can do it on your own.

### Step One: Attiny85 Micro USB

You can buy this from Amazon. A pack of 5 is around $16. https://www.amazon.com/dp/B0836WXQQR/ref=cm_sw_r_tw_dp_A5PPTYEPXT6SYT50JM02

### Step Two: Arduino Software

Attiny85 Micro USB works with Arduino. Installation is straightforward. Agree, click next, and download. 

https://www.arduino.cc/en/software

### Step Three: Configuration of Arduino

Once Arduino is installed and running, go to File > Preferences. From here, go to Additional Board Manager URLs, and copy in: http://digistump.com/package_digistump_index.json
Next, go to Tools > Board > Board Manager. Search for Digispark, and install Digistump AVR Boards.

### Step Four: Download Digistump Arduino Drivers

Go to https://github.com/digistump/DigistumpArduino/releases, and download the zip file. Unzip it, and run the Install Drivers application

### Step Five: Finally, the Payloads

Go to https://github.com/MTK911/Attiny85/tree/master/payloads, and click Wi-Fi Password Stealer. I prefer the WifiKey-Grab_Minimize-of-Shame.ino, but choose your favorite. I made slight changes to the code, increasing the delay, and adding "-Fi" to some "Wi*" portions (Example: -Path Wi* changed to -Path Wi-Fi*).

### Step Six: Webhook.site

Go to https://webhook.site and get your own personalized webhook uri. Replace https://webhook.site/<ADD-WEBHOOK-ADDRESS-HERE> with your specific address
  
### Step Seven: Now the Fun Part!
  
  From here, you want to Verify the Payload inside of Arduino, then click upload. After you click upload, plug in the Attiny85 Micro USB, and it will copy the code over. Once done, unplug the Micro USB, close Arduino, bring up your webhook.site URL, and plug back in the Attiny85 Micro USB. You will see some action, and finally, have Wi-Fi credentials in plain text. The entire process will take about 20 seconds. Enjoy!

 
