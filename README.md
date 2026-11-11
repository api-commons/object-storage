# Object Storage

The common object-storage vocabulary -- buckets and the objects stored in them -- distilled from the management APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Storage, Object Storage, Cloud Storage, S3, Blob Storage, Backup, Decentralized Storage in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| bucket | 21 | 21 | name 86%, created_at 52% | buckets 18, bucket 3, volumes 1 |
| storage_object | 10 | 10 | created_at 70%, key 70%, id 60% | keys 8, objects 3, files 1 |

Cohort: 121 providers with harvested OpenAPI, 21 crosswalks. Of the providers exposing a bucket: 67% create, 90% list, 67% fetch, 48% update, 76% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Buckets agree on name and created_at; id reaches 43% and region 33%, because many providers key a bucket by its globally unique name.
- Objects agree on created_at, key and id; size reaches only 30%. Object metadata mostly travels in response headers (Content-Length, ETag), which a schema census does not read.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The object is storage_object and its name is key, the S3 word the market converged on.
- The S3 API itself is XML and is read in no context yet; it is on the tooling backlog with the XML body reader.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
