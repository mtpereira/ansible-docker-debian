Docker Debian
========

A role for installing Docker in Debian Wheezy.

Wheezy has 2 dependencies missing for docker: golang >= 1.2 and linux kernel >= 3.8.0. This role builds and installs golang 1.2 packages from deb source and installs the newest kernel from wheezy-backports.

Oh, and also installs docker. :)

Requirements
------------

None.

Role Variables
--------------

* `docker_debian_go_build_dir`: Directory where the golang packages will be built. Defaults to `/tmp/golang`.
* `docker_debian_go_build_arch`: Architecture for the binary golang packages. Defaults to `amd64`.
* `docker_debian_go_build_system`: Architecture for `dpkg-buildpackage`. Defaults to `x86_64-linux-gnu`.
* `docker_debian_kernel_arch`: Backport kernel architecture. Defaults to the value of `docker_debian_go_build_arch`.

Dependencies
------------

None, but using **mtpereira.common** or a similar role is recommended.

License
-------

MIT

Author Information
------------------

[GitHub project page](https://github.com/mtpereira/ansible-debian-docker)

[Manuel Tiago Pereira](http://mtpereira.github.io)
