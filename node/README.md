## Information

This Docker file uses by default the 3.5.9 version of [MongoDB NodeJS driver](https://mongodb.github.io/node-mongodb-native/3.5/)
See [MongoDB NodeJS driver QuickStart](https://mongodb.github.io/node-mongodb-native/3.5/quick-start/quick-start/) for more examples.
Alternatively, you can select a specific MongoDB NodeJS driver version by leveraging the `--build-arg` option when building the image.

Note that the given code example has been tested against the default MongoDB Node driver version. There is no guarantee that the code sample with work for all possible versions of the driver.

## Build Steps 

1. Build Docker image with a tag name. Within this directory execute: 
   * For using the latest driver version:
     ```
     docker build . -t mdb-csfle-example
     ```
   This will build a Docker image with a tag name `mdb-csfle-example`. 

2. Run the Docker image by executing:
   ```
   docker run -tih csfle mdb-csfle-example
   ```
   The command above will run a Docker image with tag `mdb-csfle-example` and provide it with `csfle` as its hostname. 

## Execution Steps

Once you're inside the Docker container, you could follow below steps to run the NodeJS code example. 

1. `export MONGODB_URL="mongodb+srv://USER:PWD@EXAMPLE.mongodb.net/dbname?retryWrites=true&w=majority"`
2. `node ./example.js`

If you're connecting to MongoDB Atlas please make sure to [Configure Whitelist Entries](https://docs.atlas.mongodb.com/security-whitelist/)
