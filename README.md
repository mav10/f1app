# ![app icon](./F1PilotsApp/ios/F1PilotsApp/Images.xcassets/AppIcon.appiconset/Icon-App-29x29@1x.png) F1 Pilots App

## Introduction
Requests and renders pilots of F1 from ergast.com API. This is a small app to demonstrate how to work with external API service.

:iphone:**Platforms:** Android, iOS.<br /> :keyboard:**Languages and frameworks:** Javascript, TypeScript, React-Native<br /> :hammer_and_wrench:**Tools&CI:** AppCenter

## Contents

- [Getting Started](#getting-started)
- [Libraries](#libraries-in-use)
- [Build and Test](#build-and-test)
- [Code styles](#code-styles)
- [Directory Structure](#directory-structure)
- [Code Push](#code-push)
- [App Signing](#app-signing)
   - [Android](#android)
   - [iOS](#ios)
- [Troubleshooting](#troubleshooting)
- [Other](#other)


## Getting Started :rocket:

How to launch it. First of all, make sure that you have already configured env for React-native on your machine (windows/linux/mac) and installed sdk for target platform android or iOS. See this link how to do it [here](https://reactnative.dev/docs/environment-setup)

1. Clone the repo
2. Install dependencies `yarn install` 2. if you are building iOS project, do not forget `pod isntall` from **ios folder**
3. `yarn ios` or `yarn android`
4. Have fun :)

## Libraries in use
- [Axios](https://github.com/axios/axios) for api calls
- [Date-FNS](https://date-fns.org/) toolset for manipulating JavaScript dates
- [React Navigation](https://reactnavigation.org/) for navigation and deeplinking.
- [Redux](https://github.com/reduxjs/redux) state management
- [redux-persist](https://github.com/rt2zz/redux-persist#readme) auto sync of state to async-storage (useful for storing auth token)
- [react-native-bootsplash](https://github.com/zoontek/react-native-bootsplash) because splash screens are cool and needed (also provides CLI for generating splashes)
- [react-i18next](https://github.com/i18next/react-i18next) internationalization.
- [react-native-restart](https://github.com/avishayil/react-native-restart) helps to re-launch app if it stuck on ErrorBoundary
- [react-native-modal](https://github.com/react-native-modal/react-native-modal) provide famous MODAL component to use it in app
- [Code Push](https://github.com/microsoft/react-native-code-push) synchronize JavaScript and Images with over-the-air updates.
- [react-native-config](https://github.com/luggit/react-native-config) for providing ENV variables
- [AsyncStorage](https://github.com/react-native-community/async-storage) you're gonna install it anyway.
- [Detox](https://github.com/wix/Detox) for e2e.
- [Jest](https://github.com/facebook/jest) for unit and component testing.
- [why-did-you-render](https://github.com/welldone-software/why-did-you-render) utils which help you to avoid re-renders.


## Build and Test

To run ios: launch xcode or type in console `yarn ios` To run android: launch emulator or connect real device via USB, after that type `yarn android`

## Code styles

- use shared (stored in the project) code styles based for IDE
- configure a watcher for prettier.
- configure a watcher for eslint.

_Adjust some rules of them if it is needed._

## Directory Structure

```
root
├── __mocks__
├── __tests__
|    ├── mockApi
|    ├── PageObjects
|    ├── Tests
|    └── utils
├── android
├── assets
|    ├── fonts
|    └── images
├── ios
└── src
    └── appInfrastructure
    |   ├── constants
    |   ├── error-handling
    |   ├── hooks
    |   ├── localisation
    |   |   └── dictionaries
    |   └── redux-store
    |       └── persistence
    └── commons
    |   ├── buttons
    |   ├── modal
    |   └── styles
    └── components
    |   ├── loaders
    |   └── version
    └── features
    |   ├── app
    |   └── auth
    └── helpers
    └── navigation
    └── screens
    |   ├── Home
    |   └──NetworkError
    └── services
        └── api
```

Quickly get an idea about each folder's role.

| Directory          | Short Description  /
--------------------|---|
| root               | Root directory. Contains many configuration files and all other folders. |
| \_\_mocks\_\_      | Mocks files for JEST tests |
| \_\_tests\_\_      | (Default; as per official template) + configured component tests with JEST |
| mockApi            | Stub and mock of API calls via **nock** |
| PageObjects        | Test instances of component. Helps to manipulate/find components during test |
| Tests              | JEST test suites |
| utils              | some utils and helpers for testing |
| android            | Android project. Includes modifications to integrate libraries. |
| assets             | Shared images, fonts etc. |
| e2e                | Detox end-to-end tests and configurations.  |
| ios                | iOS project. Includes modifications to integrate libraries. |
| src                | Most of the app's code is here. |
| infrastructure     | App infrastructure codes. Setup of managers, services, redux initializing etc. |
| constants          | Shared constants like a async-storage-keys, routes of navigators |
| redux-store        | Redux integration. Redux custom middleware. |
| persistence        | Redux-persistence integration and migrations |
| commons            | Shared code between different features. Dummy controls |
| buttons            | Custom shared button control |
| modal              | Custom shared modal control |
| styles             | Shared app styles, fonts, color schema |
| components         | Shared React components. Difference between components and common - components more project orientated. e.g. There is a modal control, but there is a LoginModal component |
| loaders            | Loader for fetch/restore indication. |
| version            | Control that displays app version, including code push. It is component (not common). e.g. it could have re-used common CustomText from common. |
| features           | Feature directories. |
| app                | App-redux state (actions, reducer, state, selectors). |
| helpers            | Shared utilities. |
| navigation         | Contains a simple stack navigators and its configuration (user, authorization and common screens, plus headers controls). |
| screens            | Folder with a navigator's screens containers(components) |
| Home               | Home screen. Has logo off app (taken from bootsplash), redirect buttons to another screen, sentry test buttons, logout button and version number control. |
| NetworkError       | Screen to display that user has problem with Internet connection |
| services           | App's services. |
| api                | Folder for autogenerated clients with NSWAG and react-query factory. |

## Code Push

You can distribute CodePush release from Azure pipeline (see in "CI Readme") build or manually.

For manual release see that doc
_Pre-setup:_

1. Setup codePush CLI globally via;
2. login in cmd via token from AppCenter (Account settings -> User API tokens section)

```
npm install -g appcenter-cli
```

Every time when you are going to release something:

1. Run tests (before you changed something) **[REQUIRED]**

   `yarn test`

2. It is not required, but nice to do it before - run E2E test **[ADDITIONAL]**

   _See block with E2E tests_

3. Made some changes
4. Run unit tests again (To make sure that you didn't break anything) **[REQUIRED]**
5. Run E2E tests (To make sure that you didn't break anything) **[ADDITIONAL]**
6. Deliver changes to "Code Push" **[REQUIRED]**
    1. IOS - Do not forget to change Deployment Type (**-d**) and description message (**-description**). Description message is used only for AppCenter UI. If you want to do it for a special version - add target version via **--target-binary-version "~1.1.0"**
   ```
   appcenter codepush release-react -a AppCenterOrganisation/F1PilotApp-iOS -d Staging --description "Description Message"
   ```
    2. ANDROID - Do not forget to change Deployment Type (**-d**) and description message (**-description**). Description message is used only for AppCenter UI.  If you want to do it for a special version - add target version via **--target-binary-version "~1.1.0"**

```
  appcenter codepush release-react -a AppCenterOrganisation/F1PilotsApp-Android -d Staging --description "Description Message"
```

After that you can see result in AppCenter UI ![ios CodePush results](./doc/code_push.png)

## App signing
Your built app should be signed by developer certificate(key) to be uploaded to stores.

_A few words about it and more..._

⚠️⚠️⚠️IMPORTANT⚠️⚠️⚠️

First of all, it is recommended to use different certificate for development and production (real app that will be uploaded to store).
So, if you have already uploaded app to store - certificate can not be updated (replaced). You will have to create new (register) new one for uploading the same app with new signing certificate.
It happens, when you lose "certificate" or forgot password, so take care about clear access to such files every time of app life cycle.

### Android
For android, it is easy - you have to run `Java keytool` CLI for generating keystore certificate.

```
keytool -genkey -alias <desired certificate alias> -keystore <keystore name.keystore> -storetype PKCS12 -keyalg RSA -storepass <password> -validity 10000 -keysize 2048
```

e.g. for this app (REPLACE **PASSWORD** - it is too SIMPLE!!!).
```
keytool -genkey -alias SOME_alias -keystore MyApp_dev.keystore -storetype PKCS12 -keyalg RSA -storepass Qwerty123# -validity 10000 -keysize 2048
```

after that wizard will ask you about questions Write down corresponding information something like this
```
CN=Developer, OU=Mobile, O=Home, L=Tomsk, ST=Tomsk, C=RU
```

Generate such files and upload them into CI, where you are going to sign apps (e.g. AppCenter).
Store files somewhere where team members can access to them, but not every person.
Save certificate password, alias name and alias password in secure storage e.g. KeyPass database.

### iOS

For iOS there are same rules. But you need certificate and provision profile.
Second one must include tester's iphone UDID. (how to get it from device see 👉 https://get.udid.io/)

- Development (AD-HOC) - will be distributed thorough AppCenter
- Development (TestFlight) - will be distributed to stakeholders through TestFlight. Can not be installed directly from CI
- Production (Apple certificate) - will be distributed to stakeholders through AppStore. Can not be installed directly from CI.

## Troubleshouting

If you have some problems with startup the app, try to run these commands

```
watchman watch-del-all &&
rm -rf $TMPDIR/react-native-packager-cache-* &&
rm -rf $TMPDIR/metro-cache* &&
rm -rf node_modules/ &&
yarn cache clean &&
yarn install &&
yarn start -- --reset-cache
```

Also, you can drop build folders from Xcode apps it is located at `~/Library/Developer/Xcode/DerivedData`

## Other

- Nothing to write home about ;)
