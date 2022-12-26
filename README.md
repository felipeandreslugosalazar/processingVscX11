# ProcessingVscX11

A really really basic "guide" for Visual Studio Code (WSL2) to run Processing 3 files and see the output using VcXsrv (x11)

## Description

It's been already almost 10 years since the very first time i played with Processing3.
It's been already almost 2 years since i set up my dev env for ruby and rails.
I did really like the way processing help me in those days to grab some programming concepts in the easiest way.
I also do really like the way VSC help me now with my code.
So... let's integrate both... 
How difficult could be set up VSC connected to WSL2 to run processing files and see the output in an extra window
like it originally happened considering wsl2 doesn't have a GUI?
Well this guide it's the asnwer to my question.
Almost a day of research.
Worth the try, ohhh yeah, it always does.

## Getting Started

### Dependencies
Some of the sofwate I use and had already install is...

WSL2
Linux on x86_64 ((Ubuntu))
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.4 LTS
Release:        20.04
Codename:       focal

Visual Studio Code
Version: 1.74.2 (user setup)
Electron: 19.1.8
Chromium: 102.0.5005.167
Node.js: 16.14.2
V8: 10.2.154.15-electron.0
OS: Windows_NT x64 10.0.19044
Sandboxed: No

From https://processing.org/download I got 
https://github.com/processing/processing/releases/download/processing-0270-3.5.4/processing-3.5.4-linux64.tgz
and unzipped it on the folder root
(pick any folder, treat it as your project root and unzip the tgz there, no need to install)

VcXsrv X Server (xlaunch)
Version "1.20.14.0" (31 dic 2021)

### Checking file tree

Having the enviroment set up with Windows + WSL2 + processing3 + xlaunch
we should  now check file tree configuration

What should we check ?

We need to have the processing examples, a .vscode/tasks.json file in the root, 
the processing folder with the processing-java executable is not critical to have it on root but easy for configuration.
Check the image to have a better idea of the configuration.

![image](https://user-images.githubusercontent.com/53477788/209586560-e076a5ac-53e0-4dc1-b8fd-c8269a309982.png)

### How to link all the programs (How to make it work)

* do we have at least one processing example to execute? yes? ok. (the example must be in a folder named as the  pde example)
* do we have the .vscode/tasks.json? yes? ok.
  If you dont know how to produce the file
  (on VSC press ctrl + shift + B,  follow the instructions and select the defaults options),
  Then edit the file like this...

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "options": {
    // if you are using wsl you need to set DISPLAY var
    "env": {
      // use this command to get the wsl nameserver
      // grep nameserver /etc/resolv.conf | sed 's/nameserver //'
      // "DISPLAY":"nameserver:no. of screen (0 for laptop)" 
      "DISPLAY": "172.20.208.1:0"
    }
  },
  "tasks": [
    {
      "label": "Run Sketch",
      "type": "shell",
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "presentation": {
        "echo": true,
        "reveal": "always",
        "focus": false,
        "panel": "dedicated"
      },
      "command": ".processing3/processing-java",
      "args": [
        "--force",
        // --sketch= MANDATORY arg!
        // just indicate the path where the example that you want to run is located 
        "--sketch=${workspaceRoot}/examples/shadow",
        "--output=${workspaceRoot}/output",
        "--platform=linux",
        // don't forget to put run to execute the example
        "--run"
      ]
    }
  ]
}
```

If everything went well once in Vsc from the pde example execute the tasks (ctrl + shift + b), with some luck you will see the sketch window...
Et Voila!!! Eureka!!!

## Help

Advises for common problems or issues.
```
```

## Authors

Contributors names and contact info

ex.
ex. 

## Version History

* 0.1
    * Initial Release (26.12.2022)

## License

This guide is free to follow by anyone under her/his own risk. :P
(No risk to use)

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
