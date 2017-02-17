# fat-aar-plugin

[ ![Download](https://api.bintray.com/packages/vigidroid/maven/fat-aar-plugin/images/download.svg) ](https://bintray.com/vigidroid/maven/fat-aar-plugin/_latestVersion)

[WIP] This is a gradle plugin that helps to output fat aar from android library.

It's inspired by [android-fat-aar](https://github.com/adwiv/android-fat-aar). And intent to make more flexible and functional.

It's convenient to **sdk developer**(developer that provide a single aar library).

## Getting Started

#### Step 1: Apply plugin

Add snippet below to your root build script file:

```gradle
buildscript {
    repositories {
        maven {
            url  "http://dl.bintray.com/vigidroid/maven"
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:xxx'
        classpath 'me.vigi:fat-aar-plugin:0.1.2'
    }
}
```

Add snippet below to the `build.gradle` of your android library:

```gradle
apply plugin: 'me.vigi.fat-aar'
```

#### Step 2: Embed dependencies

change `compile` to `embed` while you want to embed the dependency in the library. Like this:

```gradle
dependencies {
    // aar project
    embed project(':aar-lib')
    // java project
    embed project(':java-lib')
    // java dependency
    embed 'com.google.guava:guava:20.0'
    // aar dependency
    embed 'com.android.volley:volley:1.0.0'
  
    // other dependencies you don't want to embed in
    compile 'com.squareup.okhttp3:okhttp:3.6.0'
}
```

**More usage see [example](./example-android).**

## About AAR File

AAR is a file format for android library.
The file itself is a zip file that containing useful stuff in android.
See [anatomy of an aar file here](https://developer.android.com/studio/projects/android-library.html#aar-contents).

**support list for now:**

- [ ] manifest merge
- [x] classes jar and external jars merge
- [ ] res merge
- [ ] R.txt merge
- [x] assets merge
- [x] jni libs merge
- [ ] proguard.txt merge
- [ ] lint.jar merge
- [ ] aidl merge?
- [ ] public.txt merge?

## Known Defects or Issues

* Produce lots of(maybe) `Note: duplicate definition of library class`, while proguard is on. A workaround is to add `-dontnote` in `proguard-rules.pro`.
* Add minSdkVersion check in task `CheckManifest`. Note that it's done by `processDebugAndroidTestManifest` while clicking gradle sync.
* Something more is welcomed

## Thanks
[android-fat-aar](https://github.com/adwiv/android-fat-aar)