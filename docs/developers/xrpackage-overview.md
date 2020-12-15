---
id: xrpackage-overview
title: What is XRPackage?
---

<img src="/img/xrpk-logo.png" width="250px" height="250px" />

XRPackage turns 3D apps into a file you can load anywhere.

It uses standards like WebGL, WebXR, GLTF, and WebBundle to package an app into a `.wbn` file.

## What's in a package?

An XRPackage is a bundle of files. The entry point is a `manifest.json` (following the <a href="https://developer.mozilla.org/en-US/docs/Web/Manifest" target="_blank" rel="noopener noreferrer">Web App Manifest</a> standard). The rest of the files in the bundle are the source files for the app.

The main addition to the Web App Manifest specification is the `xr_type` field, which specifies the type of application and the spec version.

```
$ cat manifest.json
{
  "xr_type": "webxr-site@0.0.1",
  "start_url": "cube.js"
}
```

`xr_type` can currently be:

- `webxr-site@0.0.1`
- `gltf@0.0.1`
- `vrm@0.0.1`
- `vox@0.0.1`

See also the <a href="https://github.com/webaverse/xrpackage/tree/master/examples" target="_blank" rel="noopener noreferrer">examples</a>.

The `start_url` field depends on the type of package:

1. Asset packages

   For the following types of packages, the `start_url` references the single static asset file to be loaded:

   - `gltf@0.0.1`
   - `vrm@0.0.1`
   - `vox@0.0.1`

2) WebXR packages

   For WebXR packages, the `start_url` references the `index.js` entry point for the app. `index.js` should have any assets referenced using relative paths.

## Package configuration

The package manifest can contain an `xr_details` field which further specifies how it should be treated by a compatible runtime.

See [`xr_details` API](./10-xr-details-api.md) for more details on these properties.

## Building a package

Regardless of package type, packages are built with the `xrpk` tool which you can get on `npm`:

```bash
$ npm install -g xrpk
```

To build a package with `manifest.json` in the current directory:

```bash
$ xrpk build .
a.wbn
```

The resulting package is `a.wbn`.

See [Create An XRPackage](./10-xr-details-api.md) for how to create an XRPackage.

## Test the package

Once you have an XRPackage (`a.wbn`), you can run it in your browser like so:

```bash
$ xrpk run ./a.wbn
```

This will open up the XRPackage runtime in your browser and load the given file for viewing.
  

## Design Guidelines:

- Use transparent skyboxes to make it easier to compose multiple apps together.
- Be mindful of size to improve loading speeds, keep packages under 100mb.

See [Design Guidelines](./15-xrpackage-design-guidelines.md) for more.