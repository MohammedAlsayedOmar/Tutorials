# Setup Android SDK and JDK in Unity

![](Images/MainTitle.jpg)

In this tutorial, we will setup the Android SDK and JDK in Unity to be able to build an APK file. 

## Overview
The Unity version used in this tutorial is **2017.3.1f1**. The version has nothing to do with the tutorial. The SDK steps are the same in all Unity versions.
We will first download the **Android SDK** and **JDK** then we will set things up in Unity and build for Android.

## Downloading the Android SDK

An SDK stands for Software Development Kit. 

"*SDK is typically a set of software development tools that allow the creation of applications for a certain software package*" -[Wikipedia](https://en.wikipedia.org/wiki/Software_development_kit)

If it's your first time installing Unity or you have never set the SDK and JDK then

* Go to **Edit**>**Preferences..**
* **External Tools** and scroll down to **SDK** and **JDK**. The **NDK** isn't needed to build for Android.
* Press the **Download** button in front of the SDK
![](Images/1.jpg)
*Unity External Tools*

After pressing the download button, you are moved to the [**Android Studio** download page](https://developer.android.com/studio/index.html).

It is not ideal to download a total of around 2GB of Android Studio when you are not going to use it. We only need the **SDK Tools** that can be found at the bottom of the screen.

![](Images/2.jpg)
*Android Studio SDK command line tools*

We won't download this either. As it clearly says, **command line tools**. The previous versions of the SDK platform tools included the **SDK Manager.exe** we will see shortly. The current updated versions work with command line which I have tried using but failed. Since time is really important, then I looked for alternatives to download the older version which has the **SDK Manager** then update it. In case you are a fan of command lines, check this [link](https://developer.android.com/studio/command-line/sdkmanager.html)

Here is the [stackoverflow link](https://stackoverflow.com/questions/37505709/how-do-i-download-the-android-sdk-without-downloading-android-studio). In the first answer, download the one that says r24.4.1 for windows.

![](Images/3.jpg)
*Older SDK version r24*

Specify the install location wherever you want and after everything is completed, you will have something that looks like this. I have made my installation location in **ProgramFiles**>**Android**>**android-sdk**

![](Images/4.jpg)
*SDK installed*

Now open the SDK manager and let's update it and hopefully you will see something like this. Notice the SDK is clearly visible here as we will use this in **Unity** later.

![](Images/5.jpg)
*SDK installed*

We are not going to download everything. Here is the list of things to download/update:

* From **Tools** (Simply the first 3)
   * Android SDK Tools
   * Android SDK Platform-Tools
   * Android SDK Build-Tools (The latest one available)

![](Images/6.jpg)
You can clearly see in the screenshot that I need to update my stuff.

* Only one **SDK Platform** is enough. I downloaded the latest right now which is **API 27**, **Android 8.1.0**. You can't build higher than the highest API installed. With Android 8.1 installed, you can build for Android 5 and any other version. But if you installed Android 6.0 for example, you won't be able to build for higher Android versions.
![](Images/7.jpg)
*One latest SDK Platform*

* Finally, from **Extras**
   * Google Play Services (If you want to publish on the play store)
   * Google Repositories (If you want to publish on the play store)
   * Google USB drivers.
   ![](Images/8.jpg)
*Extras*

## Installing JDK

Click the download button that was beside the **SDK** download button inside **External Tools**.

From my experience, right now, there are some issues with **JDK 10** and **JDK 9**, So I recommend using **JDK 8**.

Go to the download page and select the JDK 8 or simply visit this [link](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

![](Images/9.jpg)
*JDK Download Page*

![](Images/10.jpg)
*JDK 8*

Download the executables and simply install them like any other application.

## Setup in Unity

After installing the SDK and JDK, we need to let Unity know where are they by adding the path to **External Tools** we opened before.

You can get the SDK path from the **SDK Manager** as discussed earlier and the JDK is usually located in ``` C:\Program Files\Java\jdk1.X.X_XXX ``` if you didn't change any defaults where X is the version.

![](Images/11.jpg)

*External Tools*

## Build the APK

To build and test it on your Android device,

* Go to the **Build Setting**
* Select Android and then **Switch Platform**
* After the switch is completed, Press the **Build** button.
* Create a new folder named **Build** and choose a name for your APK
![](Images/12.jpg)
*Build*

For your information, the name that will appear when you install the app on your phone won't be the APK name. It will be the name set in the **Player Settings**
![](Images/13.jpg)
*APK Name*

## Summary

We downloaded both the SDK and JKD and set them up in Unity and finally built the project.

## Reference

* [Android Studio and SDK Tools](https://developer.android.com/studio/index.html)
* [StackOverflow Answer regarding SDK Manager.exe](https://stackoverflow.com/questions/37505709/how-do-i-download-the-android-sdk-without-downloading-android-studio)
* [SDK tools command line by Android Studio](https://developer.android.com/studio/command-line/sdkmanager.html)
* [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

## Social Media

* Connect with me on [LinkedIn](https://www.linkedin.com/in/mohammedalsayedomar/) to stay updated with the upcoming tutorials
* Follow me on [Twitter](https://twitter.com/Mohammed_Omar_U)