---
<!-- layout: post -->
title: rvictl in XCode 11 and MacOS Catalina
date: 2019-10-07 09:08:14.000000000 +03:00
type: post

meta:
  description: How to use rvictl on new MacOS Catalina and Xcode 11. This
    tutorial will also tell you how to sniff iOS traffic and find your iOS Device
    UDID.


header:
  overlay_image: /assets/rvictl.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  show_overlay_excerpt: false
  teaser: /assets/rvictl.jpg

permalink: "/rvictl-in-xcode-11-and-macos-catalina/"
---
I have faced with a problem that small and very useful program rvictl become unavailable MacOS Catalina and XCode 11\. I will provide steps how to get the application back. But at first let's take a look what rvictl is?!

rvictl ( Remote Virtual Interface Tool ) is a tool for capturing packets directly from your iOS Device. Let's imagine that you need to sniff traffic from your iOS Device. Obviously, you can use [Charles](https://www.charlesproxy.com), but what if you don't want to proxy traffic or your want to use more powerful [WireShark](https://www.wireshark.org). Then you need to use rvictl. You simply need to find your device UDID for example through Finder app.

![ios device udid catalina](/assets/image-3.png?fit=1024%2C282&ssl=1)

And type something like the following in terminal:
```
sudo rvictl -s [DEVICE UDID]
```
Output will be something like that:
```
Starting device [DEVICE UDID] [SUCCEEDED] with interface rvi0
```
But unfortunately new XCode 11 comes not bundled with rvictl available in terminal.

Go to the folder:
```
/Applications/Xcode.app/Contents/Resources/Packages
```
Double click MobileDeviceDevelopment.pkg and MobileDevice.pkg and proceed with installation.

That's it. Everything ready but there is one more thing that can be different in new version. if you'll try to use rvictl you can get something like:
```
command not found: rvictl
```
So you'll need to use it as following:
```
sudo /Library/Apple/usr/bin/rvictl -s [DEVICE UDID]
```
After that you can open WireShark and you'll see rvi0 interface that can be captured.

Hope you enjoyed this tutorial. Please let me know your thoughts.