---
title: 'SwiftUI: Project migration from UIKit'
image: /assets/migration.jpg
description: Apple released SwiftUI framework. The great tech that will allow to create great UI/UX faster. How to migrate from old project with UIKit to new SwiftUI?
lang: en    
date: 2019-06-17 10:09:09.000000000 +03:00
type: post

# categories:
# - iOS Development

classes: wide
excerpt_separator: <!--more-->

header:
  overlay_image: /assets/migration.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  show_overlay_excerpt: false
  teaser: /assets/migration.jpg


permalink: "/project-migration-to-swiftui/"
---
Apple released SwiftUI framework. The great tech that will allow to create great UI/UX faster. How to migrate from old project with UIKit to new SwiftUI?

It’s the first article of rewriting my very old project [PoloTicker](https://github.com/qaze/PoloTicker) with new SwiftUI.

Let’s start from migrating the project to new structure to run SwiftUI. So what’s new and what we need to change:

## Make sure that you are compatible with new tech.

Here’s what you’ll need:

*   macOS Catalina (beta)

*   Xcode 11 (beta)

*   (Optional) iOS 13 if you’ll need to run on device not only on simulator

All of them you can get from developer.apple.com . Scroll down to the bottom of the page and go to Software downloads. _You’ll need developer account to sign in and download updates_

![download xcode and mac os beta](/assets/0973EDE0-0170-44F1-8A6F-94C28FAD481A-1024x274.png)

## Ready to start!

Now open old project and start from creating empty SwiftUI. In this chapter we want only to move from loading old Storyboard file to starting the app from new Empty SwiftUI file. Now create a SwiftUI file:

![create swiftui file](/assets/238556B6-271F-474F-B994-21D052FD6E34-1024x721.png)

Name it some way.. I named it like MainView.swift and here is default text on centre of screen. Now I want to launch the app from it.

## Update AppDelegate

You need to add Scene life-cycle. iOS 13 now is focusing on UIWindowSceneDelegate as start point (previously it was UIApplicationDelegate). You need to implement inside your UIApplicationDelegate the following to pass the control to UIWindowSceneDelegate:

    // MARK:**UISceneSession Lifecycle**
    func application(_ application: UIApplication, configurationForConnecting connectingSceneSession: UISceneSession, options: UIScene.ConnectionOptions) -> UISceneConfiguration {
            return UISceneConfiguration(name: “Default Configuration”, sessionRole: connectingSceneSession.role)
    }

    func application(_ application: UIApplication, didDiscardSceneSessions sceneSessions: Set<UISceneSession>) {
    }

## Create your UIWindowSceneDelegate

Create an empty swift file called SceneDelegate.swift with following content:

    import UIKit
    import SwiftUI

    class SceneDelegate: UIResponder, UIWindowSceneDelegate {

        var window: UIWindow?

        func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
            // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
            // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
            // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).

            // Use a UIHostingController as window root view controller
            let window = UIWindow(frame: UIScreen.main.bounds)
            window.rootViewController = UIHostingController(rootView: MainView())
            self.window = window
            window.makeKeyAndVisible()
        }

        func sceneDidDisconnect(_ scene: UIScene) {
            // Called as the scene is being released by the system.
            // This occurs shortly after the scene enters the background, or when its session is discarded.
            // Release any resources associated with this scene that can be re-created the next time the scene connects.
            // The scene may re-connect later, as its session was not neccessarily discarded (see `application:didDiscardSceneSessions` instead).
        }

        func sceneDidBecomeActive(_ scene: UIScene) {
            // Called when the scene has moved from an inactive state to an active state.
            // Use this method to restart any tasks that were paused (or not yet started) when the scene was inactive.
        }

        func sceneWillResignActive(_ scene: UIScene) {
            // Called when the scene will move from an active state to an inactive state.
            // This may occur due to temporary interruptions (ex. an incoming phone call).
        }

        func sceneWillEnterForeground(_ scene: UIScene) {
            // Called as the scene transitions from the background to the foreground.
            // Use this method to undo the changes made on entering the background.
        }

        func sceneDidEnterBackground(_ scene: UIScene) {
            // Called as the scene transitions from the foreground to the background.
            // Use this method to save data, release shared resources, and store enough scene-specific state information
            // to restore the scene back to its current state.
        }

    }

Take a look at:

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions)

This is your start point now. As you can see we set our new created MainView as root view controller:

    // Create new Window
        let window = UIWindow(frame: UIScreen.main.bounds) 
    // Wrap our MainView in UIHostingController 
    // And set is as root view controller
        window.rootViewController = UIHostingController(rootView: MainView()) 
        self.window = window
        window.makeKeyAndVisible()

Seems pretty easy, isn’t it?  
But it won’t work yet, if you’d try you’ll see that it’s only black screen here. So what’s wrong?

## Make the app see UIWindowSceneDelegate

Check that target iOS is set to iOS 13:

![move to iOS 13](/assets/5243C43A-F097-40B1-B249-AFC6C6CBC054-1024x342.png)

1.  Update your Info.plist:  
    Open it as source code

![open info.plist as source code](/assets/A13A1B9E-60B0-4DD9-9C3C-F2895D108FBC.png)

Find there the key for your Storyboard and completely remove it from your Info.plist:

    <key>UIMainStoryboardFile</key>
    <string>STORYBOARD_NAME</string>

New you’ll need to add the following:

    <key>UIApplicationSceneManifest</key>
        <dict>
            <key>UIApplicationSupportsMultipleScenes</key>
            <false/>
            <key>UISceneConfigurations</key>
            <dict>
                <key>UIWindowSceneSessionRoleApplication</key>
                <array>
                    <dict>
                        <key>UILaunchStoryboardName</key>
                        <string>LaunchScreen</string>
                        <key>UISceneConfigurationName</key>
                        <string>Default Configuration</string>
                        <key>UISceneDelegateClassName</key>
                        <string>$(PRODUCT_MODULE_NAME).SceneDelegate</string>
                    </dict>
                </array>
            </dict>
        </dict>

This code will tell your application that you now want to launch with your scene delegate.

## It's done!

So now we’re ready!  
Launch the app and you should see MainView as first screen launched.

_P.S. I have faced with problem that the solution didn’t worked and resolved it through cleaning derived data of Xcode and completely removing old app from device at first_

_Thanks for reading!_