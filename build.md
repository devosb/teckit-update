# Building Ubuntu packages for PSO

umask 022

## Before inclusion in Debian

### xenial

- code code debian-src/changelog
- _append `+16.04.1` to version_
- ./build-linux-package.sh
- DISTRIBUTIONS=xenial pbuilder-pso build-multi teckit-linux/*.dsc

### bionic

- code code debian-src/changelog
- _append `+18.04.1` to version_

#### Source

- ./build-linux-package.sh -S
- pbuilder-pso sign teckit-linux/*.changes
- pbuilder-pso upload-multi teckit-linux/*.changes

#### Binary

- ./build-linux-package.sh
- code ~/.pbuilderrc
- _enable restricted and universe for COMPONENTS_
- DISTRIBUTIONS=bionic pbuilder-pso build-multi teckit-linux/*.dsc

## After inclusion in Debian

- git clone https://salsa.debian.org/tex-team/teckit.git
- git branch upstream
- git rm debian/*.symbols # better would be dpkg-gensymbols
- code debian/copyright
- git commit -a -m "Update packaging for new upstream release"

## eoan

- repack tarball to teckit-2.5.10+19.10.tar.gz
- gbp import-orig teckit-2.5.10+19.10.tar.gz
- dch -i
- _append `+19.10-1` to version_
- gbp buildpackage

## focal

- repack tarball to teckit-2.5.10+20.04.tar.gz
- gbp import-orig teckit-2.5.10+20.04.tar.gz
- dch -i
- _append `+20.04-1` to version_
- gbp buildpackage
