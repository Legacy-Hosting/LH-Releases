# Legacy Hosting Releases

Immutable runtime archives produced by the independent Legacy Hosting service repositories.

## Layout

Each service writes its `tar.gz` archive to its own directory and writes the matching checksum to that directory's `SHA256` child:

```text
LH-API/lh-api-1.0.32.tar.gz
LH-API/SHA256/lh-api-1.0.32.tar.gz.sha256
```

The same layout applies to `LH-Agent`, `LH-Discord`, `LH-Hub`, `LH-Panel`, `LH-SSO`, and `LH-Status`.

Archives are tracked with Git LFS. Checksum files are normal Git text files. Releases are append-only: a published version must never be overwritten or removed. Publish a new version when content changes.

Verify an archive from the service directory:

```bash
sha256sum --check SHA256/lh-api-1.0.32.tar.gz.sha256
```

Release workflows require a repository-scoped `RELEASES_TOKEN` with Contents read/write access to `Legacy-Hosting/LH-Releases`. Runtime servers only need read access.
