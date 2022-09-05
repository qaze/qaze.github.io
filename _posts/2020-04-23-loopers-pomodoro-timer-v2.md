---
title: 'Loopers: Pomodoro Timer with SwiftUI, Combine and Catalyst'
image: /assets/promo_pomodoro.jpg
description: I just published a simple pomodoro timer completely rewritten in SwiftUI and I am here to share my thoughts on it.
lang: en    
date: 2020-04-23 10:09:09.000000000 +03:00
type: post

classes: wide
excerpt_separator: <!--more-->

header:
  teaser: /assets/promo_pomodoro.jpg

permalink: "/loopers-pomodoro-timer-v2/"
---
![loopers pomodoro timer](/assets/promo_pomodoro.jpg)
Link: [App Store](https://apps.apple.com/us/app/loopers-simple-pomodoro-timer/id1255584873?ls=1)

I just published a simple pomodoro timer completely rewritten in SwiftUI and I am here to share my thoughts on it.

* **SwiftUI is a big step to the future** of iOS Development. It feels so much better when you avoid the heavy storyboards and the slow constraint systems in your app. Also it seems to be the first time in a while when Apple introduces a new framework that enforces a good architecture. It was so easy to write bad code in MVC and I hope MVVM will reduce the quantity of “bad code”.

* **SwiftUI is not ready for a “big” production yet**. If you have an existing app in App Store don’t hurry to move to SwiftUI. It has a lot of counter-intuitive solutions and will make it difficult to make some easy things. I have suffered with accessibility (it took a lot of time to figure out how to get accessibility identifiers to work), shadows (especially with paths) and animation (it’s not so clear as it looks).

* **Combine is good, perhaps**. I have not worked with RxSwift much and cannot judge how combine is efficient. But for this small project it was sufficient. Especially I’ve loved to work with Futures from Combine.

* **Catalyst is controversial**. I have been waiting for it more than for SwiftUI. I hoped that Catalyst is going to be the future where I can port an app in one week without tons of efforts. Well, partially it is so. But let’s take a look deeper:

	1. First of all, yes - **you can port your app** really quickly and it’s really amazing.
	
	2. It takes much more time to **make your app work the right way** (I’m still trying). There is a plenty of different hidden problems that you’ll find out while testing. For example, lists in Catalyst cannot be scrolled with cursor.
	3. **Look & Feel** is the most sad part. It was not obvious for me previously but just ported from iPadOS to MacOS app doesn’t feel like a Mac app. Ugly tab bars, design made for touch, how everything behaves. It feels wrong and takes time to fix it up.

**To sum it up:** SwiftUI, Combine, Catalyst are cool and fresh. Obviously, these tools will make our daily routine easier and more productive. But it needs some time to start to work the right way. I am waiting WWDC and believe Apple will improve all of them and lead us to the world without Storyboards and autolayouts.
I appreciate any feedback.


<script type="text/javascript" src="//downloads.mailchimp.com/js/signup-forms/popup/unique-methods/embed.js" data-dojo-config="usePlainJson: true, isDebug: false"></script><script type="text/javascript">window.dojoRequire(["mojo/signup-forms/Loader"], function(L) { L.start({"baseUrl":"mc.us5.list-manage.com","uuid":"0cf820f77cd8b01834a217372","lid":"94d28941f1","uniqueMethods":true}) })</script>