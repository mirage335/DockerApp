# Example
./anchor ./test/testfile ./test/testfile

# Cavets

* Images may portably create new containers. Containers themselves cannot easily provide persistent and portable file permissions matching their hosts. Applications performing oneshot operations (eg. Arduino) are ideal for seamless permissions transparency, using temporary, nonpersistent containers. Servers should rely strictly on internal services (eg. SSH, headless VNC), using semantics to find open ports on the host.

* Any configuration globally required to run the app with appropriate features (ie. Arduino libraries) must be committed back to the *image*, not the container. Docker does not allow passing of any new environment variables or commands when launching existing containers.

* Synchronization of user id numbers requires useradd, and gosu operatons. Consequently, any files owned by the internal user within docker container, must either be created with appropriate ownership (ie. useradd -m), or set to correct ownership (ie. chown -R). Installing files to /etc/skel and shared folders are valid workarounds.

