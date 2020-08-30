# AltStore Sources

This document provides all the details that describe how to make your own AltStore Source. There are five important sections to read:

*   Creating the JSON
*   Releasing apps
*   Updating apps
*   Sending out news
*   New features coming soon

So lets dive right in.

# Creating the JSON file

If you have never directly handled a JSON file, it stands for "JavaScript Object Notation" and you can learn more about if from the [official website](https://www.json.org/) and [documentation.](https://jsonapi.org/)

There are three basic properties that belong in the primary object, everything is required unless otherwise stated.
```
{
  "name": "My Source",
  "identifier": "com.myname.mysource",
  "sourceURL": "https://mysource.com/apps.json",
```

**name**

This can be any valid string and can always be changed later if necessary.

**identifier**

This is a bundle identifier AltStore uses to keep your Source separate from every other source. For this reason, it is recommended to follow Apple's standard for an identifier (it is demonstrated above).

It's important to note here that changing this identifier down the road will have **consequences.** Users with the Source already installed will suddenly have conflicting identifiers with the online Source and will cause an error in AltStore that will require them to **completely remove** the Source before they can add it back.

**sourceURL** *(optional)*

If your user adds your Source using a URL shortener or you have the link to file stored on CDN, it is recommended that you include this property. This allows AltStore to save the exact link to the file which speeds up retrieval time.

# Releasing apps

```
"apps": [
  {
    "name": "My App",
    "bundleIdentifier": "com.myname.myapp",
    "developerName": "My Name",
    "subtitle": "The newest and greatest app around.",
    "version": "1.0",
    "versionDate": "2020-04-21",
    "versionDescription": "Squashed some bugs, made some new bugs.",
    "downloadURL": "https://myapp.com/app.ipa",
    "localizedDescription": "Features include:\n\n• Cool graphics\n• Top notch performance\n• Satisfying interactions",
    "iconURL": "https://myapp.com/assets/icon.png",
    "tintColor": "8A28F7",
    "size": 857669,
    "permissions": [
      {
        "type": "photos",
        "usageDescription": "Allows you to use your photo library to set your profile image."
      }
    ],
    "screenshotURLs": [
      "https://myapp.com/assets/screen0.png"
    ],
    "beta": false
  }
],
```
<div align="center">
  <img src="https://github.com/noah978/AltStore-Docs/raw/master/assets/delta-app-listing.png" alt="Delta App Listing" width="300px" height="auto"/>
</div>

**name**

Rather self-explanatory, this is what the name of your appears as in the AltStore.

**bundleIdentifier**

AltStore uses this to separate apps as individual listings.

This **must** be the same as your application's ```"CFBundleIdentifier"``` (located in ```info.plist```) in order for AltStore to be able to open the app after installation. Technically, it can be anything, but for all AltStore functionality to work, it should be the same as the application.

**developerName**

Also self-explanatory, this is just the name of the developer/developers that will appear in the AltStore app listing.

**subtitle** *(optional)*

This should be a short description of your app that will appear in the browse tab of AltStore. It should give a quick one sentence explanation of your app and why a user wants it.

**version**

The latest version of your application. This **must** match your application's ```"CFBundleShortVersionString"``` (located in ```info.plist```) in order for AltStore updates to work properly. More on this later in the **Updating apps** section.

**versionDate**

This should be the date that you are releasing your application, and should be written in the format ```YYYY-MM-DD```.

If you are planning on releasing your application in the future, after everyone has installed your Source, there is an additional format available: ```YYYY-MM-DDTHH:MM:SS```

Using this format will create an automatic timer countdown to the release time specified. Please note that the time is automatically assumed to be UTC and uses a 24 hour clock.

If you would rather use the time in your timezone, add ```-08:00``` to the end of the ```versionDate```, where that -08 corresponds to the number of hours difference between UTC and your timezone. It is also important to note that UTC does not change with daylight saving time, so be careful if you are releasing around that time of year as it can be easy to miscalculate.

**versionDescription** *(optional)*

Use this to tell the user what new features you introduced or what bugs you squashed.

**downloadURL**

This should point directly to wherever your IPA is hosted.

**localizedDescription**

This is where you can include every feature and detail about your app. The user will see the first 5 lines of text then can click "More" to expand to the full section. So you should think of the first couple sentences as a quick pitch for your app.

**iconURL**

This should point directly to wherever you host the icon for your app. Note that this doesn't have to be the same as the icon used for the actual application, but it is recommended to maintain consistency.

**tintColor** *(optional)*

This might take some experimentation, but the best tint color is usually choosing one of the darker colors represented in your app icon. The tint color will be used in two places:

*   For the install button
*   As a background color for the larger app listing bubble (but this will be a lighter shade)

**size**

This is an integer value that should be set equivalent to the size of your IPA in bytes. This gives the user an idea of how large the application is before they install.

**permissions** *(optional)*

This is to show the user what various permissions your app requires. Create an entry for each separate permission your app requires. The accepted permission ```types``` are the following:

*   photos
*   camera
*   location
*   contacts
*   music
*   microphone
*   speech-recognition
*   bluetooth
*   calendars
*   faceid
*   siri

Your ```usageDescription``` should explain what the permission is and why your app needs it.

**screenshotURLs** *(optional)*

These should point directly to any number of screenshots/images that display your app's functionality. The first two will be displayed under the app listing in the browse tab, and the rest will be visible on the app's page.

**beta** *(optional)*

Here you can specify whether apps should be classified as a beta application and receive a special beta tag on its app listing.

# Updating apps

AltStore will automatically notify users about updates to your app and will prompt them to install the update.

<!--Releasing an update is relatively simple, you need to create a new entry in the ```versions``` array. It is recommended that you keep older versions available to download, but this is not required and older versions can be removed.-->

This means that the following properties should be changed to reflect the updated app:

*   version
*   versionDate
*   versionDescription
*   downloadURL
*   size

<!--You can change any of the other properties like the ```iconURL``` or ```screenshotURLs```, but these don't need to be specific to the various versions.-->

# Sending out news

Please note that the "news" array is required to be a valid AltStore Source. You can choose to leave the section empty if you prefer.

```
"news": [
  {
    "title": "My App Now Available!",
    "identifier": "my-app-available-download",
    "caption": "The app to beat all apps.",
    "date": "2020-04-21",
    "tintColor": "8A28F7",
    "imageURL": "https://myapp.com/assets/news.png",
    "url": "https://myapp.com",
    "appID": "com.myname.myapp",
    "notify": false
  }
]
```

<div align="center">
  <img src="https://github.com/noah978/AltStore-Docs/raw/master/assets/delta-news.png" alt="Delta News Item" width="300px" height="auto"/>
</div>

**title**

Fairly straightforward, this will be the headline for your news item.

**identifier**

This **must** be a unique identifier that should not be used by any other news items in AltStore.

**caption**

Similar to the caption for your app listing, this should be about a sentence. While there is no technically limit to the caption size, no one wants a giant text blob in their news feed. If there is more to your news than a couple sentences can deliver, try using an image or link to a website.

**date**

This date should follow the same format as the ```versionDate``` for app listings: ```YYYY-MM-DD```.

Please note that the date does not currently display on any news items and neither does the time (if provided). Instead, it is required for AltStore to organize the news into chronological order.

**tintColor** *(optional)*

This has the same function as the ```tintColor``` for app listings. The only difference, is that now it will be used as the background color for your news item (and app listing if applicable).

**imageURL** *(optional)*

This should be a direct link to any image you want to feature on your news item. Note that the recommended size for this image is 960x540 or any image with a 16:9 aspect ratio. AltStore will also take whatever image you provide it with, then crop and center it to the correct aspect ratio. Be careful not to put any important information in the corners since the AltStore rounds the images corners by default.

**url** *(optional)*

This should be used to link users to a website when they click the news item. The link will open in AltStore's built-in web browser (based off safari).

**appID** *(optional)*

This **must** be an exact match to the ```bundleIdentifier``` of the app listing in order for it to work properly.

This is required if you want an app listing to appear below the news item for quick installation.

It also makes it so that when a user click on the news item, it will take them to the specified app's page. This will be overridden if a ```url``` is specified.

**notify** *(optional)*

When set to true, AltStore will send all users of the Source a notification with the ```title``` of the news item.

Note that the notification will not be instantaneous: it will occur whenever AltStore attempts a background refresh (the same time that update notifications occur) and it does require users to leave AltStore running in the background.

# New features on the horizon

Not entirely sure what these will look like and they are not set in stone yet. But these should give you any idea of what future features AltStore Sources might have.

---

### Patreon support

```
"userInfo": {
  "patreonAccessToken": "afjbsafasfvsjdgfjhkouohjkledjyrqwfgse"
}
```

This will allow you to set certain apps to only be available to your Patrons. Other similar capabilities to this will available to specify in the ```userInfo``` section in future.

---

### Version history

```
"versions": [
  {
    "version": "1.1",
    "versionDate": "2020-04-21",
    "versionDescription": "Bug fixes.",
    "downloadURL": "https://myapp.com/myapp-1.1.ipa",
    "size": 87129
  },
  {
    "version": "1.0",
    "versionDate": "2020-03-30",
    "versionDescription": "First AltStore release!",
    "downloadURL": "https://myapp.com/myapp-1.0.ipa",
    "size": 79821
  }
]
```

This allows you to list multiple versions of your application in the app store and keep a changelog of your app. Users on older iOS versions will still be able to use your app even after you switch to newer iOS versions.

---

### Multi-device screenshot support

```
"screenshotURLs": {
  "iphone-standard": [
    "https://myapp.com/assets/screen0-standard.png"
  ],
  "iphone-edgeToEdge": [
    "https://myapp.com/assets/screen0-edgetoedge.png"
  ],
  "ipad": [
    "https://myapp.com/assets/screen0-ipad.png"
  ]
},
```

This will allow you to specify the size of the images you are adding so that AltStore will display the correct screenshot sizes for the appropriate device.

---

### App categorization

```
"category": "games",
"subcategories": [
  "action",
  "platformer"
],
```

The category and subcategories will allow you to specify which category fits your app best and what other subcategories are appropriate as well. The full list of categories that Apple uses for its App Store can be [found here.](https://www.idev101.com/code/Distribution/categories.html)

<!--Nothing new coming as of right now. Please reach out to the developer of AltStore using Twitter or the AltStore GitHub repository if there is a feature you'd like to have for your AltStore app listings.-->

# That's all there is!

If you want to see the full JSON example file that was used throughout this tutorial, [here it is.](https://github.com/noah978/AltStore-Docs/blob/master/apps.json)

My personal AltStore Sources can be found at the [Quark Sources website](https://quarksources.imfast.io) and I would highly recommend using this [AltStore Source Browser](https://altsource.by.lao.sb/browse/) to get a visual display of your Source outside of AltStore.
