# Bappo Component

Please use this workflow when you make contributions to Bappo-Component 

## Step1. Came up with an issue on ithub and discuss it

Write an issue [on this page](https://github.com/bappogroup/bappo-open/issues), in which please figure out what kind of bug you found, or what kind of feature for a user story.

Once you have done that. Reach out to discuss it =&gt; find a way to achieve that

## Step2. Create a feature branch on your local machine

develop

test

## Step3. Publish Pull Request\(pr\) after developing

list all feature, refer to which issue

## Step4. Commit to master with a version change \(Platform Team will do this\)

review de ren  test, web ios and android

merg,

 commit version







Once your code has been merged. On **master** branch,  you are authorised to change Bappo-component version. 

This commit should only include a `package.json` file updated and the commit message should also follow the pattern shown in the picture. In commit message, **there is nothing but a version number**

![Example of right commit message](../.gitbook/assets/image%20%2818%29.png)

Some changes can only infect the minor number. In this example,  previous version is `0.1.0-alpha.169`,

The **right naming** should be:  `0.1.0-alpha.170` 

The wrong naming could be :  `0.1.1-alpha.169`,    `0.1.0.170`,  `0.2.0-alpha.169`, `0.2`

## Step5. Publish to NPM  \(Platform Team will do this\)



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



