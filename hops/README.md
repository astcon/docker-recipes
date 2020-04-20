# [`HOPS`][1]

This Dockerfile builds the [Haystack Observatory Postprocessing System
(`HOPS`)](https://www.haystack.mit.edu/tech/vlbi/hops.html)
environment for performing data calibration for the [Event Horizon
Telescope (EHT)](https://eventhorizontelescope.org/)'s observations.

Because AstroContainers are based on Project Laniakea, one can simply
run this `HOPS` Docker image as a Laniakea subcommand.
That is,

    l6a hops [args]

Details on using AstroContainers and Laniakea images can be found in
https://astrocontainers.org/ and https://l6a.org, respectively.

## Releases

[`hops`][1] tags | `lanibase` tag | `hops` source version
--- | --- | ---

In general, although a Docker image is immutable, building a new image
is not, even with the same Dockerfile.
Nevertheless, by following Project Laniakea's best practices and using
the Laniakea base image, building a HOPS container using this
Dockerfile should be reproducible.
Non-reproducibility is considered a bug in Project Laniakea, please
report non-reproducibility issues to the maintainer.

[1]: https://hub.docker.com/repository/docker/astcon/hops
