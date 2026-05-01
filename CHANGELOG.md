## 2.0.0 (May 1, 2026)

**Features:**

  - Added a new `dockctl redeploy` command that restarts stacks without pulling new images.
  - Updated all commands to consider an new `/var/lib/dockctl/.dockctl.secret` file that expects the repositories in format `registry:username:password`. This allows for `docker login` before pulling images from private repositories.
  - Updated `dockctl update` command to take the stack names to just update/redeploy/stop only those stacks.

## 1.0.0 (February 7, 2022)

**Features:**

  - Converted `docker-compose` command from v1 to v2.

## 0.0.2 (October 26, 2021)

**Bugfixes:**

  - Updated system home directory for `dockctl`
  - Minor typo fixes and other improvments. 

## 0.0.1 (October 25, 2021)

**Features:**

  - Initial release.
