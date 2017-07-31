---
layout: default
title:  "Installation"
categories: Mobile-iQ
order: 1
---
# Installation

1) Download `mobileiq-0.9.1.aar` from [here](http://api.ematicsolutions.com/v1/sdk/dist/mobileiq-0.9.1.aar).

2) Switch to Project view - select Project from the Android dropdown (figure 1)

![Screenshot](http://api.ematicsolutions.com/v1/mobileiq/img/project-android-view.png)

<small>Figure 1\. The project files in Android view</small>

3) Copy `mobileiq-0.9.1.aar` to your app `libs` folder.

3) Add `flatDir` section to your **project** `build.gradle` file:

    allprojects {
        repositories {
            jcenter()
            flatDir {
               dirs 'libs'
            }
        }
    }

4) Add dependency in your **app** `build.gradle` file:

    dependencies {
        ...
        compile(name:'mobileiq-0.9.1', ext:'aar')
    }

5) Sync project.

6) Find `mobileiq-0.9.1` in External Libraries (visible in Project view), right-click -> Library Properties...

7) Click the 2nd plus sign (Specify Documentation URL). Paste `http://api.ematicsolutions.com/v1/sdk/doc/mobileiq-0.9.1-javadoc/` and press OK. Confirm with OK.


#### Product Browse Event

You should submit this event in your product Activity/Fragment/Dialog `onCreate` method:

    public void onCreate(Bundle savedInstanceState) {
       ...
       if (savedInstanceState == null) { // this will make sure the event is submitted only once, when opening the activity/fragment/dialog for the first time
          MobileIQ.Events.browse(product);
       }
    }
