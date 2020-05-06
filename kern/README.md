# [`kern`][1]

This Dockerfile builds a base image for the
[kern suite](https://kernsuite.info/)
with features developed in Project Laniakea.
One can simply run this kern Docker image as a Laniakea subcommand.
That is,

    l6a kern [args]

Details on running AstroContainers images can be found in
https://astrocontainers.org/.

## Releases

[`astcon/kern`][1] tags | `l6acon/lanibase` tag | Ubuntu digest
--- | --- | ---
`5`, `20200112`, `bionic`, `latest` | `20200130` | `sha256:3235326357dfb65f1781dbc4df3b834546d8bf914e82cce58e6e6b676e23ce8f`

TODO: because this image is based on Ubuntu, we have not pinned its
package repository to specific dates.
Hence building images from this Dockerfile is not exactly reproducible
as in other Laniakea based images.

[1]: https://hub.docker.com/repository/docker/astcon/kern
