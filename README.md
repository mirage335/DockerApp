Copyright (C) 2017 mirage335
See the end of the file for license conditions.
See license.txt for DockerApp license conditions.

Docker base/image/container management infrastructure, intended for standalone applications. See "gui" for a paricularly advanced use case, involving X11 GUI applications with fileparameter translation.

# Purpose

Applications often depend on conflicting libraries or configuration files. Notable examples include Firefox ($HOME/.mozilla) and Arduino ($HOME/.Arduino).
 
Docker solves this problem for command-line applications that use their own data.
 
DockerApp solves this problem for applications that have a GUI (X11) user interface, and read/modify/execute random files (eg. $HOME/Downloads ./sketch/sketch.ino).

# Installation
Run/setup the "gui" DockerApp to install "dexe" to ~/bin .

# Usage

```
cd ./dockerfiles/unimportant-hello-scratch
./anchor _setup
./anchor
./anchor _run /hello
cd ..

cd ./dockerfiles/gui
./anchor ./test/testfile ./test/testfile
#Should see xeyes launched from the script in the "./test" directory automatically shared with the container.
cd ..
```

# Dependencies

Base image creation requires "mkimage.sh" script. Simply clone docker to a neighboring, or higher up, directory.
git@github.com:docker/docker.git

# Design

Complex structure of shell script may seem excessive, but emphasizes scalability to more powerful solutions.

# Features

* Override internal functionality with 'ops' script.
* Resources (ie. images/containers) automatically given unique names derived from application directory.
* Symlink compatibility. Both launch and anchor scripts may be called as a symlink at ~/bin/appName .

# Ratings

* Application directory naming must follow the naming convention container[-image][-base] .
* Unique names are required for all application container/image combinations, even if different bases are used.
* Characters not allowed by filename (ie. :/) may be used through an accompanying "ops" script. Consider unimportant-hello:mirage335_debian_jessie-mirage335/debian:jessie .
* Specifying identical base/image names should result in the container being directly based, without an intermediate image. Doing so may complicate committng and backing up container changes.

# SAFETY

* Despite the _safeRMR wrapper, incidents are still theoretically possible, and commands like "rm -rf" are ultimately used. Be careful.
* Resources called by this script (ie. mkimage) are untrusted. Carefully verify these scripts before using on production systems.

# FutureWork

* Backup of working container to image stored in application directory. Completion of load/save/modify image functions.




# Copyright
This file is part of DockerApp.

DockerApp is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

DockerApp is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with DockerApp.  If not, see <http://www.gnu.org/licenses/>.
