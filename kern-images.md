# Additional Docker images based on `astcon/kern`

Add additional rows in the following table for AstroContainers to
automatically build more Docker images.
All images listed here shoudl be based, directly or through another
image, on `astcon/kern`.
If the tags column is missing, the base image tags will be used.
If the packages column is missing, the image name will be used.
If the base column is missing, `astcon/kern` is assumed.
The comments column is optional.

Image Name | Tags | Packages | Base | Comments
--- | --- | --- | --- | ---
`aips` | `31dec18`, `latest` | `aips`, `parseltongue`
`casacore` | `3.0.0`, `3.0`, `3`, `latest` | `python3-casacore`
`difmap` | `2.5b-kern5`, `latest` | | `casacore:3.0.0`
