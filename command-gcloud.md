# Command: GCloud

Just like we can access terminal/prompt in our local computers, GCP lets you access its terminal called `Cloud Shell`. We can connect to cloud shell by:

* Either our own terminal
* Or Cloud shell from the GCP GUI

To be able to call GCP APIs, it has a command called `gcloud`.

#### Common usage

###### Setup and Authentication

```
$ gcloud version
$ gcloud auth login
$ gcloud info --show-log
$ gcloud config set project <project-id>
$ gcloud init <project>

Verification
$ gcloud auth list
$ gcloud config list                        # List all the config except the default ones
$ gcloud config list --all                  # Lists all the configs including defaults
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
$ gcloud beta functions list                # List all the cloud functions in the project
$ gcloud beta functions describe <name>     # Describe a cloud function from the project
$ gcloud beta functions logs read <name>    # Read logs for a function
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



