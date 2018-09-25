# Plugins' platforms directory should not exist in tns_modules

## Issue
Plugins' `platforms` directory should not exist in `<project dir>/platforms/<platform>/.../app/tns_modules/`
During project preparation CLI copies all `node_modules` to `tns_modules` directory and cleans their native files, located in their `platforms` directories.
However, in case NativeScript plugin is a dependency of another NativeScript plugin and `npm` places it inside `node_modules` of the plugin, not at the root of the project, CLI does not clean the `platforms` directory of the inner plugin.
This issues occurs mainly in case there's a local plugin.

## Steps to reproduce:
1. Clone this repo:
```
$ git clone https://github.com/rosen-vladimirov/application-tns_modules-native-files.git
```

2. Get inside the `nativescript-ui-listview` directory and execute `npm install` there:
```
$ cd application-tns_modules-native-files/nativescript-ui-listview
$ npm i
```

3. Get back inside the project dir and build the application:

```
$ cd ..
$ tns build ios
$ tns build android
```

4. Check the following dir - it should not exist, but in fact it is there:
```
$ ls -l platforms/ios/applicationtnsmodulesnativefiles/app/tns_modules/nativescript-ui-listview/node_modules/nativescript-ui-core/platforms

$ ls -l platforms/android/app/src/main/assets/app/tns_modules/nativescript-ui-listview/node_modules/nativescript-ui-core/platforms

```

Full script:
```
git clone https://github.com/rosen-vladimirov/application-tns_modules-native-files.git
cd application-tns_modules-native-files/nativescript-ui-listview
npm i
cd ..
tns build ios
tns build android
ls -l platforms/ios/applicationtnsmodulesnativefiles/app/tns_modules/nativescript-ui-listview/node_modules/nativescript-ui-core/platforms
ls -l platforms/android/app/src/main/assets/app/tns_modules/nativescript-ui-listview/node_modules/nativescript-ui-core/platforms

```
