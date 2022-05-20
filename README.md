## How to send data from ESP8266 to Qubitro using DHT11

Full step by step Tutorial Video: https://youtu.be/85RM0oG-Y1E

IoT being an integral part of cloud computing, several cloud vendors make Iinternet of Tthings (IoT) part of the services they render. Also, with the emergence of IoT, there are different platform that makes IoT implementation available even to individuals. In this tutorial, I will be taking you through steps in sending data from ESP8266, an IoT development platform to Qubitro IoT platform.
To ensure all necessary things are in place, you will have to set up your computer to communicate with NodeMCU or ESP8266 before you can follow along this tutorial.

## The Qubitro Platform
Qubitro is the fastest way to build IoT applications with predictable pricing, developer friendly features and scalability. Qubitro makes it easy to quickly monitor your devices, manage storages, all round integrations and management. To read more on the services offered by Qubitro, head over to www.qubitro.com

## The Hardware setup
# Step 1: 
The very first step is to ensure that your PC has been configured to communicate with ESP 8266. If you haven’t did this already, now is the time. Once you have configured your PC, come right back to continue following this tutorial.
# Step 2:
Connect the NodeMCU and the DHT 11 to the breadboard, depending on your model of DHT 11, it can be a 3-pin ready made model or a 4-pin model, in this tutorial, I am using a 4-pin model. If you are using a 3-pin model, connect the VCC to 3V of the NodeMCU, GND of the DHT 11 to GND on the NodeMCU and connect the data pin to Pin 4 of the NodeMCU. If it is 4-pin model you are using, connect Pin 1 of the DHT11 to 3V of the NodeMCU, connect the 10K resistor between pin 1 and pin 2 of the DHT 11, leave pin 3 of the DHT 11 sensor unconnected and connect pin 4 of the DHT 11 to GND on the NodeMCU. Connect the NodeMCU via a USB cable to your computer and you are good to go.

![image](https://user-images.githubusercontent.com/55460620/169425286-0ce81efc-67dd-44be-a6fa-e293eab2e877.png)

##  Setting up Qubitro
# Step 3:
After setting up the hardware, we need to configure and set up Qubitro to receive data from our device, to access the Qubitro portal, head over to www.qubitro.com, there you will be presented with Qubitro homepage, here you can read more on Qubitro services, the documentation and API supports. Qubitro supports different connectivity protocols, we shall be looking at them later, a heads up, we will be using MQTT protocol for this tutorial.


![image](https://user-images.githubusercontent.com/55460620/169425324-52faacba-b23d-4b61-ba23-531b403fd196.png)

Step 4: To be able to access Qubitro developement dshboard, we need to login into the Qubitro portal, on the Qubitro homepage, click on Go to portal at the top right hand corner. If you do not have an account, you will be prompted to create one and if you are a returning user just sign in into your account.

![image](https://user-images.githubusercontent.com/55460620/169425442-37a9504b-3658-48f1-ae40-fb227b468b73.png)

 
After signing in, you will be presented with the Qubitro main interface where we can see all projects created. The left hand pannel contains contains all controls regarding our projects, Creating a new project, Monitoring, documentation, uage and billing etc. What we want to do is to create a new project and new devices inside this project that will link to our actual hardware.
Step 5: To create a new project, click on New Project, and you will be directed to fill in the project name and project description. Give your project a name and a better description that matches your project requirements. After filling in the two, click on Create Project.

![image](https://user-images.githubusercontent.com/55460620/169425483-31e09bce-1055-4ad6-b05a-e3b046a7117a.png)

# Step 6: 
After successfully creating a project, you will need to choose a connectivity method between your actual device and Qubitro platform. Various options are available to choose from: MQTT, HTTP, The things stack, Golioth, actility etc. Since we are using ESP8266 in this tutorial, the best option for us is the MQTT therefore select MQTT an click on Continue.

![image](https://user-images.githubusercontent.com/55460620/169425544-e8216279-c32c-44f5-b0a0-1a1543ec1933.png)

# Step 7: 
Immediately, we will be asked to set up our devices, devices are different from project in that each device will be mapped to one actual IoT device therefore, our ptojects can contain more than one devide depending on the number of actual IoT device we are considering. Give your Device a name and also set the description, device brand can be anything depending on your brand name and device model can be your IoT device model name. After filling in the details, click on Continue.

![image](https://user-images.githubusercontent.com/55460620/169425587-90e1f20e-9f81-449a-979e-8d49e8dc9adf.png)

After clicking continue, we will be presented with the neccessary credentials we need to connect our device to Qubitro. We will be copying this later into our code later, for now, click on Continue, I’ll do this later.

![image](https://user-images.githubusercontent.com/55460620/169425603-7b478346-f49d-4894-bc21-d4c34ec5f615.png)

With this, we are done setting up our Project and assigning a device to it. Under project settings, we can found settings on project ID, project name and also option to delete the project. 
To access our device data, analytis and rules, click on Devices.

![image](https://user-images.githubusercontent.com/55460620/169425629-5c73a39d-d9c3-4285-bd6f-e811a12d44d1.png)

![image](https://user-images.githubusercontent.com/55460620/169425643-ca265bc0-24bf-4b39-aa46-70e160289cc6.png)

Under the device settings, we can see our device credentials, Device ID and Device Token. You can copy this since we will be using these in writing our code. I will like to point out that unlike some other IoT platforms where you can create your dashboard widgets alongside your project, for Qubitro, you have to first send data to Qubitro before you can create the widgets this is to enable Qubitro automatically assign telemetries to the widgets.

##  Writing the code

![image](https://user-images.githubusercontent.com/55460620/169425689-643f7041-2462-4749-85ff-3867796d0cc5.png)

A snapshot of the code is shown in the image above, to successfully compile the code, we need to grab the Qubitromqttclient library from Arduino IDE library manager. Head over to tools > manage libraries and download QubitromqttClient library

![image](https://user-images.githubusercontent.com/55460620/169425705-29c14e11-3fac-45e1-9244-558b71c29bb0.png)

Type in your network SSID and Password, paste the DeviceID and Device token copied from Qubitro device settings to the arduino code, the link to the code: 
Go though the code and you will be able to edit the data being sent to Qubitro, for this tutorial, I am sending DHT 11 data which are temperature and humidity.

![image](https://user-images.githubusercontent.com/55460620/169425747-ba0b8168-7812-4c1a-92dc-514151780870.png)

After filling in all neccessary details and editing the code according to your need, compile and upload the code on the ESP8266.  After done uploading, open the serial monitor to see the device behavior.

![image](https://user-images.githubusercontent.com/55460620/169425768-b7583e56-ce03-40c7-adb0-c82c2024086f.png)

##  Setting up our Dashboard
# Step 8: 
After successfully sending data to Qubitro, we can now setup our dashboard, go back to Qubitro and we will set up our widgets. If we go to data tab on our device, we will see that data has been received from our IoT device.

![image](https://user-images.githubusercontent.com/55460620/169425788-3ce24b13-a3d6-4bfd-9e28-9f9c170d339c.png)

To set up our dashboard, navigate to Monitoring and click on New Dashboard, give your dashboard a name, this should be according to your device for easy identification. Click on Add Widget and fill out the neccessary information according to your project, create all the needed widgets for all your telemetries. Select your widget type according to your data and you are done creating your widget.


![image](https://user-images.githubusercontent.com/55460620/169425798-e82eaef6-3251-42a6-97f9-6436351fe801.png)

![image](https://user-images.githubusercontent.com/55460620/169425807-6b595af6-bd05-42bb-9908-5b1519c4fc1f.png)

 
![image](https://user-images.githubusercontent.com/55460620/169425862-577feac6-9c7e-413e-9c8a-b476779a0b3f.png)


![image](https://user-images.githubusercontent.com/55460620/169425873-d730ee04-6904-4e46-8092-c9b218bc51a4.png)

With this we are done setting up Qubitro to receive data from ESP8266.

Full step by step Tutorial Video: https://youtu.be/85RM0oG-Y1E
 





