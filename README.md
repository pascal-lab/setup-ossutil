# Setup Aliyun OSSUtil

Minimal GitHub Action for setting up Aliyun `ossutil` on Linux x64 runners.

This action:

- adds the bundled `ossutil` binary to `PATH`
- writes `~/.ossutilconfig`
- supports AccessKey credentials and optional STS token
- supports Linux x64 only

## Usage

```yaml
runs-on: ubuntu-latest
steps:
  - uses: actions/checkout@v6

  - uses: pascal-lab/setup-ossutil@v1
    with:
      endpoint: ${{ secrets.OSS_ACCESS_ENDPOINT }}
      access-key-id: ${{ secrets.OSS_ACCESS_KEY_ID }}
      access-key-secret: ${{ secrets.OSS_ACCESS_KEY_SECRET }}

  - run: ossutil cp -rf ./build oss://${{ secrets.OSS_BUCKET_NAME }}/path
```

## Inputs

| Name | Required | Description |
| --- | --- | --- |
| `endpoint` | yes | OSS endpoint, for example `oss-cn-hangzhou.aliyuncs.com`. |
| `access-key-id` | yes | Aliyun AccessKey ID. |
| `access-key-secret` | yes | Aliyun AccessKey Secret. |
| `sts-token` | no | STS token for temporary credentials. |

## Bundled Binary

Bundled tool:

- `ossutil` v1.7.19 Linux amd64
- official archive: `ossutil-v1.7.19-linux-amd64.zip`
- official archive SHA256: `dcc512e4a893e16bbee63bc769339d8e56b21744fd83c8212a9d8baf28767343`
- bundled binary SHA256: see `bin/ossutil.sha256`

The action verifies the bundled binary checksum before adding it to `PATH`.

## License

MIT
