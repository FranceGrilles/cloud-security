# cloud-security

Config files and helpers to implement security inside an OpenStack project/tenant.

## Setup / Installation

We provide a custom wrapper to check autorizations between two users of the same project/tenant :

https://github.com/FranceGrilles/monitoring-cloud

For these tests to work, you must :
 * update your /etc/nova/policy.json to ensure that some actions won't be performed by another user (see `policies` directory)
 * patch some of the original files if you are running kilo or a newer version (see `patch` directory)
```
# cd / && patch -p0 < correct_version_of_the_patch
```
You can add `-b` to the patch command to make a backup
You can add `--dry-run` to the patch command to make a simulation
