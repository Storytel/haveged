# haveged

We use [haveged](http://www.issihosts.com/haveged/) to provide entropy on CoreOS servers lacking other suitable sources.

## How to use

Starting a container from this image is simple.

```
docker run --name haveged --privileged storytel/haveged
```

On CoreOS we run this as a Systemd service.

```
[Unit]
Description=haveged
Requires=docker.service
After=docker.service

[Service]
Restart=always
ExecStartPre=/usr/bin/docker pull storytel/haveged
ExecStartPre=-/usr/bin/docker rm -f haveged
ExecStart=/usr/bin/docker run --name haveged --privileged storytel/haveged
ExecStop=/usr/bin/docker stop haveged
TimeoutStartSec=1m

[Install]
WantedBy=multi-user.target
```
