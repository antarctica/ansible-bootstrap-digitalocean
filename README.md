# Bootstrap DigitalOcean (`bootstrap-digitalocean`)

**Part of the BAS Ansible Role Collection (BARC)**

Performs minimal configuration required to enable management of a Digital Ocean droplet (VM) by automated tools

## Overview

* Unless disabled, creates a new OS user, 'controller' for performing privileged actions (such as apt-get install) using sudo or reading log files.
* If enabled, the authorized_keys file for the controller user is set to contain any file in the bootstrap_vagrant_controller_user_authorized_keys_directory directory.

## Availability

This role is designed for internal use but if useful can be shared publicly.

## Usage

### Requirements

#### Other requirements

* As of version **1.0.0** any OS this role is applied to **MUST** ensure passwordless sudo is enabled for the "sudo" group and SSH Agent Forwarding is preserved when using sudo.
    * If basing Droplets off the [BAS DigitalOcean image](https://stash.ceh.ac.uk/projects/BASWEB/repos/digitalocean-base-images), ensure you are using version **0.1.1** or higher, which implements these requirements.
* Public keys which should be added to the `authorized_keys` file of the controller user, each key should be a separate file. Keys should be contained in  `bootstrap_digitalocean_controller_user_authorized_keys_directory`.

### Variables

* `bootstrap_digitalocean_controller_user_username`
	* The username of the controller user, used for management tasks, if enabled
	* This variable **MUST** be a valid UNIX username
	* Default: "controller"
* `bootstrap_digitalocean_controller_user_enabled`
	* If "true" a user for management tasks, termed a controller user, will be created
    * This is a binary variable and **MUST** be set to either "true" or "false" (without quotes).
	* Default: "true"
* `bootstrap_digitalocean_controller_user_authorized_keys_directory`
	* The path, relative to where this role is installed, to the directory that contains the public key files to be added to the controller user's `authorized_keys` file.
	* This variable **MUST** point to a directory, it **MUST NOT** include a trailing `/`.
	* Default: "../../../public_keys"

## Contributing

This project welcomes contributions, see `CONTRIBUTING` for our general policy.

## Developing

### Committing changes

The [Git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) workflow is used to manage development of this package.

Discrete changes should be made within *feature* branches, created from and merged back into *develop* (where small one-line changes may be made directly).

When ready to release a set of features/changes create a *release* branch from *develop*, update documentation as required and merge into *master* with a tagged, [semantic version](http://semver.org/) (e.g. `v1.2.3`).

After releases the *master* branch should be merged with *develop* to restart the process. High impact bugs can be addressed in *hotfix* branches, created from and merged into *master* directly (and then into *develop*).

### Issue tracking

Issues, bugs, improvements, questions, suggestions and other tasks related to this package are managed through the BAS Web & Applications Team Jira project ([BASWEB](https://jira.ceh.ac.uk/browse/BASWEB)).

## License

Copyright 2015 NERC BAS. Licensed under the MIT license, see `LICENSE` for details.
