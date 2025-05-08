#self-taught 
Advanced Packaging Tool è il packet manager delle [[Linux]] distro [[Debian]], e suoi derivati ([[Ubuntu]] ecc).
```bash
apt search foo # search for foo in repository
apt-file search foo # search for packages that provide foo
aptitude # launched apts frontend
synaptic # other apt frontend
apt show foo # show install status and metadata for foo
apt-file --list foo # show all files included in foo
apt update
apt upgrade (-y)
apt install foo (-y)
apt remove foo
apt purge foo # uninstall foo and remove its configuration files
apt download foo # download foo to current directory, without installing
apt depends foo (--installed) # show all dependencies for foo, --installed shows only the installed ones
apt source foo # download the source code for foo
apt autoremove # removes unneeded package files from cache
apt autoclean # removes outdated package files from cache
apt clean # removes all package files from cache
apt -f install # fixes broken dependencies by installing missing ones or removing problematic ones
apt build-dep foo # installs build depencencies for foo
add-apt-repository -L (-s) # lists configured repositories, -s to included source repositories
egrep -r --include '*.list' '(deb|deb-src) ' /etc/apt/sources.list* # lists all registered repositories
add-apt-repository powertools # enable repository powertools
add-apt-repository -U https://example.com/updates/x86_64 # add and enable repo (URL target must contain a valid repodata/repomd.xml file)
```