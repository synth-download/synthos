# SynthOS &nbsp; [![bluebuild build badge](https://github.com/synth-download/synthos/actions/workflows/build.yml/badge.svg)](https://github.com/synth-download/synthos/actions/workflows/build.yml)

Repository containing our personalized [Fedora CoreOS](https://www.fedoraproject.org/coreos/) image, powered by [BlueBuild](https://blue-build.org/).

Based off of [uCore Minimal](https://github.com/ublue-os/ucore/).

Refer to the [BlueBuild documentation](https://blue-build.org/how-to/setup/) and the [template repository](https://github.com/blue-build/template) for image building information, and [Fedora CoreOS's](https://docs.fedoraproject.org/en-US/fedora-coreos/getting-started/) documentation for managing SynthOS itself.

> [!CAUTION]
> This image is specifically customized and modified for our own usage, and includes settings and configurations that *only* apply to ourselves.
>
> As is, this image *will not* work for others. If you're here to use this, it's best to instead fork or grab from this repository and modify things accordingly for yourself.

## Install

An [ignition file](https://docs.fedoraproject.org/en-US/fedora-coreos/producing-ign/) is not required to install SynthOS as BlueBuild ends up packaging the Anaconda GUI installer with the image.

### Generate an ISO

An ISO image can be generated via [`bluebuild`](https://github.com/blue-build/cli), which is already bundled in BlueBuild created/maintained images.

```bash
sudo bluebuild generate-iso --iso-name synthos.iso image ghcr.io/synth-download/synthos
```

### Rebase from CoreOS

> [!WARNING]
> These instructions have not been tested.

If already on a CoreOS installation, you can switch to SynthOS via `rpm-ostree`.

1. First, get on the unsigned image:
```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/synth-download/synthos:latest
```
2. Reboot:
```bash
systemctl reboot
```
3. Switch to the verified image *using `bootc`*:
```bash
bootc switch --enforce-container-sigpolicy ghcr.io/synth-download/synthos:latest
```
4. Final reboot:
```bash
systemctl reboot
```

*Note that SynthOS prefers the usage of `bootc` over `rpm-ostree`.*