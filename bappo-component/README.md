# Bappo Component

Please use this workflow when you make contributions to Bappo-Component 

## Step1. Create a feature branch on your local machine

## Step2. Publish Preview Request\(pr\) after developing

## Step3. Commit to master with a version change

Once your code has been merged. On **master** branch,  you are authorised to change Bappo-component version. 

This commit should only include a `package.json` file updated and the commit message should also follow the pattern shown in the picture. In commit message, **there is nothing but a version number**

![Example of right commit message](../.gitbook/assets/image%20%2818%29.png)

Some changes can only infect the minor number. In this example,  previous version is `0.1.0-alpha.169`,

The **right naming** should be:  `0.1.0-alpha.170` 

The wrong naming could be :  `0.1.1-alpha.169`,    `0.1.0.170`,  `0.2.0-alpha.169`, `0.2`

## Step4. Publish to NPM

Go to Bappo-component folder and publish it

```bash
cd ./bappo-open/packages/bappo-components

#Make sure you are in the right folder before publish
npm publish
```



