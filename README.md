# cloud-security

Patch and policy files intended for OpenStack cinder, nova and horizon services
to avoid user interaction in the same project/tenant.

## Setup / Installation

We provide a custom wrapper to check autorizations between two users of the
same project/tenant :

https://github.com/FranceGrilles/monitoring-cloud

Note that these tests are already set up for registered FG-Cloud sites via our
monitoring service (ccnagboxfg).

For these tests to work, you must :
 * update your `/etc/[cinder,nova]/policy.json` to define which actions that 
   can't be performed by another user (see `policy` directory)
 * update `/etc/openstack-dashboard/[cinder,nova]_policy.json`
 * patch original files if you are running kilo or a newer version to ensure
   that the policy rules defined will be enforced (see below)
 * restart openstack-nova-api and openstack-cinder-api services

You must apply each files of the `patch` directory for your current branch
(kilo/liberty) for every concerned service on every concerned server.

```
## Patches must be applied from the root directory '/' :
# cd / 
# patch -p0 < nova-isolation-same-tenant.patch
# patch -p0 < cinder-isolation-same-tenant.patch
# patch -p0 < horizon-isolation-same-tenant.patch
```
You can add `-b` to the patch command to make a backup
You can add `--dry-run` to the patch command to make a simulation

NOTES : 
 * The patchs are organized in branches you may checkout the kilo/liberty
   branch to see the patch and policy files
 * Each `policy.json` has its suffixed equivalent `policy.json.orig` to show
   the differences between the original and modified files
 * Updates to policy.json files are applied instantly

These patches have been tested on CentOS7 with a package installation.

If you have any issue, feel free to leave a comment here !
