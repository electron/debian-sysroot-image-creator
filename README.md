A set of scripts for creating linux sysroot images, copied from Chromium.

This fork adds some necessary dependencies for Electron, and upload the
images to Electron's S3 bucket.

Original link:
https://chromium.googlesource.com/chromium/src/+/master/build/linux/sysroot_scripts/

## How it works

debian-sysroot-image-creator automatically builds and uploads images, the workflow is:
1. Push some commits to debian-sysroot-image-creator
2. CircleCI builds and uploads the image, and then generates the `sysroots.json` file
3. Download the `sysroots.json` file from the Artifacts tab of the CI job, and copy it to Electron

To verify if the scripts are working, run `./build/linux/sysroot_scripts/build_and_upload.py` locally (on Linux)
