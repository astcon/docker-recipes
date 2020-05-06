# Docker Image Recipes for the AstroContainers Project

This repository contains recipes for building Docker images for the
AstroContainers project.
Each subdirecotry (except `bin/`) contains the Dockerfile and
necessary files to build a tailored Docker image.
They are in general set up for autobuild on Docker Hub.
For more simple images that does not require specific Dockerfile, they
are listed in `*-images.md` and designed for autobuild on GitHub.

To summarize, tailored images include
[`astroconda`](astroconda),
[`astropy`](astropy),
[`difmap`](difmap),
[`difx`](difx),
[`hops`](hops), and
[`kern`](kern);
and general images are listed in
[`kern-images.md`](kern-images.md).
