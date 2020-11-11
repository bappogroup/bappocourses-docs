# Set Up Minizone \(as a remote developer\)

You can boot up the entire Bappo on your local machine for easier development, we call it "minizone". With a minizone you can get latest development changes or even modify the codebase yourself.

### Steps

1. Install and configure docker. One approach is to use docker desktop: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. You'll be provided with a `credentials` file. Put it under **`~/.aws/credentials`** \(Linux & Mac\) or **`%USERPROFILE%\.aws\credentials`** \(Windows\).
3. Install dependencies by running `yarn install` under `bappo-web`, `bappo-api` and the root folder
4. Go to `minizone` and run `./launch-ci.sh`





