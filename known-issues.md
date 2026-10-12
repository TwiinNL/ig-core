# Known issues

## Not fixed by `twiin.base.template#0.1.1`

Applies to: `twiin.base.template#0.1.1` (based on `fhir2.base.template#0.1.0`) with IG Publisher 3.0.0. The template fixes the redirect to `en/` for non-English browsers, the empty release label, the doubled `<h2 id="root">` on profile history pages and the not well formed profile pages (see its [README](https://github.com/TwiinNL/ig-template)); this repository has no workarounds for those any more. What remains, the same with `fhir2.base.template#0.1.0` alone and also listed in the template README:

- `searchform.html` has its own markup that the publisher reports as not well formed: 8 warnings for `output/searchform.html` and 8 for `output/en/searchform.html` (16 in total, not allowlisted, warnings do not fail the build).
- Profile history pages are not in the page list of the publisher, so their breadcrumb bar is empty and the heading has no section number. This IG has no profiles yet.
