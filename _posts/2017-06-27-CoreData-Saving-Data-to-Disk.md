---
layout: post
title: "Persisting (Saving) Data to Disk"
tags:
  - swift
  - ios
  - CoreData
  - persistance
published: true
---

in AppDelegate.swift

- `applicationWillResignActive` - e.g. using app and phone call comes in
- `applicationDidEnterBackground` - e.g. user switched to another app


> Note: `applicationWillTerminate` - app is about to be killed by the OS. Not enough time to save, can cause errors. Too risky.

Don't save to often. On every record creation. Use **autosave** at set intervals. Don't forget to check the context to check if there is new data to be saved.

	func autoSave(_ delayInSeconds : Int) {
	
	    if delayInSeconds > 0 {
	        do {
	            try saveContext()
	            print("Autosaving")
	        } catch {
	            print("Error while autosaving")
	        }
	
	        let delayInNanoSeconds = UInt64(delayInSeconds) * NSEC_PER_SEC
	        let time = DispatchTime.now() + Double(Int64(delayInNanoSeconds)) / Double(NSEC_PER_SEC)
	
	        DispatchQueue.main.asyncAfter(deadline: time) {
	            self.autoSave(delayInSeconds)
	        }
	    }
	}