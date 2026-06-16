# Datasets

Registry of datasets used by experiments. The actual files live in
`workspace/data/` and are **not** git-tracked — this file plus the fetch
scripts in `workspace/code/` are what make them reproducible. One entry per
dataset; experiments link here by heading, e.g. `[[datasets#imagenet-1k]]`.

Record per entry: source (URL/DOI), version/date, checksum, license, and the
fetch command/script. If a different version or preprocessing is needed, add a
**separate entry** rather than mutating an existing one.

<!-- Example — delete once real entries exist:

## imagenet-1k

- **Source:** https://www.image-net.org/ (ILSVRC2012)
- **Version / date:** ILSVRC2012, fetched 2026-05-23
- **Checksum:** sha256 <…> (downloaded archive)
- **License:** ImageNet terms of use — not redistributable
- **Fetch:** `workspace/code/fetch_imagenet.sh`
- **Local path:** `workspace/data/imagenet-1k/`

-->
