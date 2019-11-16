---
<!-- layout: post -->
title: 'iOS Common Issues #1: … this class is not key value coding-compliant for the key …'
date: 2019-06-28 09:37:04.000000000 +03:00
type: post
categories:
- iOS Development Posts
tags:
- crash
- ios
- swift
- uiviewcontroller
- xcode

meta:
  title: "How to fix: this class is not key value coding-compliant"
  description: "Every iOS developer definitely face with problem like: this class is not key value coding-compliant for the key. Here we will see how to resolve it."

permalink: "/this-class-is-not-key-value-coding-compliant-for-the-key/"

excerpt: "When you just at start of becoming great iOS Developer you already have faced or definitely will face with wide range of crashes. It can be very frustrating and can be big problem on your way on learning iOS development. I think every dev has faced and knows this XCode statement: _this class is not key value coding-compliant for the key_."

header:
  overlay_image: /assets/error_big.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  show_overlay_excerpt: false
  teaser: /assets/error.jpg

---
When you just at start of becoming great iOS Developer you already have faced or definitely will face with wide range of crashes. It can be very frustrating and can be big problem on your way on learning iOS development. I think every dev has faced and knows this XCode statement: _this class is not key value coding-compliant for the key_.

Full text of this crash can seem like the following:
```
*** Terminating app due to uncaught exception ‘NSUnknownKeyException’, reason: ‘[<UIViewController 0xXXXXXX> setValue:forUndefinedKey:]: this class is not key value coding-compliant for the key XXX.’
```
This crash can be quite annoying and it’s unclear what to do with that. But the issue is pretty simple to resolve. Let's take a look on common reasons:

## Outlet removed in the code, but is still set in Storyboard/Xib

You can have the situation like that.. You have some element in Storyboard/Xib that was previously bind to your View Controller but now you removed it from code and didn’t remove it from your interface file. Double check that you don't have situation like on following screenshots:

<table class="wp-block-table">

<tbody>

<tr>

<td>Outlet is connected to ViewController</td>

<td>Outlet is commented out in the code</td>

</tr>

<tr>

<td><img src="/assets/3DBB319E-BC51-48F2-AD01-9AC4A52D6453-e1561716031217.png"></td>

<td><img src="/assets/46F1D09E-3E82-4984-8B94-AE3DF5A27E7F.png"></td>

</tr>

</tbody>

</table>

* * *

## Class Name in Storyboard/Xib is wrong

It’s common mistake that class name set in StoryBoard / Xib is wrong. Below is example… just a misspelled word can cause this annoying crash:

<table class="wp-block-table">

<tbody>

<tr>

<td>Name is set to ViwController</td>
<td>Class name is View Controller</td>

</tr>

<tr>

<td><img src="/assets/BA005FA1-C081-46DC-9093-93F5DA5F8292.png"></td>

<td><img src="/assets/7301A409-391C-4D5B-A9BF-72A845050622.png"></td>

</tr>

</tbody>

</table>

* * *

## Error after copying a View Controller

Somehow it can appear after you have copied your View Controller. Please double check View Controller’s connection inspector each time you’re copying view controller in order to avoid such situations as below:

![ios xcode connection inspector](/assets/2475997A-D5D7-4739-BE13-4D79CEE239C9.png)

To resolve "class is not key value coding-compliant for the key" issue you just need to click on close button (x) of problem outlet and re-bind it one more time.

_Also please make sure that you have done full clean + rebuild after resolving such issues. Xcode is not perfect IDE and it still has a huge issue that can be resolved simply by clean ( Shift + CMD + K ) and build ( CMD + B )_

_Thanks for reading!_