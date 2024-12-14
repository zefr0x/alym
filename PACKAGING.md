# Packaging

[![Please do not ship work in progress to users](https://dont-ship.it/dontshipwip.svg)](https://dont-ship.it/)

## Releases

### What is a release?

The [Semantic Versioning](https://semver.org/) is used for version numbering in this project.

A release is a [git tag](https://git-scm.com/docs/git-tag) in the `main` branch of the project's git repositry that starts with the letter `v` followed by the Semantic Versioning based version number.

### Creating a new release

1. Update the version number in the [`Cargo.toml`](https://github.com/zefr0x/alym/blob/main/Cargo.toml) file.
2. Build the project to update the `Cargo.lock` file and to test it before publishing the release.
3. Write what happend from fixes, changes and updates and every thing in this release to the [CHANGELOG.md](https://github.com/zefr0x/alym/blob/main/CHANGELOG.md) file.
4. Create a git commit with all of those changes.
5. Create a signed git tag with a `v` letter followed by the version number e.g. for `v1.5.3` you should do `git tag -s v1.5.3`.
6. Push changes to the remote using `git push origin main --tags`

## Packages

- [Cargo](https://doc.rust-lang.org/stable/cargo/) is used for installing the application ether directly in a system or inside a fake root to create a package.

### AUR

To be added...

### What should be packaged?

Only stable [releases](#releases) should be packaged. Not an `alpha` nor a `beta` releases should be.
