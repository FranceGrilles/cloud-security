# cloud-security

Patch and policy files intended for the OpenStack nova services to avoid user
interaction in the same project/tenant.

## Setup / Installation

To deploy the patch, you must :

 * Update your `/etc/nova/policy.json` to define which actions
   that can't be performed by another user (see `policy` directory). An
   sample of this policy file is provided in the `nova` directory.
   If you are running Ubuntu server, you can generate the file with the following command:

```
     # oslopolicy-policy-generator --namespace nova
```
 * Patch original files if you are running kilo or a newer version to ensure
   that the policy rules defined will be enforced (see below)
 * Restart openstack-nova-api

You must apply each files of the `patch` directory for your version by selecting the right branch. The patches must be applied from the root directory (```/```) :

```
 # cd /
 # patch -p0 < nova-isolation-same-tenant.patch
```
You can add `-b` to the patch command to make a backup
You can add `--dry-run` to the patch command to make a simulation

NOTES:

 * The patchs are organized in branches you may checkout the correct
   version to fit your installation. The kilo/liberty/mitaka branch are
   for CentOS 7. For Ubuntu, you have the full version name of your package.
 * Updates to policy.json files are applied instantly

If you have any issue, feel free to leave a comment here !
