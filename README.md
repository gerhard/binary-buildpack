CF Buildpack that works with static binaries (go in our case). Any
statically linked binary that has been compiled for Linux x64 should
work with this buildpack. The only requirement is that the app pushed
to CF has a `web` executable binary which takes a single argument, the
port number that it should bind to.

The binary must bind to all interfaces, not just localhost. CF
HealthManager (HM9000) will see the app as down if it doesn't bind to
`0.0.0.0`

This buildpack also contains a web binary which can be used as an
example. To use this buildpack, after git cloning it, run the following:

```sh
cf create-buildpack binary_buildpack binary-buildpack 1
cd binary-buildpack
cf push static-go
curl static-go.10.244.0.34.xip.io # if deploying to bosh-lite
```
