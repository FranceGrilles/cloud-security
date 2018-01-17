# cloud-security

Patch and policy files intended for the OpenStack nova, cinder, glance and
horizon services to avoid user interaction in the same project/tenant.

The `13.1.4-0ubuntu4.1` branch has been designed for:

* python-nova-13.1.4-0ubuntu4.2
* python-cinder-8.1.1-0ubuntu3
* python-glance-12.0.0-ubuntu2
* openstack-dashboard-9.1.2-0ubuntu3

## Setup / Installation

To deploy the patch, you must :

 * Update your `/etc/[cinder,nova,glance]/policy.json` to define which actions
   that can't be performed by another user (see `policy` directory).
 * update `/etc/openstack-dashboard/[cinder,nova,glance]_policy.json`
 * Patch original Python files to ensure that the policy rules defined will be
   enforced (see below)
 * Restart `nova-api`, `cinder-api`,
   `glance-api` and `apache2` services`

You must apply each files of the `patch` directory for your version by selecting the right branch. The patches must be applied from the root directory (```/```):

```
 # cd /
 # patch -p0 < nova-isolation-same-tenant.patch
 # patch -p0 < cinder-isolation-same-tenant.patch
 # patch -p0 < glance-isolation-same-tenant.patch
 # patch -p0 < horizon-isolation-same-tenant.patch
```
You can add `-b` to the patch command to make a backup
You can add `--dry-run` to the patch command to make a simulation

NOTES:

 * The patchs are organized in branches you may checkout the correct
   version to fit your installation. The kilo/liberty/mitaka branch are
   for CentOS 7. For Ubuntu, you have the full version name of your package.
 * Updates to policy.json files are applied instantly

If you have any issue, feel free to leave a comment here !
