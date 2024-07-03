# **Silently Install Chrome Extension For Persistence**

### Introduction

The last few weeks I have been interested in how Chrome Extensions work and how an attacker or Red Teamers like myself could leverage these for persistence/cookie stealing/etc. I came across a couple articles such as attackers using powershell to use the [--load-extension](https://unit42.paloaltonetworks.com/chromeloader-malware/) parameter at the command line or using [remote debbuging](https://posts.specterops.io/stalking-inside-of-your-chromium-browser-757848b67949). However, these seemed somewhat easy to "detect" because of the command line parameters and the PPID's. Additionally, these are not persistent across sessions. I could hear my ex-coworker in the back of my mind saying "there's gotta be a better way!". My main inspiration was when opening Chrome and going to extensions, you could turn debug mode on and load an extension so I thought there HAS to be a way to do it without command line shenanigans. 

So I began to dig into Chrome--I had all my debuggers ready in my FLARE VM. I was ready to tackle all the AES and DPAPI Google would throw at me! Then after a few hours, I realized all I would need to be able to silently install a Chrome extension was some parameters for an HMAC algorithm and JSON edits in 1 file. I have not seen anyone write about this other then a [research paper](https://www.cse.chalmers.se/~andrei/cans20.pdf) I came across while writing the PoC. I certainly did not see any "red team" blogs weaponizing it or anything like that so I hope this is somewhat new to most. I cannot imagine someone did not weaponize this already so I apologize if I burn a TTP.  

### tl;dr

I have identified a way to silently install a Chrome extension avoiding the "common" TTP's attackers use today. 

- no command line parameters
- persistent
- can be installed while in use but it wont re-load until chrome restarts so it is up to you if you want to kill chrome

### Methodology/Walkthrough

My initial methodology was to inspect DLL's related to Chrome to see if there was any obvious exports related to extensions. Additionally I wanted to debug Chrome to see what exactly happens when loading an extension (yes I know Chromium is open source but this is easier for me than reading gigantic code bases). After a bit of troubleshooting I thought about it and realized the EASIEST and LAZIEST way to identify what changes when Chrome loads an extension was just simple ProcMon. So I loaded up ProcMon and fired off Chrome and continued adding/removing extensions to see what files changed. 

I identified one file continusouly was getting touched -- "Secure Preferences" in %localappdata%\Google\Chrome\User Data\Default. The easiest way to check if this was really the "key" was to load an extension, copy the file off, unload it and close Chrome.   


### POC

-We will be using [Crux](https://github.com/mttaggart/crux) since its easy to use and install
-Crux Extension folder must be in C:\Users\Public\Downloads

```

```

Note: While writing the PoC I realized someone wrote a [research paper](https://www.cse.chalmers.se/~andrei/cans20.pdf) on this topic it just has not widely be weaponized (that I know of). They had some PoC code for the HMAC I leveraged on [github](https://github.com/Pica4x6/SecurePreferencesFile)

### Caveats

- I hardcoded some things and I purposefully made some "opsec mistakes"

### Detections

- Edits on the "Secure Preferences" file not by Chrome processes
- Identify anomalous chrome extension file locations
- Low prevalence extensions

### Future Work

Below are some ideas I think could expand this TTP:

- Automagically creating the extensionId's based on the parameters given
- BoF it
- "Extension Stomping"
-- think module stomping but chrome extensions :)