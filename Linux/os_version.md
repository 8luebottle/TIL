# OS Version
> Check OS Version in Linux

### Table of Contents
- [/etc/os-release](#etcos-release)
- [lsb_release](#lsbrelease)

## `/etc/os-release`

```shell
$cat /etc/os-release
```

- e.g. Check OS Version of a docker container  
  Syntax:
  ```
  $docker exec -it <containerName> <command>
  $cat /etc/os-release
  ```
  Example:
  ```
  $docker exec -it sei-whale /bin/sh
  $cat /etc/os-relase
  ```

  result:
  ```
  PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
  NAME="Debian GNU/Linux"
  VERSION_ID="11"
  VERSION="11 (bullseye)"
  VERSION_CODENAME=bullseye
  ID=debian
  HOME_URL="https://www.debian.org/"
  SUPPORT_URL="https://www.debian.org/support"
  BUG_REPORT_URL="https://bugs.debian.org/"
  ```

[↑ return to TOC](#table-of-contents)

## `lsb_release`
> print distribution specific information.

LSB stands for **L**inux **S**tandard **B**ase.

```shell
$lsb_release -a
```

- e.g.  
  result: 
  ```
  No LSB modules are available.
  Distributor ID:	Debian
  Description:	Debian GNU/Linux 11 (bullseye)
  Release:	11
  Codename:	bullseye
  ```

[↑ return to TOC](#table-of-contents)