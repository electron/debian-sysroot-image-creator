This repository contains a set of scripts for creating linux sysroot images, copied from Chromium.

It adds some necessary dependencies for Electron and uploads the images to Electron's Azure storage container.

[Upstream Sysroots Logic](https://chromium.googlesource.com/chromium/src/+/master/build/linux/sysroot_scripts/)

## Updating Sysroots in Electron

`debian-sysroot-image-creator` automatically builds and uploads sysroot images.

Sysroots are generated when new pull requests are merged to `bullseye`.

To initiate a sysroot update, make changes locally and open a new pull request containing the desired changes. Once you open the PR, sysroots will be built. They will be uploaded as artifacts in CI so that you can verify the changes you've made.

Once you've received review and the PR is merged, a new build and upload job will be initiated. When it is complete, there will be a newly generated `sysroots.json` artifact in the [GitHub Actions](https://github.com/electron/debian-sysroot-image-creator/actions/workflows/build.yml) run for the commit merged to `bullseye`.

Take the artifact and copy its contents to the [associated sysroots file](https://github.com/electron/electron/blob/main/script/sysroots.json) in `electron/electron`.

Finally, open a new PR to [`electron/electron](https://github.com/electron/electron/). When that PR passes CI and is merged, the process completes.

## How It Works

At the moment, we build the following sysroots:

* `amd64`
* `i386`
* `armhf`
* `arm64`
* `mipsel`
* `mips64el`
* `ppc64el`

## Building A Single Sysroot

To build a single sysroot, run:

```console
./build/linux/sysroot_scripts/sysroot_creator.py build <arch>
```

This will build the desire sysroot in `<arch>` at `out/sysroot-build/bullseye/debian_bullseye_<arch>_sysroot.tar.xz`, e.g. `out/sysroot-build/bullseye/debian_bullseye_amd64_sysroot.tar.xz`.

## Building All Sysroots

To build all sysroots at once, run:

```console
./build/linux/sysroot_scripts/build_and_upload.py --build
```

This will generate all sysroots at `out/sysroot-build/bullseye`.

## Uploading Sysroots

To upload sysroots to the Azure storage container after they've been generated, run:

```console
./build/linux/sysroot_scripts/build_and_upload.py --build
```

Ensure you have a valid `AZURE_STORAGE_SAS_TOKEN` as well as `AZURE_STORAGE_ACCOUNT` in your environment, or upload will fail.
