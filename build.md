# Updating TECkit in Encoding Converters Core

- cd encoding-converters-core
- git checkout -b TECkit20yy
- cp -p -v -f ../TECkit-2.5.??/32-bit/* redist/32bit/
- cp -p -v -f ../TECkit-2.5.??/64-bit/* redist/64bit/
- cp -p -v -f ../TECkit-2.5.??/Documentation/*.pdf redist/Help/
- git commit -a -m "Update to TECkit 2.5.?? released in 20yy"

# Building Ubuntu packages for PSO

umask 022

- git clone https://salsa.debian.org/tex-team/teckit.git
- git branch upstream
- git rm debian/*.symbols # better would be dpkg-gensymbols
- code debian/copyright
- git commit -a -m "Update packaging for new upstream release"

## package

- repack tarball to teckit-2.5.10+20.04.tar.gz
- gbp import-orig teckit-2.5.10+20.04.tar.gz
- dch -i
- _append `+20.04-1` to version_
- gbp buildpackage

## build and upload

- DISTS=focal pbuilder-pso build result/teckit_2.5.10+20.04-1.dsc
- remove `*.ddeb` from `*.changes` and filesystem in `~/pbuilder` tree
- pbuilder-pso sign
- pbuilder-pso upload-multi

## after focal

- _replace 2.5.10 with the current TECkit release version_
- _replace 20.04 in the instructions above with the correct release date_
- _replace focal in the instructions above with the correct release name_
