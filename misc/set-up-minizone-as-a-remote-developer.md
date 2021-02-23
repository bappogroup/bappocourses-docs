# Set Up Minizone \(as a remote developer\)

You can boot up the entire Bappo on your local machine for easier development, we call it "minizone". With a minizone you can get latest development changes or even modify the codebase yourself.

### Steps

1. Install and configure docker. One approach is to use docker desktop: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

2. Install aws cli version 1  
[https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html\#install-macosos-bundled](https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html#install-macosos-bundled)

3. Configure aws crendentials  
You'll be provided with a `credentials` file. Put it under **`~/.aws/credentials`** \(Linux & Mac\) or **`%USERPROFILE%\.aws\credentials`** \(Windows\).  
Note: `credentials`is a file containing plain text like:

```text
[default]
aws_access_key_id=YOUR_ACCESS_KEY
aws_secret_access_key=YOUR_SECERT_KEY
```

Verify the credentials are correctly set - restart terminal and run 

```text
aws sts get-caller-identity --query Account --output text
```

If result is 676666413781 then you're good.

4. Install dependencies by running `yarn install` under `bappo-web`, `bappo-api` and the root folder

5. Go to `minizone` and run `./launch-ci.sh`

6. Open Keychain Access on Mac. Select login and All Items on the left. Then drag file `minizone/nginx/conf.d/cert.pem` into the right-hand side.

![Keychain Access 1](../.gitbook/assets/image%20%2822%29.png)

   7. You should see an item added to the list. Right click it and select "Get Info".

![Keychain Access 2](../.gitbook/assets/image%20%2823%29.png)

   8. Expand "Trust" and select "Always Trust" in the dropdown next to "When using this certificate". Then close the popup. The system will ask for your password to save this change.

![Keychain Access 3](../.gitbook/assets/image%20%2821%29.png)

   9. You're done!  
Run `docker ps` and you should see these containers up and running:  


![List of container names](../.gitbook/assets/image%20%2825%29.png)

  10. Open a browser and go to your local bappo via `https://local.bappo.com:8080`

### Troubleshooting

1. **Some container is not up** Check Logs from docker. Known reasons include not allocating enough cpu, memory or disk space to docker. 
2. **API response with CORS error** This normally happens when the api server is down. Check the docker logs from api/database/redis container logs. You can first run `docker ps` , then e.g. `docker logs minizone_bappo-api_1` to see logs from a specific container. Sometimes simply relaunching the minizone by `./destroy-local-db.sh` and `./launch-ci.sh` solves the problem.



