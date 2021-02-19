# `astropy`

This Dockerfile builds a `astropy` environment for AstroContainers.

Because AstroContainers are based on Project Laniakea, one can simply
run this Docker image as a Laniakea subcommand.
That is,

    l6a astropy [args]

Details on running AstroContainers images can be found in
https://astrocontainers.org/.

## Releases

`astcon/astropy` tags | `l6acon/lanibase` tag | `astropy` version
--- | --- | ---
`3.2.3`, `20200422`, `3.2`, `3`, `latest` | `20200422` | `3.2.3`
`3.1.2`,             `3.1`                | `20200422` | `3.1.2`
`3.0.5`,             `3.0`                | `20200422` | `3.0.5`
`2.0.16`,`20200130`, `2.0`, `2`           | `20200130` | `2.0.16`

In general, although a Docker image is immutable, building a new image
is not even when using the same Dockerfile.
Nevertheless, by following Project Laniakea's best practices and using
the Laniakea base image, building image with this Dockerfile should be
reproducible.
Non-reproducibility is considered a bug in Project Laniakea, please
report non-reproducibility issues to the maintainer.
