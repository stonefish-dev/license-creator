<p align="center">
  <a href="https://github.com/stonefish-dev/license-creator"><img alt="slic" src="https://raw.githubusercontent.com/stonefish-dev/license-creator/main/images/stonefish-license-creator-logo.svg" width="60%"></a>
</p>

[![PyPi Version](https://img.shields.io/pypi/v/stonefish-license-creator.svg?style=flat-square)](https://pypi.org/project/stonefish-license-creator/)

<!-- [![PyPI pyversions](https://img.shields.io/pypi/pyversions/python-license-manager.svg?style=flat-square)](https://pypi.org/project/python-license-manager/) -->

SLiC (**S**tonefish **Li**cense **C**reator) is a command-line tool for
creating licenses compatible with the [Stonefish License
Manager](https://github.com/stonefish-dev/license-manager) (SLiM).

Install with

```
pip install stonefish-license-creator
```

### Quickstart

- Make sure you have a valid license for
  [Stonefish](https://github.com/stonefish-dev/). (Trial licenses are
  available.)

- Have your private key ready. If you don't have a key pair yet, create one
  with, e.g.,

  ```
  slic create-random-keypair
  ```

  <p align="center">
  <img alt="slic" src="https://raw.githubusercontent.com/stonefish-dev/license-creator/main/images/termshot-slic-ck.png" width="80%">
  </p>

- Create a license with

  <!--pytest.mark.skip-->

  ```sh
  slic create-license <your-input-file> <your-ed25519-private-key-hex>
  ```

  where `<your-input-file>` is a YAML- or JSON-formatted configuration file,
  e.g.,

  ```yaml
  vendor:
    id: your-vendor-uuid # assigned to you

  product:
    id: your-product-uuid # set by you, e.g., `slic uuid`
    name: KewlPack

  user:
    id: user-uuid # set by you
    name: J. Doe # optional
    email: j.doe@example.com

  machines: # optional
    - name: prometheus # optional
      # fingerprints can be retrieved with `slic fp` or `slim fp`
      fingerprint: 914b7459c8db4229ac9ef9e5dbf2837e

  license:
    expiry: 2030-01-08T15:13:17Z # ISO 8601 datetime
    # expiry: P1Y  # or ISO 8601 duration, here: 1 year

  metadata:
    trial: true
    comment: "dummy license"
  ```

- Your users can install the resulting key with the [Stonefish License
  Manager](https://github.com/stonefish-dev/license-manager) via

  ```
  slim install <key-file>
  ```

- Add a key check somewhere in your software. For example:

  <!--pytest.mark.skip-->

  ```python
  import stonefish_license_manager as slim

  # Throws a slim.LicenseError if no valid license is found:
  slim.slic.find_license_and_validate(
      vendor_id="<your-vendor-uuid>",
      product_id="<your-product-uuid>",
  )
  ```

  (More info
  [here](https://github.com/stonefish-dev/license-manager/blob/main/README-dev.md).)

> [!TIP]
>
> SLiM is also compatible with various other license services such as
> [Keygen.sh](https://keygen.sh/),
> [LicenseSpring](https://licensespring.com/), or
> [Cryptolens](https://cryptolens.io/).

### More info

For more info, don't hesitate to contact us at support@mondaytech.com.
