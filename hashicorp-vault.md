# HashiCorp Vault

> https://learn.hashicorp.com/vault

### Basics

Steps to setup Vault

```
Install the vault on local computer
https://www.vaultproject.io/downloads.html

Set the path
$ export PATH=$PATH:/Users/anshul/Tools

Install auto-completions
$ vault -autocomplete-install

Restart the shell
$ exec $SHELL
```

Starting the server

```
$ vault server -dev

Launch a new terminal session, since vault server runs in foreground
Now copy the following commands from the server in previous tab and execute
1. export VAULT_ADDR='http://127.0.0.1:8200'
2. export VAULT_DEV_ROOT_TOKEN_ID="s.rFNLzmWATEJO5VgF10SccS9q"

Verify the server is running
$ vault status
```

Writing a secret

```
$ vault kv put secret/hello foo=world
$ vault kv put secret/hello foo=world excited=yes
$ vault write kv/my-secret value="s3c(eT"            # write is same as kv put

$ vault list kv                                      # Display all key-value pairs
```

Getting a secret

```
$ vault kv get secret/hello
$ vault kv get -field=excited secret/hello      # Fetch specific attribute
$ vault kv get -format=json secret/hello        # Json formatted output
```

Delete a secret

```
$ vault kv delete secret/hello
```

### Secret Engines

The path prefix tells Vault which secrets engine to which it should route traffic. When a request comes to Vault, it matches the initial path part using a longest prefix match and then passes the request to the corresponding secrets engine enabled at that path.

By default, Vault enables a secrets engine called kv at the path secret/. The kv secrets engine reads and writes raw data to the backend storage. Vault supports many other secrets engines besides kv.

Enable/Disable a secret engine

```
$ vault secrets enable -path=kv kv    # enable another instance of the kv secrets engine at a different path
$ vault secrets enable kv             # Same as above, since path defaults to name of the secrets engine
$ vault secrets list                  # List out all the secret engines enabled on all paths
$ vault secrets disable kv/           # disable instance of kv secrets engine
```

### Dynamic Secrets

Dynamic secrets are generated when they are accessed. Dynamic secrets do not exist until they are read, so there is no risk of someone stealing them or another client using the same secrets. Because Vault has built-in revocation mechanisms, dynamic secrets can be revoked immediately after use, minimizing the amount of time the secret existed.

Enable other secret engines

```
$ vault secrets enable -path=gcp gcp        # Google Cloud secret engine
$ vault secrets enable -path=aws aws        # AWS secret engine
```

Create a Role

A role in Vault is a human-friendly identifier to an action. Vault knows how to create an IAM user via the AWS API, but it does not know what permissions, groups, and policies you want to attach to that user. This is where roles come in - roles map your configuration options to those API calls.

```
$ vault write aws/roles/my-role \
        credential_type=iam_user \
        policy_document=-<<EOF
        ...
```

Generating the secret

```
$ vault read aws/creds/my-role
```

Revoke the secret

```
$ vault lease revoke <leaseID>
$ vault lease revoke aws/creds/my-role/0bce0782-32aa-25ec-f61d-c026ff22106e
```

### Built-in Help

Instead of having to memorize or reference documentation constantly to determine what paths to use, Vault has a built-in help system.

```
$ vault path-help aws
$ vault path-help aws/creds/my-non-existent-role

$ vault path-help gcp
```

### Authentication

Authentication is the mechanism of assigning an identity to a Vault user. When starting the Vault server in dev mode, it automatically logs you in as the root user with admin permissions. In a non-dev setup, you would have had to authenticate first.

Vault has pluggable auth methods, making it easy to authenticate with Vault using whatever form works best for your organization. Example, GitHub auth method.

##### Token

Token authentication is enabled by default in Vault and cannot be disabled. When you start a dev server with vault server -dev, it prints your root token.

```
$ vault token create                                # Create a token
$ vault login s.iyNUhq8Ov4hIAx6snw5mB2nL            # Authenticate with a token
$ vault token revoke s.V6T0DxxIg5FbBSre61y1WLgm     # Revoke a token
$ vault lease revoke                                # Revoke lease on a token
```

By default, this will create a child token of your current token that inherits all the same policies. The "child" concept here is important: tokens always have a parent, and when that parent token is revoked, children can also be revoked all in one operation. This makes it easy when removing access for a user, to remove access for all sub-tokens that user created as well.

##### Auth Methods

Vault supports many auth methods, but they must be enabled before use. Enabling and configuring auth methods are typically performed by a Vault operator or security team.

```
$ vault auth enable -path=github github            # Enable GitHub auth method
$ vault auth enable github                         # Same as above
GitHub auth method we just enabled is accessible at auth/github
$ vault auth disable github                        # Completely disable the GitHub auth method

$ vault auth enable -path=my-github github
This would make the GitHub auth method accessible at auth/my-github

Configure the GitHub auth method. Each auth method has different configuration options.
Configure Vault to pull authentication data from the "zenabi" organization on GitHub.
$ vault write auth/github/config organization=zebani

Tells Vault to map members of team "my-team" (in zenabi) to map to the policies "default" and "my-policy"
$ vault write auth/github/map/teams/my-team value=default,my-policy

$ vault auth list                                  # Find out which auth methods are enabled
$ vault auth help github                           # Help on a auth method
$ vault auth help gcp

$ vault login -method=github                       # Authenticate using GitHub in Vault via personal token
$ vault token revoke -mode path auth/github        # revoke any logins from an auth method
```

### Policies/Authorization

The access control and permissions associated with an identity are authorization. The root and default policies are required policies and cannot be deleted. The default policy provides a common set of permissions and is included on all tokens by default. The root policy gives a token super admin permissions, similar to a root user on a linux machine.

```
$ vault policy fmt my-policy.hcl                # format the policy automatically according to specification
$ vault policy write my-policy my-policy.hcl
$ vault policy write my-policy -<<EOF
    ...
$ vault policy list                             # List policies
$ vault policy read my-policy                   # Read a policy
$ vault token create -policy=my-policy          # Test a policy
$ vault login s.X6gvFko7chPilgV0lpWXsdeu

Mapping Policies to Auth Methods
$ vault write auth/github/map/teams/default value=my-policy

```

### Deploy Vault

How to configure Vault, start Vault, the seal/unseal process, and scaling Vault.





