Android application development with C,C++ or C#
======================================

### Introduction
Android applications are written in the Java programming language. 
The Android SDK tools compile the code—along with any data and resource files—into an Android package, an archive file with an .apk suffix. All the code in a single .apk file is considered to be one application and is the file that Android-powered devices use to install the application.

### Key challenge
Integrating/Using existing components developed in C/C++/C# is a key challenge and is the focus of this post.
C/C++/C# development for Android Applications

Typical Android applications are composed of one or more application components (activities, services, content providers, and broadcast receivers). Each component performs a different role in the overall application behavior, and each one can be activated individually (even by other applications). The manifest file must declare all components in the application and should also declare all application requirements, such as the minimum version of Android required and any hardware configurations required. Following are the options explored for integrating with programs developed/available in native libraries.

- Mono: A cross platform solution - C# style coding for developing android/iPhone apps
- JNI: ‘.dll’ & ‘.so’ usage in any java programs and hence Android applications
- NDK: Android support for C/C++ coding integration

## MONO for Android
MONO - An open source, cross-platform, implementation of C# and the CLR that is binary compatible with Microsoft.NET
Mono for Android is a commercial product from Xamarin. Xamarin offers 'Mono for Android' along with 'MonoTouch framework' for iOS (iPhone and iPad development) and consists of a plug-in for Microsoft Visual Studio, a core Mono runtime, a Software development and bindings for native android APIs.
Such software is designed to leverage existing .NET applications, libraries and tools for Android development. With Mono for Android, developers can also call upon their native skills in .NET and the C# programming language in developing Android apps.

## Android NDK
NDK is designed to allow Android application developers to include native code in their Android application packages, compiled as JNI shared libraries. The Android NDK can be viewed as a set of tools that allows developers to embed native machine code compiled from C and/or C++ source files into their application packages.

## Observation & Suggestion
Android NDK is the extension of JNI from android community and it is free of cost, whereas Mono for Android is a commercial product and JNI needs additional configuration and root privileges
Development of Android apps with SDK & NDK will allow the full use of features available in android, whereas Mono has some restriction in using some features.
Development with SDK & NDK will be simple java (android based) rather, Mono has a different way C#. Android developers will find it difficult to adapt to Mono style of Application development.
For the reasons mentioned above we suggest using Android NDK for integrating C/C++ codes in an Android Application.
