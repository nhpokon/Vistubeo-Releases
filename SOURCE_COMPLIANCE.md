# Vistubeo source compliance work log

This is a development document, not a public source offer. It must not be
renamed or represented as `SOURCE_OFFER.txt`. The QuickTube v0.49–v0.51
artifact names and audit results below are historical records and are retained
as recorded.

## Verified baseline

- Application baseline: v0.49.0
- Python: 3.14.6
- Custom PyAV: 18.0.0, source commit
  `54a4395bb4cdd9cdd53ff6216c50b69f6475c13d`
- Custom PyAV wheel FFmpeg: 8.1.2, LGPL-3.0-or-later,
  `--enable-version3`, x264/x265 disabled
- Standalone FFmpeg: Vistubeo minimal Windows x64 static native-codec build
  `9.0.1`, FFmpeg commit `b3ef323dd256d4b94ad5fd60b04ff7cba7df4259`
- Standalone FFmpeg SHA256:
  `a9d070f88cadbf999c331e38b4b6567dc90fd3a41f5aaa4b2bff92af48e018b5`
- Whisper model snapshot:
  `ebe41f70d5b6dfa9166e2c581c45c9c0cfc57b66`

The repository's old `dist/QuickTube` must not be used as the formal inventory;
it may contain obsolete x264/x265 libraries. A clean distribution must be made
with `build_distribution.py` and audited again.

## v0.51 source-bundle generator

`build_source_bundle.py` and `source_bundle_manifest.json` generate the local
archive `dist-sources/QuickTube-third-party-source-v0.51.0.zip`. Downloads use
bounded retries, temporary files, atomic replacement, and mandatory SHA256
verification. The cache and generated archive are intentionally not tracked.

The archive records the audited custom-wheel and standalone-FFmpeg binary
hashes, fixed revisions, build metadata, license texts, and the exact
x264/x265 exclusion patch. No public download URL is claimed yet.

Current completeness status:

- Custom PyAV: COMPLETE for the audited wheel. All 23 DLLs are mapped to fixed
  source archives. The MSYS2 GCC, libiconv, winpthreads, and zlib source-only
  packages are included with exact package releases and SHA256 values.
- Standalone FFmpeg: COMPLETE for the fixed FFmpeg upstream revision. The
  audited native-codec build has no external codec-library dependency; its
  source URL, archive SHA256, configuration, and binary hash are recorded.

The standalone FFmpeg source portion is complete. General distribution remains
blocked by the other unresolved items listed below.

`build_source_bundle.py --release` refuses to generate a release archive while
either deliverable is not `COMPLETE`, while a development/audit archive can
still be generated without that flag.

## Remaining corresponding-source work

Create reproducible, versioned source packages for both LGPL deliverables:

1. Publish the real source archive and immutable download information for the
   fixed standalone FFmpeg candidate when a public release is prepared.

Publish only real archives and real stable URLs. Do not create a placeholder
source offer or a URL for an archive that does not exist.

## Resolved: Intel OpenMP Runtime

`libiomp5md.dll` in the CTranslate2 4.8.1 Windows wheel is byte-identical to
`runtimes/win-x64/native/libiomp5md.dll` in Intel-owned formal runtime-redist
package `intelopenmp.redist.win` version `2025.3.0.640`.

- DLL SHA256: `982233366b0afcda1e0f55a0b134097e35b779613f54ddb69e685e6cd06b755f`
- Intel license: Intel Simplified Software License (Version October 2022)
- Required OpenMP third-party notice: preserved verbatim in
  `LICENSES/component-notices/Intel-OpenMP-2025.3.0.640-ThirdPartyPrograms.txt`
- The supplied license and listed OpenMP notices do not impose a corresponding
  source-offer obligation.

The Intel Simplified Software License permits unmodified binary redistribution
when its copyright notice and terms are reproduced with the distribution, Intel
is not used for endorsement, and the binary is not reverse engineered,
decompiled, disassembled, modified, or altered. This historical record
predates Vistubeo's own license; that license must not conflict with these
preserved Intel terms.

## Unresolved before general distribution

- Confirm whether any Microsoft Visual C++ runtime files are physically bundled
  by the formal onedir build. If present, record the applicable Microsoft
  redistribution terms and notices; if absent, document the external runtime
  prerequisite. Do not guess.
- Reconcile Python runtime third-party components (OpenSSL, SQLite, libffi and
  other items listed by CPython's license) against the actual onedir inventory.
- Historical v0.51 item: decide the application's own LICENSE/EULA separately.
  It was intentionally not part of that third-party notice phase.

## Optional Deno dependency

Vistubeo does not redistribute a Deno executable. yt-dlp may use a compatible
Deno installed separately by the user and available on PATH. When Deno is not
available, Vistubeo still lets yt-dlp attempt extraction without a JavaScript
runtime. Because no Deno binary is included in the onedir distribution, Deno is
not part of Vistubeo's binary inventory or corresponding-source bundle.

## Release gate

Before any general release:

1. Produce a clean v0.49+ onedir build with the audited custom LGPL PyAV wheel.
2. Confirm the build contains no x264/x265 artifacts.
3. Complete every unresolved item above or explicitly remove the affected
   binary from the distribution.
4. Publish the real LGPL corresponding-source archives and record immutable
   checksums and download URLs.
5. Update `THIRD_PARTY_NOTICES.txt` with those real URLs.
6. Confirm `THIRD_PARTY_NOTICES.txt` and `LICENSES/` are beside
   `Vistubeo.exe`, not hidden only under `_internal`.
7. Perform a clean Windows installation and notice/source-access audit.
