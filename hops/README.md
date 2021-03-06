# [`HOPS`][1]

This Dockerfile builds the [Haystack Observatory Postprocessing System
(HOPS)](https://www.haystack.mit.edu/tech/vlbi/hops.html) environment
for performing data calibration for the [Event Horizon Telescope
(EHT)](https://eventhorizontelescope.org/)'s observations.

Because AstroContainers are based on Project Laniakea, one can simply
run this HOPS Docker image as a Laniakea subcommand.
That is,

    l6a hops [args]

Details on running AstroContainers images can be found in
https://astrocontainers.org/.

## Releases

[`astcon/hops`][1] tags | `l6acon/lanibase` tag | HOPS source version
--- | --- | ---
`3.21`, `20200422`, `3`, `latest` | `20200422` | `hops-dv-difx-tc-3.21swc`
`3.20`, `20200130`                | `20200130` | `hops-dv-difx-tc-3.20swc`

In general, although a Docker image is immutable, building a new image
is not even when using the same Dockerfile.
Nevertheless, by following Project Laniakea's best practices and using
the Laniakea base image, building image with this Dockerfile should be
reproducible.
Non-reproducibility is considered a bug in Project Laniakea, please
report non-reproducibility issues to the maintainer.

[1]: https://hub.docker.com/repository/docker/astcon/hops
