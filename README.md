# Legacy Hosting Releases

Immutable runtime archives produced by the independent Legacy Hosting service repositories.

## Layout

Each service writes its `tar.gz` archive to its own directory, the matching
checksum to `SHA256`, and the detached Ed25519 signature to `SIGNATURES`:

```text
LH-API/lh-api-1.0.32.tar.gz
LH-API/SHA256/lh-api-1.0.32.tar.gz.sha256
LH-API/SIGNATURES/lh-api-1.0.32.tar.gz.sig
```

The same layout applies to `LH-Agent`, `LH-Discord`, `LH-Hub`, `LH-Panel`, `LH-SSO`, and `LH-Status`.

Archives are tracked with Git LFS. Checksum files are normal Git text files and
signatures are 64-byte binary Git files. Releases are append-only: an archive,
checksum, or signature for a published version must never be overwritten or
removed. Publish a new version when content changes.

Verify an archive from the service directory with the service public key that
was independently provisioned by `LH-Ops`:

```bash
/usr/local/lib/legacy-hosting-ops/verify-release-artifact.sh \
  /etc/legacy-hosting/release-keys/lh-api.pub \
  lh-api-1.0.32.tar.gz \
  SHA256/lh-api-1.0.32.tar.gz.sha256 \
  SIGNATURES/lh-api-1.0.32.tar.gz.sig
```

Unsigned historical releases are retained for rollback history but must not be
promoted as new production releases.

Release workflows require a repository-scoped `RELEASES_TOKEN` with Contents read/write access to `Legacy-Hosting/LH-Releases`. Runtime servers only need read access.
