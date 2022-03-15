# Updating TECkit in Encoding Converters Core

- cd encoding-converters-core
- git checkout -b TECkit20yy
- cp -p -v ../TECkit-*/32-bit/* redist/32bit/
- cp -p -v ../TECkit-*/64-bit/* redist/64bit/
- cp -p -v ../TECkit-*/Documentation/*.pdf redist/Help/

# Building Ubuntu packages for PSO

umask 022

## Before inclusion in Debian

### bionic

- code debian-src/changelog
- _append `+18.04.1` to version_
- ./build-linux-package.sh
- code ~/.pbuilderrc
- _enable restricted and universe for COMPONENTS_
- DISTRIBUTIONS=bionic pbuilder-pso build-multi teckit-linux/*.dsc

### Source

- ./build-linux-package.sh -S
- pbuilder-pso sign teckit-linux/*.changes
- pbuilder-pso upload-multi teckit-linux/*.changes

## After inclusion in Debian

- git clone https://salsa.debian.org/tex-team/teckit.git
- git branch upstream
- git rm debian/*.symbols # better would be dpkg-gensymbols
- code debian/copyright
- git commit -a -m "Update packaging for new upstream release"

### focal

- repack tarball to teckit-2.5.10+20.04.tar.gz
- gbp import-orig teckit-2.5.10+20.04.tar.gz
- dch -i
- _append `+20.04-1` to version_
- gbp buildpackage

### after focal

- _replace 2.5.10 with the current TECkit release version_
- _replace 20.04 in the instructions above with the correct release date_
