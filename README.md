# ig-core

FHIR R4 implementation guide for the technical core of the Twiin Afsprakenstelsel. It holds artifacts shared by multiple Twiin IGs (e.g. `nl.twiin.fhir.r4.notifications`, `nl.twiin.fhir.r4.workflow`).

- Package id: `nl.twiin.fhir.r4.core`
- Canonical: https://fhir.twiin.nl/ig/core
- FHIR version: 4.0.1
- Version: 0.1.0 (draft)
- Publisher: Twiin

Built with [SUSHI](https://fshschool.org/docs/sushi/) and the HL7 IG Publisher.

## TODO before the first release

- Pin the template version in `ig.ini` (currently `fhir.base.template#current`).
- Remove the placeholder artifact (`input/fsh/placeholder.fsh`, Questionnaire `twiin-placeholder`). R4 requires at least one `ImplementationGuide.definition.resource`, so an IG without artifacts cannot build without errors.

## Build

```sh
./_updatePublisher.sh   # download/update the IG Publisher
sushi build .
./_genonce.sh -no-sushi # output in output/ (see output/qa.html)
```

Requires Java, Node (SUSHI) and Jekyll. The template is set in `ig.ini`, not in `sushi-config.yaml`: SUSHI 3.20.1 reports the `template` property as no longer supported.

## CI

`.github/workflows/build.yml` runs on pull requests and pushes to `main`: SUSHI, download of IG Publisher 3.0.0 (pinned), build, upload of `output/` (including `qa.html`) as artifact `ig-output`.

The build fails on every publisher error that is not listed in [known-errors.txt](known-errors.txt) (see [known-issues.md](known-issues.md)); both are currently empty, so any error fails the build. The publisher exit code cannot be used for this: IG Publisher 3.0.0 exited with 0 on a build whose `qa.html` listed 3 errors (verified locally, 2026-10-08). Warnings and hints do not fail the build. Errors cannot be suppressed via `input/ignoreWarnings.txt`.

`.github/scripts/check-qa.py` reads the individual errors from `output/qa.xml`, a FHIR Bundle of OperationOutcomes written by the publisher. Chosen over the alternatives because it is structured (severity, message and expression as separate elements): `qa.txt` and `qa-eslintcompact.txt` are text for humans, and they carry absolute local paths or no location. Each error becomes one line `<location>: <message>`, with the issue's `expression` as location (file name if there is none), and must match a line in `known-errors.txt` exactly. Matching is on text and location, not on count. As a cross-check the script requires the number of errors in `qa.xml` to equal `errs` in `output/qa.json`, and fails otherwise.

Neither file's layout is documented as far as I could verify; both were inspected with IG Publisher 3.0.0, which is why the CI pins that version (`PUBLISHER_VERSION` in the workflow). On every publisher update, re-check that `qa.xml` still lists the same errors as `qa.html`, and that the publisher exit code still behaves as described above. Entries in `known-errors.txt` that no longer occur are reported as a notice.

## License

- IG content (everything in `input/`, including FSH): CC BY-SA 4.0 (SPDX: `CC-BY-SA-4.0`), see [LICENSE](LICENSE).
- Code (workflows, own scripts): TBD.
- `_updatePublisher.*` and `_genonce.*` are copied unmodified from [HL7/ig-publisher-scripts](https://github.com/HL7/ig-publisher-scripts). The license of that repository is unknown (see [TwiinNL/ig-notifiedpull-stu3](https://github.com/TwiinNL/ig-notifiedpull-stu3)); clarify with HL7 before publishing.
