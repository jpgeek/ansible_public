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
This task pulls repos into the

    external_roles/repos

directory, checks out the revision or tag specified in the vars file, and then
copies the task from the specified path in to the 

    external_roles/roles

directory.

## .gitignore

In most cases, you should add this to your .gitignore:

    external_roles/

However, you may want to specify only the `external_roles/repos` and check the 
copied `external_roles/roles` code into git.

## `vars/external_roles_vars`

To use this role in your playbook, define the `external_roles_repos` variable in
your playbook with the necessary details.  This can be specified in the 

    vars/external_roles_vars

file or directly in the playbook.  For each repository, you can specify a version
(revision) and then a list of roles to check out from that revision.

The format is:

    external_roles_repos:
      - name: my_git_repo_name   # name of the repository
        url: git@bitbucket.org:MyOrg/my_git_repo_name.git  # url of the repo
        version: abc123 ...                                 # revision or tag

        roles:
          - name: my_role         # name of the role
            path: roles/my_role   # path relative to top directory of repo
          - name: another_role
            path: roles/another_role

      - name: another_git_repo_name
        url: git@bitbucket.org:MyOrg/another_git_repo_name.git
        version: def123 ...

        roles:
          - name: kewl_role
            path: roles/kewl_role
