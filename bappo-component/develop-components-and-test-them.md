# Develop components and Test them

## Bappo-component project structure

```sql
├── src
│   ├── apis
│   ├── primitives -- foundation components
│   ├── components -- components made by primitives
│   ├── internals
│   └── index.js -- New components registering
```

## 1. Start developing

* Go to `bappo-components/src/components` folder create a new folder for your new components. For example `IconButton`
* Register your new component in `bappo-components/src/index.js`. For example add a new line in it as shown in the picture.

![register new component](../.gitbook/assets/image%20%287%29.png)

* Refer to other component folders to build your own components. Here we highly recommend using TypeScript to build your UIs.

## 2. Compile new components

Every time you make a new components or modify the old one, you need to compile the code first before you test it on Story-book-web. Go to `bappo-components` folder and build it

**Remember to close you story-book-web**/native project before compile new components

```bash
#Go to the root of components project
cd ./bappo-open/packages/bappo-components

#run the build script
npm run build
```

![successfully compile bappo-component](../.gitbook/assets/image%20%2814%29.png)

If you see the prompts saying that Successfully you can go to next step.

## 3. Add new story page for the new component

To let your new components can be seen on story-book. You need to add a new story\(displaying page\).

**Noticed that**: Storybook-web and Storybook-native share **the same** "story contents". So you only need to add a new page under `/bappo-open/packages/bappo-components/storybook/storybook-native/storybook/stories`

**1.Create new story** Go to the `stories` folder.

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native/storybook/stories
```

Follow the patterns to build your own story page.

![](../.gitbook/assets/image%20%2811%29.png)

**2.Write your example**

In each `example.js` file you can write the features of your new component. The following picture shows define `name`,`color` and `onPress` event of the `IconButton` components.

![code snippet example ](../.gitbook/assets/image%20%2810%29.png)

**3. Register your story**

If the story page is a new one, you need to register them in `index.js` under `bappo-open/packages/bappo-components/storybook/storybook-native/storybook/stories`  as show in the picture

![](../.gitbook/assets/image%20%2819%29.png)

## 4. Start storybook and Test your components

### 4.1 Test the performance on web-browser



Go to `storybook-web` folder and run the web server

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-web

npm start
```

Web browser will be open automatically and you will your new components page and example, in this case is `Icon Button`

![](../.gitbook/assets/image%20%2815%29.png)

### 4.2 Test the performance on ios



* Start the web server. Go to the storybook-native folder

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native/

npm start
```



* Run the Storybook-native on  simulator. 

  **Keep the web browser server running**, and open **a new  terminal** then start the ios simulator under the same folder

```bash
cd ./bappo-open/packages/bappo-components/storybook/storybook-native
# start the simulator
npx react-native ios
```

**Since Bappo-components is designed for cross platform.** If your components works well on mobile your will see your UI like this

![Iconbutton on story-book native](../.gitbook/assets/image%20%288%29.png)

If there some code not compatible with mobile platform you may see error like this.

![Error when code is not compatable with native](../.gitbook/assets/image%20%289%29.png)

### 4.3 Test the performance on Andorid

Repeat the steps in 4.2 but use `npx react-native android` to start android simulator

## 5. Commit changes and create a pull request

Once you have finished your code, commit it  in your branch and create a pull request 

## 6. Publish 

People who review the code need to publish the new version of the bappo component, please follow these steps .

### 6.1 Modify bappo-component Version and commit in master branch

Changes the version of Bappo-component in package.json, and make the commit message as same as the version number

![](../.gitbook/assets/image%20%2829%29.png)

**You don't need to push this change to master branch on github, this will be done automatically in step 6.2**

### 6.2 Publish it in npm

use the following command to publish 

```bash
cd ./bappo-open/packages/bappo-components

#Make sure you are in the right folder before publish
npm publish
```

Once you finish, the successful log should like this

> There are prepublish and postpublish hook setted to do several tasks, including storybook deploy etc.
>
> If you have interests in that have a look in package.json
>
> "prepublish": "npm run build",
>
>  "postpublish": "npm run release-storybook",

![successful log](../.gitbook/assets/image%20%2828%29.png)

There are errors you may  meet during publish

![](../.gitbook/assets/image%20%2827%29.png)

To fix that, one solution would be make sure you logon npm with command

```text
npm login
```

then enter your username, password and email address and one-time password from authenticator. See this help about how to setup [two facts authentication](https://docs.npmjs.com/configuring-two-factor-authentication)

![](../.gitbook/assets/image%20%2826%29.png)

### 6.3 Double check with github

After you publish, go to [bappo-open repo](https://github.com/bappogroup/bappo-open/commits/master) and you should see a commit group follow this pattern

![](../.gitbook/assets/image%20%2832%29.png)



