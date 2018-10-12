## Secrets

### Example Handling

* Hard-coded into the source code
  - Not a good idea
* Entered via the command line
  - Somebody has to enter the secret,
    how to remember?
* Obtained from a configuration file
  - Don't put in the SCM
* Received from environment variables
  - setting environment in script?
* Via user-provided services
  - vulnerable for attacks on the service
* By mounted volumes
  - shared by containers

### Examples of types

* Username/Passwords
* DB connection strings
* Cryptographic keys
* API keys
* OAuth 2.0
