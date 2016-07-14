# debian8-php
Vagrant configuration file for web development using PHP on Debian 8 (64 bit).

- Debian 8 (64 bit)
- PHP 7
- Apache

To use this configuration, place any files that Apache should serve in a
directory named `public`, located in the project's root directory.

The debian box uses `rsync` rather than the VirtualBox synchronization features.
To sync the shared directory, run `vagrant rsync-auto` after `vagrant up`.
