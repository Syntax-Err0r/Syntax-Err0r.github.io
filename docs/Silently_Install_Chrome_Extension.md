# **Silently Install Chrome Extension For Persistence**

### Introduction

### tl;dr

### Methodology

### POC

- Crux Extension folder must be in C:\Public\Downloads

```

```

### Caveats

- I do not know how the extension id is created, this is why the hard coded path. However I do know away around it, just not programmatically but that should be an exercise for the reader

### Detections

- Edits on the "Secure Preferences" file not by Chrome
- Identify anomalous chrome extension file locations
- Low prevalence extensions

### Future Work
