# cPanel Ansible QA Roles & Tasks

These are a few Ansible roles and tasks that I have created thus far to facilitate orcastrating specific cPanel
server configurations when our usual automation is not yet implemented or for manual testing teams to use.

## Roles

`set_internal_repo.yaml`
* This simple role will configure the plugin YUM repository (RHEL) or APT source (DEB) to the default internal development repository.
This role makes use of the included tasks to ensure that the custom repositories remain persistent.

`set_plugin_branch.yaml`
* Similar to the previous role, with the ability to specify a custom branch. If a specific development branch is required,
this role prompts the user for the name of the branch and configures the repository while also ensuring its persistence.

`upgrade_cp-version.yaml`
* If a cPanel server requires upgrading to specific versions, the role accepts a full version, makes the necessary configuration
changes and then runs the correct cPanel upgrade script.

## Tasks

* `cpanel/retain_custom_repo.yaml` - This helper module task can be used with any playbook or role that modifies the repository and requires that the changes are persistent.
By default, the cPanel software "fixes" the repositories by ensuring they are always correct, however, custom sources can be used to prevent
modifications from being undone. This task module performs the necessary chagnes to ensure custom repositories remain, simply by providing the 
task with the name of the repository needed to retain.

* `cpanel/run_upcp.yaml` - This task simply runs cPanel's upgrade script (upcp) in a detached mode from Ansible with a default timeout of 1 hour.

* `cpanel/set_cpversion.yaml` - This task allows the modification of the `/etc/cpupdate.conf` file for cPanel servers that allows specific version modifiations.

* `tasks/configure_repository.yaml` - Non-cPanel specific task file that configures a custom YUM/APT repository on the destination host.
