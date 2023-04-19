# Download-Artifact

This downloads artifacts from your build
This action is an extension of Github's [download-artifact](https://github.com/actions/download-artifact) action that `untar` the files after downloading.

See also [upload-artifact](https://github.com/eviden-actions/upload-artifact).

[![Release](https://github.com/eviden-actions/download-artifact/actions/workflows/on_push.yml/badge.svg#main)](https://github.com/eviden-actions/download-artifact/actions/workflows/on_push.yml)

## Usage

See [action.yml](action.yml)

### Download a Single Artifact

Basic (download to the current working directory):

```yaml
steps:
  - uses: actions/checkout@v3

  - uses: eviden-actions/download-artifact@v1
    with:
      name: my-artifact

  - name: Display structure of downloaded files
    run: ls -R
```

Download to a specific directory:

```yaml
steps:
  - uses: actions/checkout@v3

  - uses: eviden-actions/download-artifact@v1
    with:
      name: my-artifact
      path: path/to/artifact

  - name: Display structure of downloaded files
    run: ls -R
    working-directory: path/to/artifact
```

Basic tilde expansion is supported for the `path` input:

```yaml
- uses: eviden-actions/download-artifact@v1
  with:
    name: my-artifact
    path: ~/download/path
```

# Download path output

The `download-path` step output contains information regarding where the artifact was downloaded to. This output can be used for a variety of purposes such as logging or as input to other actions. Be aware of the extra directory that is created if downloading all artifacts (no name specified).

```yaml
steps:
  - uses: actions/checkout@v3

  - uses: eviden-actions/download-artifact@v1
    id: download
    with:
      name: 'my-artifact'
      path: path/to/artifacts

  - name: 'Echo download path'
    run: echo ${{steps.download.outputs.download-path}}
```

> Note: The `id` defined in the `download/artifact` step must match the `id` defined in the `echo` step (i.e `steps.[ID].outputs.download-path`)

## Additional Documentation

See [Github's download-artifact action](https://github.com/actions/updownload-artifact) for additional documentation.

See extra documentation for the [@actions/artifact](https://github.com/actions/toolkit/blob/main/packages/artifact/docs/additional-information.md) package that is used internally regarding certain behaviors and limitations.
