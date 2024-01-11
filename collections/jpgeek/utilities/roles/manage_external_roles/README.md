# Overview
Extract specific versions of specific roles from arbitrary git repositories.
This allows creating a single repository with (for example) a "roles" directory
which can contain arbitrary collections of roles.  The roles are then copied
into the current ansible playbook/ project.

# Motivation
Many roles are not public and do not belong in Galaxy.  This allows using any
git repository to manage these roles without setting up a local Galaxy server
or reverting to git sub repositories.

Further, it is much safer to pin a playbooks dependencies to specific versions
of roles.

# Usage
Add `{playbook_dir}/tmp/` to your .gitignore.
Add `{playbook_dir}/external_roles/` to your .gitignore.

To use this role in your playbook, define the `external_roles_repos` variable in
your playbook with the necessary details.


            # playbook.yml
            ---
            - hosts: localhost
              gather_facts: no
              roles:
                - manage_external_roles
              vars:
                external_roles_repos:
                  - name: repo1
                    url: https://yourcompany.com/git/repo1.git
                    roles:
                      - name: role1
                        version: abc
                        path: path/to/role1
                  - name: repo2
                    url: https://yourcompany.com/git/repo2.git
                    roles:
                      - name: role2
                        version: def
                        path: path/to/role2

The path is relative to the root of the repository.

