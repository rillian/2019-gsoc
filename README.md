# 2019 Google Summer of Code Project

From June through August of 2019 I wrote a
[Text Encoding Initiative](https://tei-c.org://tei-c.org/)
exporter for the [Cuneiform Digital Library Initiative](https://cdli.ucla.edu),
to make data from cuneiform tablets and other inscriptions more accessible,
in particular to the [Scaife](https://scaife-viewer.org) reading environment.
[Project link](https://summerofcode.withgoogle.com/projects/#5983146665836544).

This is a summary of what I accomplished.

## Demonstration

The project itself didn't have a public staging server, so I set
up a temporary one on my own domain.

 - Visit the test server at https://cdli.thaumas.net/scaife/
   (If necessary, click the gear and enable the 'CDLI Reader'.)
 - Enter X001001 and click **Lookup**.
 - Click **Translation** to show/hide the parallel translation.

## Milestones

- [x] Convert a document from ATF and display it in Scaife.
- [ ] Publish a repo with a subset of convertable records.
- [ ] Set up automated export from CDLI data to a CTS repo.
- [ ] Integrate with the cdli website.

# Code

 - https://github.com/cdli-gh/atf2tei (document converter)
 - https://github.com/cdli-gh/cdli-cts (tei export target repo)
 - https://github.com/cdli-gh/cdli-cts-server (capitains server for
cdli-cts)
 - https://github.com/rillian/readhomer (scaife fork; check cdli branch)
 - https://github.com/oracc/pyoracc (parser atf2tei is using)

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

 - Reported various atf syntax inconsistencies I found to @epp
   who corrected the master database.

## Open problems

### Find a js library to sanitize html code.

To get good typography for transliteration lines we need markup for
determinatives, logograms and damage. Those should be represented
by tei elements in the document served by CTS and converted to html
elements like `<sup>` and `<span>` with custom classes for display.
That's not too hard, but to protect against cross-site scripting
the entire xml tree must be checked and cleaned of elements we don't
want, which isn't something we should write ourselves.

Suggestions welcome. Scaife avoids this issue by serving plain unicode
text, which works ok for greek and latin, but not for us.

### pyoracc doesn't handle enough of the cdli atf files.

The parser is strict, but what's in the library hasn't been carefully
validated, so it rejects many entries.

I've done a lot of cleanup work on the library and am happy to keep
working on it, but I don't expect I can get it handling the whole cdli
corpus by the end of the summer. I want to revisit my ad hoc line-based
parser and if that can get more documents available in the time available.

### Parallel reader.

Scaife right now expects text and translation as separate, long
documents. That makes some sense given the history of the scholarship
they're supporting. We have short documents where photo, copy,
transliteration, normalization and translation are usually thought
of line-by-line together.

Would like to work with the scaife people to develop something which
meets our needs in the context of other projects. For example, it would
be nice if all of the above could be shown/hidden independently, and
transitioned between parallel and interlinear presentations depending on
screen size.

So far upstream hasn't been very responsive, and I'm not a front-end
developer, so we'll probably end up with something that's a technical
proof-of-concept but will need further work after the project finishes.

### Localization.

An Arabic interface translation is something we'd like to do for the
reader. Scaife-viewer is using django to do this, can try one of the
vue.js packages on the readhomer re-write.

### CTS GetCapabilities doesn't scale.

Returning the whole cdli corpus in a single query is too much data.
Opened an issue with scaife-viewer to figure out a shared way to
address this. DTS (ld-json) or ATLAS (graphql) are options.
