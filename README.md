# documenation-public README

This is a test repo for the next version of ActiveState Platform documentation.

## Setup

1. Clone the [documentation-public](https://github.com/ActiveState/documentation-public.git) repo

2. Create a pre-commit hook file (`.git/hooks/pre-commit`) with the following content:

```text
#!/bin/sh
# .git/hooks/pre-commit
echo 'Compiling site...'
# Running the gc step so that we do not check-in the files used to
# Setup the development mode. Those are not needed in production.
hugo --gc
# Add the docs folder to Github.
git add docs/*
```

3. Give the file execution rights:

```text
chmod +x .git/hooks/pre-commit
```

4. Download the `hugo` binary and save it to a folder that's on your PATH, or update you PATH.
  
  * We're currently using the [extended build of v0.63.2](https://github.com/gohugoio/hugo/releases/download/v0.63.2/hugo_extended_0.63.2_macOS-64bit.tar.gz) for macOS. Builds for other platforms are available on the [release page](https://github.com/gohugoio/hugo/releases/tag/v0.63.2).

  The minimum requirement is v0.60.0 extended.

5. Run `hugo server` from the root of the repostory to run the server locally, or commit changes and see the updates at [https://activestate.github.io/documentation-public](ttps://activestate.github.io/documentation-public).

Last updated: April 17, 2020
