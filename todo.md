# Current todo list

In the near term

- Complete class model for TEI serialization. (done)
- Generate and poke in CTS metadata in atf2cts. (done)
- Modularize changes to readhomer.
- Improve conversion to pass HookTest. (mostly done; capytains bugs)
- Complete atf line markup generation.
  - tag words
  - tag damaged signs.
  - tag restored text.
- Report atf syntax problems as issues on cdli-gh/data. (ongoing progress)
  - https://github.com/cdli-gh/data/issues?q=label:"atf+syntax"

In the medium term

- Set up automated conversion and publication to cdli-cts. (done)
- Merge metadata from csv export.
- Continue to report atf syntax problems with the database.
- Figure out Nautilus/HookTest performance problems.
  - Bugs? Slow algorithms?
  - Write my own sketch to understand the problem better.
- Handle line markup rendering in scaife.
- Make scaife reader switch between parallel and interlinear display.

Further ideas

- Figure out something for search!
  - https://github.com/cdli-gh/cdli-search
- Merge conll annotation data.
- Write 'lax' line-based parser for pyoracc.
  - Handle variants in the cdli atf.
  - Issue warnings.
- Improve HookTest to give command-line feedback.
- GraphQL mockup as research for ATLAS.
- Containerize current cdli data export for the new framework.
- Move framework passwords into non-repo config.
- Get cdli.ucla.edu deploying from a repo.
  - Requires going though a filesystem image and merging changes.
  - Move secrets out of the tree.
  - Then we can publish the repo!
