Docker-Ganglia-Monitor-Mini
==============

## Summary

Repository name in Docker Hub: **[williamyeh/ganglia-monitor-mini](https://registry.hub.docker.com/u/williamyeh/ganglia-monitor-mini/)**

This repository contains Dockerized components of [Ganglia](http://ganglia.sourceforge.net/), including **Ganglia Monitoring Daemon** (**gmond**) and **Ganglia Custom Metric Utility** (**gmetric**), published to the public [Docker Hub](https://registry.hub.docker.com/) via **automated build** mechanism.



## Configuration

This docker image (less than 6 MB in size) contains the following software stack:

- Ganglia Monitoring Daemon (`gmond`).
- Ganglia Custom Metric Utility (`gmetric`).

### Dependencies

Minimal.

- [`williamyeh/dash`](https://registry.hub.docker.com/u/williamyeh/dash/), a Docker image for static DASH (“the Debian Almquist Shell”) without GPLv2 parts.




## Installation

   ```
   $ docker pull williamyeh/ganglia-monitor-mini
   ```


## Usage


#### Show usage

```
$ docker run --rm williamyeh/ganglia-monitor-mini  help
```

#### Start Ganglia Monitoring Daemon (`gmond`)

- Default configuration:
  ```
  $ docker run williamyeh/ganglia-monitor-mini
  ```

- Default configuration with published port:
  ```
  $ docker run      \
      -p 8649:8649  \
      williamyeh/ganglia-monitor-mini
  ```

- Default configuration with higher debug level:
  ```
  $ docker run williamyeh/ganglia-monitor-mini  \
      gmond --debug 2
  ```

- Customized configuration:
  ```
  $ docker run         \
      -v $(pwd):/etc   \
      williamyeh/ganglia-monitor-mini  \
        gmond --conf /etc/gmond.conf
  ```

#### Start Ganglia Custom Metric Utility (`gmetric`)


1. First, start the gmond with `--name`:

   ```
   $ docker run  --name gmond  \
       williamyeh/ganglia-monitor-mini
   ```

2. Then, start the gmetric with `--link`:

   ```
   $ docker run  --link gmond:gmond    \
       williamyeh/ganglia-monitor-mini \
         gmetric -d 120 --type=string  \
                 --name=demo_gmetric   \
                 --value=`date '+%Y-%m-%dT%H:%M:%S%:z'`
   ```

## History

- 0.1 - Initial release.


## Author

William Yeh, william.pjyeh@gmail.com


## License

Apache License V2.0.  See [LICENSE](LICENSE) file for details.
