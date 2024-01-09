## Minio

Find files and then copy them down:

```shell
mc find littlebox/flights --name "169299*.json" --exec "mc cp {} ./"
```