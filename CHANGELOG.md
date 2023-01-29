# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## Releases

### [0.1.5] - 2023-01-29

* Add more documentation

### [0.1.4] - 2023-01-29

* Change path to SQL directory to a relative one (execution from vendor directory)

### [0.1.3] - 2023-01-29

* Add overview of configuration

### [0.1.2] - 2023-01-29

* Add new documentation

### [0.1.1] - 2023-01-28

* Change .env access (available from vendor execution)

### [0.1.0] - 2023-01-28

* Initial release
* Add bin/db-dumper
* Add README.md
* Add LICENSE.md

## Add new version

```bash
# Checkout master branch
$ git checkout main && git pull

# Check current version
$ vendor/bin/version-manager --current

# Increase patch version
$ vendor/bin/version-manager --patch

# Change changelog
$ vi CHANGELOG.md

# Push new version
$ git add CHANGELOG.md VERSION && git commit -m "Add version $(cat VERSION)" && git push

# Tag and push new version
$ git tag -a "$(cat VERSION)" -m "Version $(cat VERSION)" && git push origin "$(cat VERSION)"
```
