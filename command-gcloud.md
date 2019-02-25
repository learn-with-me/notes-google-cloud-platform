# Command: GCloud

Just like we can access terminal/prompt in our local computers, GCP lets you access its terminal called `Cloud Shell`. We can connect to cloud shell by:

* Either our own terminal
* Or Cloud shell from the GCP GUI

To be able to call GCP APIs, it has a command called `gcloud`.

#### Common usage

###### Setup and Authentication

```
$ gcloud version
$ gcloud info --show-log
$ gcloud init <project>

Verification
$ gcloud config list                        # List all the config except the default ones
$ gcloud config list --all                  # Lists all the configs including defaults
$ gcloud config set project <project-id>

Authentication
$ gcloud auth login
$ gcloud auth list                            # List all the accounts you're signed-in with
$ gcloud config set account <account>         # Switch between logins

Activate Service Account in local terminal
gcloud auth activate-service-account <service_name>  --key-file <key_file_path>
```

###### Application

```
$ gcloud init                          # Initializes current folder into a gcloud project and setup links
$ gcloud app deploy                    # Deploy your app in cloud App engine
$ gcloud app deploy app.yaml           # Deploy app with specific configurations
$ gcloud app browse                    # Open the application page in browser
                                         # or visit http://YOUR_PROJECT_ID.appspot.com
$ gcloud app describe                  # Displays GCloud app information
```

###### Beta Functions

```
$ gcloud beta functions list                            # List all the cloud functions in the project
$ gcloud beta functions describe <name>                 # Describe a cloud function from the project
$ gcloud beta functions logs read <name>                # Read logs for a function
$ gcloud beta functions deploy <name> --trigger-http    # Deploy to production
$ gcloud beta functions deploy psHelloHTTP --entry-point <name> --trigger-http
$ gcloud beta functions deploy <name> --trigger-topic <topicName>
$ gcloud beta functions call psHelloHTTP --data={"message": ""}
```

###### Help

```
$ gcloud -h                            # Lists all the available commands and command groups
$ gcloud --help                        # Detailed information on commands
$ gcloud help compute instances create # Help on specific command combination
```

#### Deployment

###### Basic

```
$ gcloud deployment-manager deployments list
$ gcloud deployment-manager deployments describe platform-qa-deployment
```



