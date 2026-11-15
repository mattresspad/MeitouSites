# MeitouSites

An independent extraction of the [MeitouClient website](https://github.com/VlcekM/MeitouClient/tree/026b94fb15ad1059aa91db3a0f2fa01fb7258397/site), maintained at [mattresspad/MeitouSites](https://github.com/mattresspad/MeitouSites).

## Upstream baseline

Extracted from VlcekM/MeitouClient master at `026b94fb15ad1059aa91db3a0f2fa01fb7258397`. Git history is filtered to the website, benchmark sources, site build check, and license files, retaining original authors, dates, and messages. Commit IDs change when their trees and parent history are filtered.

The website source, routes, media, download destinations, canonical site URL, and design retain the upstream baseline. The earlier presentation and mod-directory changes are not applied here. Extraction changes are limited to this repository's documentation, build check, ignore rules, and committed benchmark snapshot. See [UPSTREAM.json](UPSTREAM.json) for provenance and checksums.

- `site/`: Astro website, including homepage, benchmarks, roadmap, and client build instructions.
- `bench/`: upstream benchmark data, generator, and contribution/measurement tooling. The client engine is not included.
- `site/public/bench/bench.json`: generated upstream benchmark snapshot, committed so this site builds independently.

## Develop

Use Node.js 24.

```sh
npm --prefix site ci
npm --prefix site run dev -- --host 127.0.0.1
npm --prefix site run build
npm --prefix site run preview -- --host 127.0.0.1
```

The static output is `site/dist/`. The existing Dockerfile can build the same committed snapshot:

```sh
docker build -t meitou-sites ./site
docker run --rm -p 8080:80 meitou-sites
```

GitHub Actions builds on main and relevant pull requests. It does not publish an image, call an upstream webhook, or deploy a site. Make subsequent website changes in branches and open pull requests against this repository's main branch.

## Refresh benchmark data

Ordinary development and builds use the committed snapshot. The upstream generator needs original engine commit IDs and tags; filtered site history cannot replace that history. To refresh, use a full, separately maintained MeitouClient checkout containing the intended upstream commit and tags:

```sh
python bench/tools/generate.py --repo /path/to/MeitouClient --ref UPSTREAM_COMMIT --out site/public/bench/bench.json
```

Update the benchmark source files from that same upstream revision, regenerate the snapshot with LF line endings, and update its source commit and SHA-256 in `UPSTREAM.json` together. The baseline snapshot was generated from the exact upstream commit above.

## Credits and license

MeitouClient and its website are the work of VlcekM and the upstream contributors; their authorship is preserved in Git history. The extracted code remains GPL-3.0-or-later. Keep [LICENSE](LICENSE), the upstream [additional permission](LICENSE-EXCEPTION.md), and [third-party notices](THIRD_PARTY_NOTICES.md) with redistributions. Asset and trademark credits remain with their respective owners.
