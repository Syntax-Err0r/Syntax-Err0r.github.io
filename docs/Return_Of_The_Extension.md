# **Silent Chrome Extension Installation Revisited**


### tl;dr

Chrome has had some changes that identify installed extensions not from the web store and preventing them from being turned on not in Developer Mode, breaking my previous [method](https://syntax-err0r.github.io/Silently_Install_Chrome_Extension.html). I have not identified what exactly Chrome is keying off of but I did find a way to still load these extensions using the same files/techniques. This still avoids the IOC's of the more common methods attackers are known to use.

For the PoC I am installing [RedExt](https://github.com/Darkrain2009/RedExt)

### Introduction

A friend alerted me to the fact that something had changed with Chrome and my older script. I noticed that while the extension would be installed, Chrome would not allow it to run unless it was in Developer Mode because it was not from the Chrome Store. However, I also noticed by turning Developer Mode on I could still run the extensions, which is the purpose of Developer Mode. I was originally avoiding Developer Mode because I incorrectly assumed this had to be turned on via the GUI and it would be evident in the Process Command Line (similar to debug mode). However, there does not appear to be any indicators it is running in Developer Mode from a process perspective and turns out you can turn Developer Mode on via the Preferences/Secure Preferences File :)

### Methodology/Walkthrough

As originally mentioned Chrome is now doing some level of checking to prevent extensions not installed via the Chrome Store from being turned on without Developer Mode. Below is my original PoC against the most up to date Chrome. You will see the extension loaded but not turned on. 

![](assets/old_extension.gif)

Following a similar walkthrough on my [first blog](https://syntax-err0r.github.io/Silently_Install_Chrome_Extension.html) I recommend turning Developer Mode on, installing the extension, and then opening the Secure Preferences/Preferences file to identify WHAT exactly changed. You can use a [JSON diff tool](https://jsondiff.com/) for this.

### POC

Below is clip of the new working PoC. You will notice the extension is now enabled and running, and the chrome session is in Developer Mode.   

![](assets/new_extension.gif) 

### Detections

- Edits on the "Secure Preferences" or "Preferences" file not by Chrome processes which is easily doable in Defender (credit to waldo-IRC on this idea)
- Identify anomalous chrome extension file locations
- Low prevalence extensions

### Future Work

Below are some ideas I think could expand this TTP:

- BoF it
- "Extension Stomping" (think module stomping but chrome extensions)
- Identify what exactly broke so we do not need to use the Developer Mode method (although this may not even really be necessary)
