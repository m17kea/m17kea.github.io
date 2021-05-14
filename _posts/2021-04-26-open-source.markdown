---
layout: post
title:  "Developer setup - the basics"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---

# Custom apps

### Privacy preapproval 

Get bundle id: 
`osascript -e 'id of app "Parallels Desktop"'`

Get Codesign information: 
`sudo codesign -dv --verbose=4 /Applications/Parallels\ Desktop.app`

Complete Code signature requirement:

identifier="com.parallels.desktop.console" and anchor apple generic