# Notes
Forked from [pysysops/docker-dashing](https://hub.docker.com/r/pysysops/docker-dashing/), added extra gems to be installed and allow mounting of /assets for dashing-contrib and changed default port to 3040. Everything else is identical to [pysysops/docker-dashing](https://hub.docker.com/r/pysysops/docker-dashing/).

When running on a CentOS with selinux on (like you should) apply the following permissions to your /dashing directory 

``` chcon -Rt svirt_sandbox_file_t dashing ```

Installs extra gems uptimerobot faraday faraday_middleware faraday-cookie_jar dashing-contrib

# Dashing
Run [Dashing](http://dashing.io/) in a [Docker](http://docker.io/) container.

Link: [mylivingweb/docker-dashing](https://registry.hub.docker.com/u/mylivingweb/docker-dashing/)

## About
Forked to install extra gems and mount /assets to allow dashing-contrib gem configuration. Forked specifically for RHEV API integration.

## Run
```docker run -d -p 8080:3040 mylivingweb/docker-dashing```

And point your browser to [http://localhost:8080/](http://localhost:8080/).


## Configuration
### Custom dashing port
If you want dashing to use a custom port inside the container, e g 8080, use the environment variable `$PORT`:

```docker run -d -e PORT=8080 -p 80:8080 mylivingweb/docker-dashing```

### Dashboards
To provide a custom dashboard, use container volume **/dashboards**:

```docker run -v=/my/custom/dashboards:/dashboards -d -p 8080:3040 mylivingweb/docker-dashing```

(*Don't forget to also provide the layout.erb*)

### Jobs
To provide custom jobs, use container volume **/jobs**:

```docker run -v=/my/cool/job:/jobs -d -p 8080:3040 mylivingweb/docker-dashing```

### Widgets
To install custom widgets supply the gist IDs of the widgets as an environment variable:

```docker run -d -e WIDGETS=5641535 -p 8080:3040 mylivingweb/docker-dashing```

This example will install the [Random Aww](https://gist.github.com/chelsea/5641535) widget
before starting dashing. Multiple widgets can be supplied.

Also you can use local custom widgets

```docker run -v=/my/cool/widgets:/widgets -d -p 8080:3040 mylivingweb/docker-dashing```


### Gems
To install gems, supply the gem name(s) as an environment variable:

```docker run -d -e GEMS=instagram -e WIDGETS=5278790 -p 8080:3040 mylivingweb/docker-dashing```

This example installs the [Instagram photos by location](https://gist.github.com/mjamieson/5278790) widget,
which depends on the instagram gem. Multiple gems and widgets can be supplied like so:

```docker run -d -e GEMS="mysql instagram" -e WIDGETS=5278790 -p 8080:3040 mylivingweb/docker-dashing```

### Assets
To mount your own assets directory, use container volume **/assets**:

```docker run -d -e -v=/path/to/assets:/assets -p 8080:3040 mylivingweb/docker-dashing```

### Public (favicon, 404)
To provide custom 404 and favicon, use container volume **/public**.

### Configuration File
The configuration file ```config.ru``` is available on volume */config*.

Edit this file to change your API key, to add authentication and more.


### Thanks
- [@frvi](https://github.com/frvi), For the original DockerFiles
- [@mattgruter](https://github.com/mattgruter), Awesome contributions!
- [@rowanu](https://github.com/rowanu), [Hotness Widget](https://gist.github.com/rowanu/6246149).
- [@munkius](https://github.com/munkius), [fork](https://gist.github.com/munkius/9209839) of Hotness Widget.
- [@chelsea](https://github.com/chelsea), [Random Aww](https://gist.github.com/chelsea/5641535).
- [@pysysops](https://github.com/pysysops), For the modified DockerFiles and general heavy lifting of it all.
