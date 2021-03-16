# [`am`][1]

This Dockerfile builds `am`, a tool for radiative transfer
computations at microwave to submillimeter wavelengths, see
https://www.cfa.harvard.edu/~spaine/am/ .
Spectra which can be computed with am include thermal emission,
absorption, transmission, and excess delay.
The program can modify computed spectra to model the response of
spectrometers and receiving systems, and can compute Jacobians of
output spectra differentiated with respect to selected model
parameters.
Measured spectra can be fitted using a simple scheme for flagging
model parameters as fit variables.

The primary application area for `am` is in radio astronomy, involving
terrestrial propagation paths between ground and sky.
The program can also be applied to a variety of other radiative
transfer problems, and has been used for applications ranging from
laboratory receiver testing to radio spectrum management.

Because AstroContainers are based on Project Laniakea, one can simply
run this `am` Docker image as a Laniakea subcommand.
That is,

    l6a am [args]

Details on running AstroContainers images can be found in
https://astrocontainers.org/.

## Releases

[`astcon/am`][1] tags | `l6acon/lanibase` tag | `am` source version
--- | --- | ---
`11.0`, `11`, `latest` | `20201117` | `11.0`

In general, although a Docker image is immutable, building a new image
is not even when using the same Dockerfile.
Nevertheless, by following Project Laniakea's best practices and using
the Laniakea base image, building image with this Dockerfile should be
reproducible.
Non-reproducibility is considered a bug in Project Laniakea, please
report non-reproducibility issues to the maintainer.

[1]: https://hub.docker.com/repository/docker/astcon/am
