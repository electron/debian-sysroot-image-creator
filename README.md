# debian-sysroot-image-creator

Chromium's scripts for creating Debian sysroot images, modified to fit
Electron's dependencies.

## Boostrap (if you need to upload binaries)

```bash
$ go get github.com/aktau/github-release
$ export GITHUB_TOKEN=YOURTOKEN
```

## Usage

```bash
$ ./scripts/sysroot-creator-wheezy.sh BuildSysrootARM
$ ./scripts/sysroot-creator-wheezy.sh UploadSysrootAll 0.1.0 "release description"
```
