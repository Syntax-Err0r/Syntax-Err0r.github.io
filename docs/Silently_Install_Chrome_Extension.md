# **Silently Install Chrome Extension For Persistence**

### Introduction

### tl;dr

### Methodology

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