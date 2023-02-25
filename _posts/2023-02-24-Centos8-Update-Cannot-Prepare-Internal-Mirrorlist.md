---
published: true
header:
  overlay_image: #/assets/images/rocky-mtns.jpg
  caption: #"[CC License](https://creativecommons.org)"
categories:
        #- Testing
---
Recently when installing Centos8 Streams onto a bare metal 'server' I was getting an error that wouldn't allow me to update the system.  

# Error Message
```
$ sudo dnf update
CentOS Linux 8 - AppStream                                                                                                                             73  B/s |  38  B     00:00
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist
```

Checking the list of repos:
```
$ sudo dnf repolist
repo id                                                                            repo name
appstream                                                                          CentOS Linux 8 - AppStream
baseos                                                                             CentOS Linux 8 - BaseOS
extras                                                                             CentOS Linux 8 - Extras
```
It turns out the fix is a simple one line command:
```
$ sudo dnf --disablerepo '*' --enablerepo=extras swap centos-linux-repos centos-stream-repos
```

Once this was run it removes the older 'centos-linux-repos' and installs the 'centos-stream-repos' repo.
```
CentOS Linux 8 - Extras                                                                                                                                12 kB/s |  11 kB     00:00
Dependencies resolved.
======================================================================================================================================================================================
 Package                                             Architecture                           Version                                   Repository                                 Size
======================================================================================================================================================================================
Installing:
 centos-stream-repos                                 noarch                                 8-3.el8                                   extras                                     19 k
Removing:
 centos-linux-repos                                  noarch                                 8-3.el8                                   @anaconda                                  26 k

Transaction Summary
======================================================================================================================================================================================
Install  1 Package
Remove   1 Package

Total download size: 19 k
Is this ok [y/N]: y
Downloading Packages:
centos-stream-repos-8-3.el8.noarch.rpm                                                                                                                 82 kB/s |  19 kB     00:00
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                  55 kB/s |  19 kB     00:00
CentOS Linux 8 - Extras                                                                                                                               1.6 MB/s | 1.6 kB     00:00
Importing GPG key 0x8483C65D:
 Userid     : "CentOS (CentOS Official Signing Key) <security@centos.org>"
 Fingerprint: 99DB 70FA E1D7 CE22 7FB6 4882 05B5 55B3 8483 C65D
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
Is this ok [y/N]: y
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                              1/1
  Installing       : centos-stream-repos-8-3.el8.noarch                                                                                                                           1/2
  Erasing          : centos-linux-repos-8-3.el8.noarch                                                                                                                            2/2
  Verifying        : centos-stream-repos-8-3.el8.noarch                                                                                                                           1/2
  Verifying        : centos-linux-repos-8-3.el8.noarch                                                                                                                            2/2

Installed:
  centos-stream-repos-8-3.el8.noarch
Removed:
  centos-linux-repos-8-3.el8.noarch

Complete!
```

Following this a standard update/upgrade runs fine.

<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

