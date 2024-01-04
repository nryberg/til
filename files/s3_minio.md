# Minio

Is amazing but frustrating.

## File Pattern Download

First you have to find the files, then you use the `--exec` flag to actually move the files down.

```shell
mc find littlebox/flights --name "16924499*.json" --exec "mc cp {} ./"
`littlebox/flights/1692449917.json` -> `1692449917.json`
Total: 2.78 KiB, Transferred: 2.78 KiB, Speed: 81.58 KiB/s
`littlebox/flights/1692449947.json` -> `1692449947.json`
Total: 3.28 KiB, Transferred: 3.28 KiB, Speed: 111.48 KiB/s
`littlebox/flights/1692449955.json` -> `1692449955.json`
Total: 4.74 KiB, Transferred: 4.74 KiB, Speed: 221.80 KiB/s
`littlebox/flights/1692449977.json` -> `1692449977.json`
Total: 4.82 KiB, Transferred: 4.82 KiB, Speed: 115.28 KiB/s
^C
ls
1692449917.json  1692449955.json  config.yaml  hooks  soft-serve.db
1692449947.json  1692449977.json  flights      log    ssh
```