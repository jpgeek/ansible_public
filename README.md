# `ansible_public`

Zergsoft public collections of Ansible roles.
Ansible collections are stored under `jpgeek/<role-name>`.

## Build Collection Artifact

Inside the collection directory, run:
    cd collections/jpgeek/utilities
    ansible-galaxy collection build

This generates a .tar.gz file, which is the collection artifact.

## Publish to Galaxy:
Upload the built artifact to Ansible Galaxy using:

    ansible-galaxy collection publish <path_to_tarball>

You'll need an API token from Galaxy for this.
