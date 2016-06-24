# cloud-security

Config files and helpers to implement security inside an OpenStack project/tenant.
Patch and policy files intended for cinder, nova and horizon services to avoid user interaction in the same tenant.

## Setup / Installation

We provide a custom wrapper to check autorizations between two users of the same project/tenant :

https://github.com/FranceGrilles/monitoring-cloud

For these tests to work, you must :
 * update your /etc/[cinder|nova]/policy.json to ensure that some actions won't be performed by another user (see `policies` directory)
 * update /etc/openstack-dashboard/[cinder|nova]_policy.json (see `policies` directory)
 * patch original files if you are running kilo or a newer version (see `patch` directory)

 ```
## Patches must be applied from the root directory '/' :
# cd / && patch -p0 < correct_version_of_the_patch
```
You can add `-b` to the patch command to make a backup
You can add `--dry-run` to the patch command to make a simulation

NOTES : 
 * The patchs are organized in branches you may checkout the kilo/liberty/mitaka branch to see the patch and policy files
 * Each `policy.json` has its suffixed equivalent `policy.json.orig` to show the differences between the original and modified files
