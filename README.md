# 2019 Google Summer of Code Project

From June through August of 2019 I wrote a
[Text Encoding Initiative](https://tei-c.org/)
exporter for the [Cuneiform Digital Library Initiative](https://cdli.ucla.edu),
to make data from cuneiform tablets and other inscriptions more accessible,
in particular to the [Scaife](https://scaife-viewer.org) reading environment.
The work was funded as a
[Google Summer of Code Project](https://summerofcode.withgoogle.com/projects/#5983146665836544).

This is a summary of what I accomplished.

## Demonstration

The project itself didn't have a public staging server, so I set
up a temporary one on my own domain.

 - Visit the test server at https://cdli.thaumas.net/scaife/
   (If necessary, click the gear and enable the 'CDLI Reader'
   and 'Suggested Documents' components.)
 - Click on one of the suggested documents.
 - Click **Translation** to show/hide the parallel translation.

## Milestones

- [x] Convert a document from ATF and display it in Scaife.
- [x] Publish a repo with a subset of convertible records.
- [x] Set up automated export from CDLI data to a CTS repo.
- [x] Demonstrate a scaife instance running somewhere.

# Code

The following repositories are new code I wrote as part of the project:

 - https://github.com/cdli-gh/atf2tei (document converter)
 - https://github.com/cdli-gh/cdli-cts (tei export target repo)
 - https://github.com/cdli-gh/cdli-cts-server (capitains server for cdli-cts)
 - https://github.com/cdli-gh/cdli-search (Catalogue search experiment)

I made contributions to two more repositories which are important
components of the project:

 - https://github.com/cdli-gh/scaife (fork of the reading environment)
 - https://github.com/oracc/pyoracc (parser atf2tei is using)

Changes to the scaife repo were not accepted upstream, so this
repo reflects our project's customized version.
See the [cdli branch](https://github.com/cdli-gh/scaife/commits/cdli)
for the changes I made for the demo running above.

See below for a contributions to the pyoracc parser.

## Contributions to upstream projects

### Pull requests

 - https://github.com/Capitains/MyCapytain/pull/192 (merged)
 - https://github.com/Capitains/flask-capitains-nemo/pull/125 (merged)
 - https://github.com/Capitains/HookTest/pull/146 (merged)
 - https://github.com/Capitains/HookTest/pull/144 (merged)
 - https://github.com/Capitains/HookTest/pull/143 (merged)
 - https://github.com/oracc/pyoracc/pull/85 (merged)
 - https://github.com/oracc/pyoracc/pull/84 (merged)
 - https://github.com/oracc/pyoracc/pull/81 (merged)
 - https://github.com/oracc/pyoracc/pull/80 (merged)
 - https://github.com/oracc/pyoracc/pull/79 (merged)
 - https://github.com/oracc/pyoracc/pull/77 (merged)
 - https://github.com/oracc/pyoracc/pull/76 (merged)
 - https://github.com/cdli-gh/pyoracc/pull/42 (merged)
 - https://github.com/cdli-gh/pyoracc/pull/41 (merged)
 - https://github.com/pallets/jinja/pull/1030 (merged)
 - https://github.com/pytest-dev/pytest/pull/5416 (merged)
 - https://github.com/scaife-viewer/readhomer/pull/30
 - https://github.com/scaife-viewer/readhomer/pull/31
 - https://github.com/scaife-viewer/readhomer/pull/33
 - https://github.com/scaife-viewer/scaife-basic/pull/6
 - https://github.com/scaife-viewer/scaife-basic/pull/5
 - https://github.com/vim/vim/pull/4619 (merged)
 - https://gitlab.com/cdli/framework/merge_requests/11 (merged)

### Issues

 - https://github.com/Capitains/Nautilus/issues/85
 - https://github.com/Capitains/HookTest/issues/145
 - https://github.com/scaife-viewer/scaife-viewer/issues/370
 - https://github.com/scaife-viewer/readhomer/issues/34
 - https://github.com/oracc/pyoracc/issues/78
 - https://github.com/oracc/pyoracc/issues/82
 - https://github.com/oracc/pyoracc/issues/83

### Data

 - [Reported](https://github.com/cdli-gh/data/issues?q=is:issue+label:%22atf+syntax%22)
   various atf syntax inconsistencies I found to @epp who
   corrected the master database.

## Future work

Continuation points for the project, which I didn't have
time to pursue. Hopefully these can be developed over time.

### Improve ATF conversion

ATF line markup isn't fully converted. The export xml files
should use tei markup to represent damage, restorations,
smallcap logograms, and superscript determinative.
This would need to be supported both in `atf2tei` and in the
tei parser in Scaife. Greek and Latin layout works well enough
with plain unicode text, but cuneiform transliteration requires
extra typographic features.

There are also a some unhandled annotations, like comments
and cross-references which should be supported.

Export data should maintain correctness according to the
[HookTest](https://github.com/Capitains/HookTest) suite.

### Add catalogue metadata

In addition to the ATF-format transcription data, CDLI publishes
a csv-format catalog of each record. The conversion tool should
read this and represent relevant fields in the teiHeader, so
the xml documents are a more complete representation of the
texts. At a minimum there should be publication references
and urls for the hand-drawn copies and photographs of the
source object. This will provide viewer software with everything
it needs to present the same data as the main CDLI website.

I wrote a [python wrapper](https://github.com/cdli-gh/cdli-cts/blob/1813415/update/cdli.py)
for the catalog metadata. This should be packaged so it can be
shared between the various applications.

There are other data sources which can also be added,
either to the xml or the viewer. There are lemma and
part of speech annotation data for many tablets from
mtaac, oracc, and other projects.

### Develop a Scaife parallel reader

Scaife right now expects text and translation as separate, long
documents. That makes some sense given the history of the scholarship
they're supporting. We have short documents where photo, copy,
transliteration, normalization and translation are usually thought
of line-by-line together. Ideally all of these could be shown/hidden
independently, and transition between parallel and interlinear
presentations depending on screen size.

I would like to see my proof-of-concept *CDLI Reader* component
developed into a proper modular set of files which could be easily
added to any Scaife instance to support cuneiform documents.

### Develop full-text search

I wrote a quick script to upload the catalog metadata to
Elasticsearch where is could be searched as a full text.
It didn't do better than the general search on the current
CDLI website, but with some tuning it should be possible
to improve things.

For example, searching for a tablet reference like 'K 162'
should find P345482, the primary example of the Akkadian
*Descent of Ishtar* text, without the user having to know
to search for 'K 00162' in the accession number field.

If the atf data is also uploaded and indexed appropriately,
the service could provide easy programmatic access to the
whole corpus from a very small codebase, loaded directly
from the published data set.

## Open problems

### Find a js library to sanitize html code.

To get good typography for transliteration lines we need markup for
determinative, logograms and damage. Those should be represented
by tei elements in the document served by CTS and converted to html
elements like `<sup>` and `<span>` with custom classes for display.
That's not too hard, but to protect against cross-site scripting
the entire xml tree must be checked and cleaned of elements we don't
want, which isn't something we should write ourselves.

Suggestions welcome. Scaife avoids this issue by serving plain unicode
text, which works ok for greek and latin, but not for us.

### pyoracc doesn't handle enough of the CDLI atf files.

The parser is strict, but what's in the library hasn't been carefully
validated, so it rejects many entries.

I did a lot of cleanup work on the library, but it wasn't
possible to get it handling the whole CDLI corpus within the term.
Over the long term, syntax errors with the ATF in the database
should be corrected, ingest should do more validation to reduce
new errors, and pyoracc should be extended to support common features
of the CDLI corpus.

For future work, I'd also want to revisit my ad-hoc, line-based parser
and see if that can get more documents available. ATF is a simple
format and a permissive parser might work better for an application
like this where we're just trying to present the corpus as it is.

### Localization.

An Arabic interface translation is something we'd like to do for the
reader. Scaife-viewer is using django to do this, can try one of the
vue.js packages on the readhomer re-write.

### CTS GetCapabilities doesn't scale.

Returning the whole CDLI corpus in a single query is too much data.
Capitains is also quite slow indexing a large corpus.
I opened an issue with scaife-viewer to figure out a shared way to
address this.
[DTS](https://distributed-text-services.github.io/specifications/) (ld-json)
or ATLAS (graphql) are options.
