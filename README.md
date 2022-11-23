# Parcel/Lightning.css docker arm issue

## Apple M1 (without copying binaries)

### Run

```shell
$ docker build .
```

### Output

```
@parcel/transformer-css: Could not resolve module
"/usr/src/app/node_modules/lightningcss/lightningcss.linux-arm64-gnu.node" from
"/usr/src/app/node_modules/lightningcss/node/index.js"


  Error: Could not resolve module
  "/usr/src/app/node_modules/lightningcss/lightningcss.linux-arm64-gnu.node"
  from "/usr/src/app/node_modules/lightningcss/node/index.js"
      at $0578d0f6e116167e$export$fb2a0b866a8162dc.resolve
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:4991:21)
      at NodePackageManager.resolveSync
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3510:42)
      at NodePackageManager.requireSync
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3352:34)
      at m.require
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3366:25)
      at require (node:internal/modules/cjs/helpers:103:18)
      at Object.<anonymous>
  (/usr/src/app/node_modules/lightningcss/node/index.js:21:22)
      at Module._compile (node:internal/modules/cjs/loader:1159:14)
      at Module._extensions..js (node:internal/modules/cjs/loader:1213:10)
      at Module.load (node:internal/modules/cjs/loader:1037:32)
      at NodePackageManager.load
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3375:15)
error Command failed with exit code 1.
```

## Apple M1 (with copying binaries)

### Run

```shell
$ docker build -f ./Dockerfile-cp-bin .
```

### Output

```
@parcel/transformer-css: /lib/aarch64-linux-gnu/libm.so.6: version `GLIBC_2.35'
not found (required by
/usr/src/app/node_modules/lightningcss/lightningcss.linux-arm64-gnu.node)

  Error: /lib/aarch64-linux-gnu/libm.so.6: version `GLIBC_2.35' not found
  (required by
  /usr/src/app/node_modules/lightningcss/lightningcss.linux-arm64-gnu.node)
      at Module._extensions..node (node:internal/modules/cjs/loader:1243:18)
      at Module.load (node:internal/modules/cjs/loader:1037:32)
      at NodePackageManager.load
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3375:15)
      at NodePackageManager.requireSync
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3353:21)
      at m.require
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3366:25)
      at require (node:internal/modules/cjs/helpers:103:18)
      at Object.<anonymous>
  (/usr/src/app/node_modules/lightningcss/node/index.js:21:22)
      at Module._compile (node:internal/modules/cjs/loader:1159:14)
      at Module._extensions..js (node:internal/modules/cjs/loader:1213:10)
      at Module.load (node:internal/modules/cjs/loader:1037:32)
error Command failed with exit code 1.
```

## Docker Buildx arm/v7 (without copying binaries)

### Run

```shell
$ docker buildx build --platform linux/arm/v7
```

### Output

```
@parcel/transformer-css: Could not resolve module
"/usr/src/app/node_modules/lightningcss/lightningcss.linux-arm-gnueabihf.node"
from "/usr/src/app/node_modules/lightningcss/node/index.js"

  Error: Could not resolve module
  "/usr/src/app/node_modules/lightningcss/lightningcss.linux-arm-gnueabihf.node"
   from "/usr/src/app/node_modules/lightningcss/node/index.js"
      at $0578d0f6e116167e$export$fb2a0b866a8162dc.resolve
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:4991:21)
      at NodePackageManager.resolveSync
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3510:42)
      at NodePackageManager.requireSync
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3352:34)
      at m.require
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3366:25)
      at require (node:internal/modules/cjs/helpers:103:18)
      at Object.<anonymous>
  (/usr/src/app/node_modules/lightningcss/node/index.js:21:22)
      at Module._compile (node:internal/modules/cjs/loader:1159:14)
      at Module._extensions..js (node:internal/modules/cjs/loader:1213:10)
      at Module.load (node:internal/modules/cjs/loader:1037:32)
      at NodePackageManager.load
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3375:15)

error Command failed with exit code 1
```

## Docker Buildx arm/v7 (with copying binaries)

### Run

```shell
$ docker buildx build --platform linux/arm/v7 -f ./Dockerfile-cp-bin .
```

### Output

```
@parcel/transformer-css: /lib/arm-linux-gnueabihf/libc.so.6: version
`GLIBC_2.33' not found (required by
/usr/src/app/node_modules/lightningcss/lightningcss.linux-arm-gnueabihf.node)


  Error: /lib/arm-linux-gnueabihf/libc.so.6: version `GLIBC_2.33' not found
  (required by
  /usr/src/app/node_modules/lightningcss/lightningcss.linux-arm-gnueabihf.node)
      at Module._extensions..node (node:internal/modules/cjs/loader:1243:18)
      at Module.load (node:internal/modules/cjs/loader:1037:32)
      at NodePackageManager.load
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3375:15)
      at NodePackageManager.requireSync
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3353:21)
      at m.require
  (/usr/src/app/node_modules/@parcel/package-manager/lib/index.js:3366:25)
      at require (node:internal/modules/cjs/helpers:103:18)
      at Object.<anonymous>
  (/usr/src/app/node_modules/lightningcss/node/index.js:21:22)
      at Module._compile (node:internal/modules/cjs/loader:1159:14)
      at Module._extensions..js (node:internal/modules/cjs/loader:1213:10)
      at Module.load (node:internal/modules/cjs/loader:1037:32)
error Command failed with exit code 1.
```
