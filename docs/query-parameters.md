
# Query Parameters
The Mol\* Mesoscale Explorer supports a number of URL [parameters](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL#parameters) to load structures and change viewer options.

## Parameters

### `hide-controls`
This will hide the UI panels on all sides. If set to `1`, the controls are hidden. For all other values, the controls are shown. By default, the controls are shown. Clicking on the wrench icon in the top right of the canvas will toggle the visibility of the controls.

    hide-controls=1

### `pdb-provider`
Specifies where to load PDB entries from. Allowed values are `pdbe`, `pdbj`, and `rcsb`. Defaults to `pdbe`. From Europe, `pdbe` generally offers faster PDB downloads. From Asia-Pacific, `pdbj` is usually faster. From the Americas, `rcsb` is usually faster.

    pdb-provider=pdbe

### `emdb-provider`
Specifies where to load EMDB entries from. Allowed values are `pdbe` and `rcsb`. Defaults to `pdbe`. From Europe, `pdbe` generally offers faster EMDB downloads. From the Americas, `rcsb` is faster.

    emdb-provider=pdbe

### `url`
URL pointing to a Mol\* snapshot. Use `type` to define the type.

    url=https%3A%2F%2Fmolstar.org%2Fdemos%2Fstates%2Fbtub.molx

### `type`
Specifies the type of snapshot. Allowed values are `molj`, `molx`, `cif`, `bcif`.

    snapshot-url-type=molj

### `pdb`
Load one or more (comma separated) [PDB](https://www.wwpdb.org/) entries.

    pdb=3pqr

### `pdbdev`
Load one or more (comma separated) [PDB-Dev](https://pdb-dev.wwpdb.org/) entries.

    pdbdev=PDBDEV_00000030

### `debug-mode`
If set to `1`, debug mode is enabled. This will print debug info to the browser console and perform (expensive) runtime checks.

    debug-mode=1

### `timing-mode`
If set to `1`, timing mode is enabled. This will print timing info.

    timing-mode=1

### `prefer-webgl1`
If set to `1`, forces using WebGL1 instead of WebGL2.

    prefer-webgl1=1

### `allow-major-performance-caveat`
If set to `1`, allows using WebGL1 instead of WebGL2.

    allow-major-performance-caveat=1

### `power-preference`
Specifies the power preference. Allowed values are `high-performance`, `low-power`, etc.

    power-preference=high-performance

### `graphics-mode`
Specifies the graphics mode. Allowed values are `ultra`, `quality`, `balanced`, `performance`, `custom`.

    graphics-mode=quality

### `example`
Allowed values:

    petworld-hiv
    petworld-sarscov2
    petworld-postsynmushroom
    petworld-postsynstubby
    petworld-presynapse
    petworld-syngap
    petworld-synvesicle
    machineryoflife
    cellpack-hiv1
    cellpack-exosome
    cellpack-mg
    cellpack-isg_immature
    cellpack-isg_mature

    machineryoflife-tour
    petworld-hiv-tour
    petworld-sarscov2-tour
    cellpack-exosome-tour
    cellpack-hiv-tour
    cellpack-mg-tour

    example=machineryoflife-tour


## Examples
Load a Mol\* snapshot from a [URL](https://molstar.org/me/?url=https%3A%2F%2Fmolstar.org%2Fdemos%2Fstates%2Fbtub.molx&snapshot-url-type=molx)

    https://molstar.org/me/?url=https%3A%2F%2Fmolstar.org%2Fdemos%2Fstates%2Fbtub.molx&snapshot-url-type=molx

Load a mmCIF file from a [URL](https://molstar.org/me/?url=https://files.rcsb.org/download/6Z1W.cif&type=cif)

    https://molstar.org/me/?url=https://files.rcsb.org/download/6Z1W.cif&type=cif

Load PDB entry [3PQR](https://molstar.org/me/?pdb=3pqr)

    https://molstar.org/me/?pdb=3pqr

Load PDB-Dev entry [PDBDEV_00000030](https://molstar.org/me/?pdbdev=PDBDEV_00000030)

    https://molstar.org/me/?pdbdev=PDBDEV_00000030

Load Example [Exosome](https://molstar.org/me/?example=cellpack-exosome&hide-controls=1) wile hiding main control by default.

    https://molstar.org/me/?example=cellpack-exosome&hide-controls=1


