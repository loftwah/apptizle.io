# apptizle.io

I'm not 100% what this is for now but it will be fun :)

## Getting started

You will need a fresh install of Ubuntu 20.04 or similar. I will be using Ubuntu 20.04 for this project so if you are using a different operating system, or distro you'll need to adjust accordingly.

### Install dependencies

Download the install script and install Docker.

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Once Docker is running and you are happy with it, set up Appwrite.

```shell
docker run -it --rm \
    --volume /var/run/docker.sock:/var/run/docker.sock \
    --volume "$(pwd)"/appwrite:/usr/src/code/appwrite:rw \
    --entrypoint="install" \
    appwrite/appwrite:0.10.4
```

Appwrite should be up and running now, and you can view it on localhost with the port you have set. The dashboard for a new project should look like this.

![chrome_1c2mloGpRr](https://user-images.githubusercontent.com/19922556/135816109-38305986-8e52-4f57-b8ab-bbb2f0944896.png)

To use with NPM (node package manager) you can use the following command. I suggest creating a directory for your project.

```shell
npm install appwrite
```

Or for webpack

```json
import { Appwrite } from "appwrite";
```

Or to simply use it from a CDN for playing around, or just developing

```html
<script src="https://cdn.jsdelivr.net/npm/appwrite@4.0.3"></script>
```

An example of using the Appwrite SDK in JavaScript

```javascript
// Init your Web SDK
const appwrite = new Appwrite();

appwrite
    .setEndpoint('http://localhost:8098/v1') // Your Appwrite Endpoint
    .setProject('1337h4x0r') // Your project ID

// Register User
appwrite
    .account.create('dean@deanlofts.xyz', 'Password01', 'Dean Lofts')
        .then(response => {
            console.log(response);
        }, error => {
            console.log(error);
        });

// Subscribe to files channel
appwrite.subscribe('files', response => {
    if(response.event === 'storage.files.create') {
        // Log when a new file is uploaded
        console.log(response.payload);
    }
});
```
