# Facter 3

Besides getting all system facts it is possible to name a fact as argument:

```
facter os
```

    {
      architecture => "amd64",
      distro => {
        codename => "jessie",
        description => "Debian GNU/Linux 8.2 (jessie)",
        id => "Debian",
        release => {
          full => "8.2",
          major => "8",
          minor => "2"
        }
      },
      family => "Debian",
      hardware => "x86_64",
      name => "Debian",
      release => {
        full => "8.2",
        major => "8",
        minor => "2"
      },
      selinux => {
        enabled => false
      }
    }
