The [Nictiz FHIR Implementation Guide R4](https://informatiestandaarden.nictiz.nl/wiki/FHIR:V1.0_FHIR_IG_R4) (version 1.0.6) sets general principles for exchanging data with HL7 FHIR R4 in the Netherlands. These principles apply to the exchanges specified in the Twiin implementation guides, unless a Twiin implementation guide or the TA it specifies explicitly deviates from them.

Among other things, these principles cover:

- HTTP: UTF-8 with an explicit `charset`, support for both XML and JSON, and `fhirVersion` in the `Accept` and `Content-Type` headers (section 2.3).
- References and identifiers (sections 2.5 and 2.8).
- Profiles in `meta.profile`, without a version appended to the canonical (section 2.6).
- Search, paging and error handling with HTTP status codes and an OperationOutcome (sections 2.7 and 2.9).
- Terminology, missing data and narrative (sections 2.4, 2.12 to 2.14).

The Nictiz guide is the source for these principles; this page does not repeat or interpret them. Where a Twiin implementation guide deviates, it says so on its own pages, with the section of the Nictiz guide it deviates from. Where a Twiin implementation guide and the TA differ, the TA applies.
