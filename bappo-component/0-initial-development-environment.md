# Initial development environment

## 1. Install software and solve dependences 

please read this article to initialize your development environment

> [https://app.gitbook.com/@bappo/s/bappo-platform-team/new-staff-training/working-environment-setup/macbook-setups-for-developing](https://app.gitbook.com/@bappo/s/bappo-platform-team/new-staff-training/working-environment-setup/macbook-setups-for-developing)

## 2. Clone repository

Using command line

```bash
git clone https://github.com/bappogroup/bappo-open.git
```



## 3. Install Dependencies



Please follow the order to install dependencies,otherwise, you may meet some error. This document is written under `node 10.18.1` `yarn 1.22.4` 

1.Install Dependencies for Storybook-web

```bash
cd bappo-open/packages/bappo-components/storybook/storybook-web

#install dependencies
yarn
```

2.Install Dependencies for Bappo-components

```bash
cd bappo-open/packages/bappo-components

#install dependencies
yarn
```

3.Install Dependencies for Storybook-native

```bash
cd bappo-open/packages/bappo-components/storybook/storybook-native

#install dependencies
yarn
```

## 4. Project Structure



**bappo-components** folder is the place we develop cross-platform components for Bappo-app.

**storybook** folder is the place where we store the display and testing project. After you add a new component or modifing the existing one. You can see the performance of your components by starting up Storybook-web and Storybook-native. This project is using [Storybook](https://storybook.js.org/) to show the use of bappo-components on each [story page](https://storybook.js.org/docs/basics/writing-stories/).\(Click the link to know more about storybook\)

Each story page is React based, components are imported from `bappo-components/src`. Developer can use it to test functions they made on their own components.

```sql
.
├── docs -- Documentation
└── packages
    ├── bappo-components
    │   ├── es -- Components after compile (ES modules)
    │   │   ├── apis
    │   │   ├── components
    │   │   ├── internals
    │   │   └── primitives
    │   ├── lib -- Components after compile (CommonJs)
    │   │   ├── apis
    │   │   ├── components
    │   │   ├── internals
    │   │   └── primitives
    │   ├── scripts
    │   ├── src -- Components source code
    │   │   ├── apis
    │   │   ├── components
    │   │   ├── internals
    │   │   └── primitives
    │   └── storybook -- Web and Mobile displaying and Function testing
    │       ├── storybook-native --Mobile displaying and Function testing
    │       └── storybook-web --Web displaying and Function testing
    └── bappo-grid
```

## 

## 5. Run Storybook-web locally

Go Storybook-web folder and run it.

```bash
#Go the bappo-web
cd ./bappo-open/packages/bappo-components/storybook/storybook-web

npm start
```

After Webpack Building, the storybook will be loaded and you can check all the existing components

![](../.gitbook/assets/image%20%285%29.png)

**Storybook-web** is for displaying Bappo-components and Functional test. Details can be seen in [Develop components and Test them](develop-components-and-test-them.md)

## 6. Run Storybook-native on a IOS/Android simulator

### 6.1 login your ios developer account in Bappo

**Noticed:** before login, ask William to add your account into Bappo group

Go to Xcode =&gt; Preference =&gt; Account, and click follow the order showing in this picture

![](../.gitbook/assets/image%20%2813%29.png)

After that make sure you are in the Bappo Team like this

![](../.gitbook/assets/image%20%284%29.png)

### 6.2 Install dependencies for storybook-native project



* Go to `ios` folder under `storybook-native` and install the Xcode project dependencies with `pod install`

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native/ios

pod install
```

If every thing goes right, you will see the output like this

![](../.gitbook/assets/image%20%2816%29.png)

> If you are curious about what `pod install` do, check this article to have a deep understanding - [What does pod install do](https://medium.com/@scottlydon18/podspecs-podfile-pod-install-what-happens-518af7e6471d#:~:text=The%20program%20pod%20goes%20to%20the%20source%20listed%20at%20the,.com%2FCocoaPods%2FSpecs.&text=and%20if%20there%20are%20different,it%20can't%20find%20it.)

### 6.3 Start storybook-native

* Start the Metro Bundler. Go to the storybook-native folder

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native/

##use one of the following command

npm start

or

npx react-native start --projectRoot storybook
```

> Check this article to know more about npx - [Introducing npx: an npm package runner](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b)

Go to next step until you see the following prompt

![Metro Bundler started](../.gitbook/assets/image%20%2817%29.png)

* Run the Storybook-native on Android simulator. 

  **Keep the Metro Bundler running**, and open **a new  terminal** then start the simulator under the same folder

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native

# This command is used to start the iOS simulator
npx react-native run-ios
```

**Notice:** If this is the first time you run it, it will take a few more minutes to install. Just take a cup of coffee. It depends on your CPU, memory. Then you will see the storybook on mobile.

![Storybook-native on IOS](../.gitbook/assets/image%20%2812%29.png)

## 7. Run Storybook-native on an Android simulator



* Start the Metro Bundler. Go to the storybook-native folder

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native/

##use one of the following command

npm start

or

npx react-native start --projectRoot storybook
```

> Check this article to know more about npx - [Introducing npx: an npm package runner](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b)

Go to next step until you see the following prompt

![Metro Bundler started](../.gitbook/assets/image%20%2817%29.png)

* Run the Storybook-native on Android simulator. 

  **Keep the Metro Bundler running**, and open **a new  terminal** then start the simulator under the same folder

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native

# This command is used to start the iOS simulator
npx react-native run-android
```

**Notice:** If this is the first time you run it, it will take a few more minutes to install. Just take a cup of coffee. It depends on your CPU, memory. Then you will see the storybook on mobile.

![Storybook-native on Android](../.gitbook/assets/image%20%286%29.png)

