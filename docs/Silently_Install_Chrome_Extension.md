# **Silently Install Chrome Extension For Persistence**

### Introduction

The last few weeks I have been interested in how Chrome Extensions work and how an attacker or Red Teamers like myself could leverage these for persistence/cookie stealing/etc. I came across a couple articles such as attackers using powershell to use the [--load-extension](https://unit42.paloaltonetworks.com/chromeloader-malware/) parameter at the command line or using [remote debbuging](https://posts.specterops.io/stalking-inside-of-your-chromium-browser-757848b67949). However, these seemed somewhat easy to "detect" because of the command line parameters, potentially the PPID's. I could hear my ex-coworker in the back of my mind saying "there's gotta be a better way!"

### tl;dr

I have identified a way to silently install a Chrome extension avoiding the "common" TTP's attackers use today. 

### Methodology/Walkthrough

### POC

- Crux Extension folder must be in C:\Public\Downloads

```

```

### Caveats

- I do not know how the extension id is created by Chrome but it appears to be related to HMAC (this is why we must have the hard coded path). However I do know away around it, just not programmatically but that should be an exercise for the reader :)

### Detections

- Edits on the "Secure Preferences" file not by Chrome processes
- Identify anomalous chrome extension file locations
- Low prevalence extensions

### Future Work

Below are some ideas I think could expand this TTP:

- Automagically creating the extensionId's based on the parameters given
- "Extension Stomping"
-- think module stomping but chrome extensions :)