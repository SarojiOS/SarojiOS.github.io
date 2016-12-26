
+++
categories = ["Swift"]
comments = false
date = "2016-05-27T19:34:45-08:00"
draft = false
showpagemeta = true
showcomments = true
tags = ["swift","function"]
title = "Static vs Class vs Global Functions in Swift"
description = "A short description on Static vs Class vs Global Functions in Swift"
+++

Almost every projects contains Utility Functions. With the introduction of Swift, there are multiple ways to write such functions.
Static Functions
Static functions are invoked by the class itself, not by an instance. This makes it simple to invoke utility functions without having to manage an object to do that work for you.
class AppUtils {
    static func appUtility() {
    }
}
We can access static function as AppUtils.appUtility()
Static functions can not be overridden.
Class Functions
Class functions (not instance methods) are also static functions but they are dynamically dispatched and can be overridden by subclasses unlike static functions.
class AppUtils{
    class func appUtility(){
        println("In AppUtils")
    }
}
class AppOtherUtils: AppUtils{
    override class func appUtility(){
        println("In AppOtherUtils")
    }
}
We can access them similar to static functions as AppUtils.appUtility() and AppOtherUtils.appUtility().
static is same as class final.
Global Functions
But then you can also just do a stand alone function in Swift which is not within a class and access it anywhere in the project. The global functions can be kept in a separate file that we can import into any project as per requirement.
func appUtility() {
}
We can just access them as appUtility() anywhere in the project. If you have method with same name as of global function, then access global function with MyAppName.appUtility()
In case of static functions, if we access one of the static member, entire class gets loaded in memory. But in case of global function, only that particular function will be loaded in memory.
So, which one is better to use?
It is largly subjective why we pick one over another. Some prefer static method approach as a form of namespacing. For example, using the static method approach also allows us to have a method ClassA.appUtility() and a method named ClassB.appUtility(), which is useful while developing a library or framework.
Global functions are more modular and factor out single tasks for a single function - a good global utility function that does exactly one thing and does it perfectly can also sometimes be abstracted or made generic and used in other context as well.
We can just create a AppUtility.swift file and put all the utility functions in it. Later this file can be used across multiple projects.
