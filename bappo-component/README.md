# Bappo Component

Please use this workflow when you make contributions to Bappo-Component 

## Step1. Came up with an issue on Github and discuss it

Write an issue [on this page](https://github.com/bappogroup/bappo-open/issues), in which please figure out what kind of bug you found, or what kind of feature for a user story.

Once you have done that. Reach out Platform team to discuss it. The reason we are doing that, is because we always want to have a beautiful and thorough solution to meet new feature. So discuss could you a lot of time on refactoring your code\(Hope this would never happen\). 

## Step2. Create a feature branch on your local machine

* Create local branch on your machine and then start developing, workflow could see this [page](develop-components-and-test-them.md#1-start-developing)
* After coding please test your component to see if that works well, follow [this](develop-components-and-test-them.md#4-1-test-the-performance-on-web-browser) to start your storybook



## Step3. Publish Pull Request\(pr\) after developing

* In your PR description, please list all the changes you made,  which will help people to review your code
* It will be wonderful if you also mention the issue number your create in Step1 

## Step4. Commit to master with a version change \(Platform Team will do this\)

From this step, Platform team members will take over the rest works.

* People who review codes will test its function as well on web and native
* Once pass the test, he will make a version change commit

This commit should only include a `package.json` file updated and the commit message should also follow the pattern shown in the picture. In commit message, **there is nothing but a version number**

![Example of right commit message](../.gitbook/assets/image%20%2818%29.png)

Some changes can only infect the minor number. In this example,  previous version is `0.1.0-alpha.169`,

The **right naming** should be:  `0.1.0-alpha.170` 

The wrong naming could be :  `0.1.1-alpha.169`,    `0.1.0.170`,  `0.2.0-alpha.169`, `0.2`

## Step5. Publish to NPM  \(Platform Team will do this\)

After step4, Platform team member will publish the new version of Bappo-component

```bash
cd ./bappo-open/packages/bappo-components

#Make sure you are in the right folder before publish
npm publish
```

```bash
cd ./bappo-open/packages/bappo-components

#Make sure you are in the right folder before publish
npm publish
```



