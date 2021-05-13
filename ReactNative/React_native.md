# React Native Notes

## Core and Native components

### Native Components

- At runtime, React Native creates the corresponding Android and iOS views for React components.
- Because React Native components are backed by the same views as Android and iOS, React Native apps look, feel, and perform like any other apps.
- lets you build your own Native Component for Android and iOS to suite your apps unique needs.
- Native Directory = a place where community build Native components

### Core Components

- a set of essential, ready-to-use Native Components you can use to start building your app today.

## Platform Specific Code

- React Native provides two ways to organize code and separate it by platform:
  - Platform Module
  - platform-specific file extensions

### Platform Module

- React Native provides a module that detects the platform in which the app is running.(`Platform.OS`, `Platform.select`)
- this option is for when only small parts of a component are platform-specific.
- can also detect android and iOS version

### Platform Specific Extensions

- React Native will detect when a file has a `.ios.` or `.android.` extension and load the relevant platform file when required from other components.

```js
// BigButton.ios.js
// BigButton.android.js
import BigButton from "./BigButton";

// React native will automatically pick the right file based on the platform
```

### Native Specific Extensions

- can also use the .native.js extension when a module needs to be shared between NodeJS/Web and React Native but it has no Android/iOS differences.
- Tip: configure web bundler to ignore `.native.js` extensions in order to avoid having unused code in your production bundle.
-
