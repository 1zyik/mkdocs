---
title: Command Prompt 
description: This doc page covers tips and tricks you can use with windows command prompt.
icon: lucide/terminal
---

# Windows CMD Prompt Tips and Tricks

### Install a windows service
``` bash
sc create name_of_the_service binPath="path\to\theexecutable.exe" DisplayName="name_of_the_service"
```
???+ tip
    Since this is an admin features, make sure to run this in an elevated window. <br/>
    You can also create multiple services at once using a ```.cmd``` file and runing it once


### Install an NService Bus service in windows
``` bash
"path\to\ServiceBusHost.exe" /install /serviceName:name_of_the_service /displayName:"name_of_the_service"
```