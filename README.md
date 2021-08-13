# EasyBuild helpers

These helpers accompany my [blog post on setting up EasyBuild environments](https://blog.entek.org.uk/notes/2021/07/29/setting-up-easybuild-environments.html)

Please refer to that post for detailed background and development information.

## Brief usage

This refers to another blog post on [OS detection with Lmod](https://blog.entek.org.uk/notes/2021/07/27/platform-detection-with-lmod.html), for the bash variables HPC_OS_SHORT and HPC_ARCH_CPU_SHORTNAME.  You can substitute these with something else, if you do not have platform detection available.

To setup from scratch, first download the sources:

```bash
mkdir -p /apps/easybuild/sources
eb-download --dependencies /apps/easybuild/sources
```

Then prepare the main branch:

```bash
eb-toolchain-bootstrap --create-easybuild-sources-folder /apps/easybuild/2020b
# Initialise for the current platform (using the platform detection in hpc_environment module, e.g. EL-7-sky or Deb-10-has)
eb-platform-init --easybuild-source-path=/apps/easybuild/2020b/sources --install-sources=/apps/easybuild/sources /apps/easybuild/2020b/$HPC_OS_SHORT-$HPC_ARCH_CPU_SHORTNAME
```

And, for a development branch with it’s own easyconfig tree:

```bash
eb-toolchain-bootstrap --install-sources=/apps/easybuild/sources --clone-easyconfigs /apps/easybuild/2020b-some-app-test
# Initialise for current platform, using the base configuration's source space
eb-platform-init --easybuild-source-path=/apps/easybuild/2020b/sources --install-sources=/apps/easybuild/sources /apps/easybuild/2020b-some-app-test/$HPC_OS_SHORT-$HPC_ARCH_CPU_SHORTNAME
```

