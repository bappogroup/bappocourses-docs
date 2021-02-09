# Set Up Minizone \(as a remote developer\)

You can boot up the entire Bappo on your local machine for easier development, we call it "minizone". With a minizone you can get latest development changes or even modify the codebase yourself.

### Steps

1. Install and configure docker. One approach is to use docker desktop: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Install aws cli version 1 [https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html\#install-macosos-bundled](https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html#install-macosos-bundled)
3. You'll be provided with a `credentials` file. Put it under **`~/.aws/credentials`** \(Linux & Mac\) or **`%USERPROFILE%\.aws\credentials`** \(Windows\).
4. Install dependencies by running `yarn install` under `bappo-web`, `bappo-api` and the root folder
5. Go to `minizone` and run `./launch-ci.sh`
6. Open Keychain Access on Mac. Select login and All Items on the left. Then drag file `minizone/nginx/conf.d/cert.pem` into the right-hand side.

![Keychain Access 1](../.gitbook/assets/image%20%2822%29.png)

   6. You should see an item added to the list. Right click it and select "Get Info".

![Keychain Access 2](../.gitbook/assets/image%20%2823%29.png)

   7. Expand "Trust" and select "Always Trust" in the dropdown next to "When using this certificate". Then close the popup. The system will ask for your password to save this change.

![Keychain Access 3](../.gitbook/assets/image%20%2821%29.png)

   8. You're done!  
Run `docker ps` and you should see these containers up and running:  


![List of container names](../.gitbook/assets/image%20%2825%29.png)

### Troubleshooting

1. **Some container is not up** Check Logs from docker. Known reasons include not allocating enough cpu, memory or disk space to docker. 



