# Pandit Booking Mobile App

This repository contains a Cordova-based mobile wrapper for the `Pandit Booking` app by Peaklyft. The project currently ships with a prebuilt web bundle inside `www/`, plus Cordova configuration, native app resources, and plugin declarations for Android and iOS packaging.

## What This Project Is

At a high level, this repo is:

- A Cordova mobile app with app id `com.peaklyftdev.panditbooking`
- A precompiled React single-page app mounted in `www/`
- Configured for both Android and iOS
- Focused on booking pandits and poojas, managing addresses, bookings, reviews, rewards, and account settings

This repo is not a full source workspace for the frontend. The original React source files are not present here. Instead, the app is already compiled into:

- [`www/index.html`](/Users/peaklyftdev/Documents/Cordova-Mobile/www/index.html)
- [`www/assets/index.js`](/Users/peaklyftdev/Documents/Cordova-Mobile/www/assets/index.js)
- [`www/assets/index.css`](/Users/peaklyftdev/Documents/Cordova-Mobile/www/assets/index.css)

That means:

- You can build and package the mobile app from this repo
- You can change Cordova configuration and native wrapper behavior
- You cannot comfortably maintain the React app feature code here, because only the production bundle is available

## Current App Identity

The real app identity comes from [`config.xml`](/Users/peaklyftdev/Documents/Cordova-Mobile/config.xml):

- App name: `Pandit Booking`
- Package id: `com.peaklyftdev.panditbooking`
- Version: `1.0.0`
- Author: `Peaklyft`

Important note: [`package.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package.json) still contains default Cordova sample metadata like `Hello Cordova`. That file should be treated as partially stale. For actual app branding and runtime behavior, trust [`config.xml`](/Users/peaklyftdev/Documents/Cordova-Mobile/config.xml) and the `www/` bundle.

## Product Summary

From the compiled routes and UI text, this app supports the following user-facing flows:

- App onboarding and language selection
- Login and OTP flow
- Profile setup
- Home screen and search
- Location and saved addresses
- Pooja listing and pooja details
- Pandit listing and pandit profile
- Booking slot selection
- Cart and booking confirmation
- My bookings
- Ratings and reviews
- Rewards / points / referral rewards
- Notifications
- Terms, privacy, refund policy, about, FAQs
- Language preferences
- Online pooja selection

## Likely Frontend Stack

The original source is not included, but the compiled bundle strongly indicates the app was built with:

- React 18
- React Router
- Tailwind CSS v4
- Lucide React icons
- Cordova runtime integration through `deviceready`

Evidence:

- React 18 appears in [`www/assets/index.js`](/Users/peaklyftdev/Documents/Cordova-Mobile/www/assets/index.js)
- Router-based route definitions appear in [`www/assets/index.js`](/Users/peaklyftdev/Documents/Cordova-Mobile/www/assets/index.js)
- Tailwind CSS banner appears in [`www/assets/index.css`](/Users/peaklyftdev/Documents/Cordova-Mobile/www/assets/index.css)

## Repository Structure

Key files and folders:

- [`config.xml`](/Users/peaklyftdev/Documents/Cordova-Mobile/config.xml)
  Cordova app config, preferences, native permissions, icons, splash setup
- [`package.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package.json)
  npm dependencies and declared Cordova plugins
- [`package-lock.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package-lock.json)
  locked dependency versions
- [`www/`](/Users/peaklyftdev/Documents/Cordova-Mobile/www)
  compiled web app loaded by Cordova
- [`resources/`](/Users/peaklyftdev/Documents/Cordova-Mobile/resources)
  Android and iOS app icons and splash images

Notably missing:

- No `src/` folder
- No Vite config
- No React source files
- No Android platform folder checked in
- No iOS platform folder checked in

This means native platforms are expected to be generated locally with Cordova commands.

## Cordova Plugins Used

The project currently declares these plugins in [`package.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package.json):

- `cordova-plugin-splashscreen`
- `cordova-plugin-wkwebview-engine`
- `cordova-plugin-ionic-keyboard`
- `cordova-plugin-statusbar`
- `cordova-plugin-camera`
- `cordova-plugin-file`
- `cordova-plugin-actionsheet`

### What Each Plugin Is For

- `cordova-plugin-splashscreen`
  Controls the native splash screen
- `cordova-plugin-wkwebview-engine`
  Uses WKWebView on iOS
- `cordova-plugin-ionic-keyboard`
  Keyboard behavior and resize control
- `cordova-plugin-statusbar`
  Status bar styling and overlay behavior
- `cordova-plugin-camera`
  Camera access, likely for profile photo uploads
- `cordova-plugin-file`
  File system access
- `cordova-plugin-actionsheet`
  Native action sheet menus

## Plugin Install Commands

If you need to recreate plugin setup manually, run:

```bash
npm install
```

Or install one by one with Cordova:

```bash
cordova plugin add cordova-plugin-splashscreen
cordova plugin add cordova-plugin-wkwebview-engine
cordova plugin add cordova-plugin-ionic-keyboard
cordova plugin add cordova-plugin-statusbar
cordova plugin add cordova-plugin-camera
cordova plugin add cordova-plugin-file
cordova plugin add cordova-plugin-actionsheet
```

You can also install the platform packages from npm:

```bash
npm install --save-dev cordova-android@^15.0.0 cordova-ios@^8.0.1
```

## Tools You Need Installed

### Required

- Node.js
- npm
- Cordova CLI

Install Cordova CLI globally:

```bash
npm install -g cordova
```

### For Android Development

- Android Studio
- Android SDK
- Java JDK compatible with your installed Android toolchain

### For iOS Development

- macOS
- Xcode
- CocoaPods

Install CocoaPods if needed:

```bash
sudo gem install cocoapods
```

## First-Time Setup

From the project root:

```bash
npm install
cordova platform add android
cordova platform add ios
```

If the platforms were previously added and you only want to refresh dependencies:

```bash
cordova prepare
```

## Common Commands

### Check the environment

```bash
cordova requirements
```

### List installed platforms and plugins

```bash
cordova platform ls
cordova plugin ls
```

### Prepare assets and web bundle for native platforms

```bash
cordova prepare
```

### Build Android

```bash
cordova build android
```

### Build iOS

```bash
cordova build ios
```

### Run on Android device or emulator

```bash
cordova run android
```

### Run on iOS simulator/device

```bash
cordova run ios
```

### Open native projects

```bash
cordova platform add android
cordova platform add ios
```

After platform creation, open:

- `platforms/android` in Android Studio
- `platforms/ios` in Xcode

## Runtime Behavior and Native Notes

Important configuration from [`config.xml`](/Users/peaklyftdev/Documents/Cordova-Mobile/config.xml):

- App is portrait-only on both Android and iOS
- Broad external navigation is allowed:
  - `http://*/*`
  - `https://*/*`
- Global access origin is currently `*`
- Keyboard resizing is disabled
- Android uses `adjustPan`
- Splash screen is configured on both platforms
- iOS status bar style is set to `lightcontent`
- iOS camera and photo library permission strings are defined

## How the App Starts

Startup behavior from the compiled app:

- `www/index.html` loads the built frontend and `cordova.js`
- The app waits for Cordova `deviceready`
- If `deviceready` does not arrive within 5 seconds, it force-starts the app
- On app resume, it checks `localStorage` for:
  - `authToken`
  - `userId`
- If either is missing, it redirects toward login

## Important Routes Found in the Bundle

The compiled app exposes these main routes:

- `/`
- `/language`
- `/onboarding`
- `/login`
- `/otp`
- `/profile-setup`
- `/app/home`
- `/app/search`
- `/app/location`
- `/app/add-address`
- `/app/edit-address/:id`
- `/app/saved-addresses`
- `/app/pooja/:id`
- `/app/pooja-list`
- `/app/pandits`
- `/app/pandit/:id`
- `/app/booking-slot/panditProfile/:id`
- `/app/cart`
- `/app/booking-confirmation/:id`
- `/app/account`
- `/app/my-bookings`
- `/app/my-reviews`
- `/app/my-points`
- `/app/rate-review`
- `/app/online-pooja-selection`
- `/app/notifications`
- `/app/referral-rewards`
- `/app/terms`
- `/app/privacy`
- `/app/about`
- `/app/faqs`
- `/app/language-preferences`

## What a New Developer Should Know First

If someone is starting on this project, this is the shortest accurate mental model:

1. This repo is mainly the mobile packaging layer, not the full frontend source.
2. The actual app UI is already compiled into `www/assets`.
3. Cordova plugins and `config.xml` matter a lot here because they control native capabilities and packaging.
4. If UI features need real development, you likely need the original React/Vite source repository that produced this bundle.
5. If the task is app signing, icons, splash screens, permissions, plugin wiring, or native build output, this repo is enough.

## Recommended Handoff Workflow

When a new developer starts:

1. Read [`config.xml`](/Users/peaklyftdev/Documents/Cordova-Mobile/config.xml)
2. Read [`package.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package.json)
3. Run `npm install`
4. Run `cordova requirements`
5. Add the target platforms with `cordova platform add android` and/or `cordova platform add ios`
6. Run `cordova plugin ls` and confirm all plugins are present
7. Build the app locally
8. If feature development is needed, ask for the original frontend source code repository

## Known Gaps / Risks

- [`package.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package.json) still has default sample metadata, which can confuse maintainers
- No real source code for the React app is included
- No test scripts are configured
- No CI/CD setup is present in this repo
- `access origin="*"` and broad navigation permissions may be looser than desired for production
- The app appears production-built, so debugging business logic from this repo alone will be difficult

## Suggested Next Improvements

To make this repo easier for future developers:

1. Update [`package.json`](/Users/peaklyftdev/Documents/Cordova-Mobile/package.json) metadata to match the real app
2. Add the original frontend source or link to its repository
3. Add a section for environment versions actually used by the team
4. Add signing and release instructions for Android and iOS
5. Add API/backend environment documentation
6. Document where the final `www/` bundle comes from and how it is generated

## Quick Start

If you just want to get moving:

```bash
npm install
npm install -g cordova
cordova requirements
cordova platform add android
cordova build android
```

For iOS:

```bash
npm install
cordova platform add ios
cordova build ios
```
