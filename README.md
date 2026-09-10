# homebrew-tap

The Homebrew tap for [trustdiff](https://github.com/vahapogut/trustdiff), a single binary that finds trust regressions in a project's dependency tree before they land.

```sh
brew install --cask vahapogut/tap/trustdiff
```

The cask is named in full on purpose. Since Homebrew 6.0 a tap that is not one of Homebrew's own has to be trusted before its code will run, and installing a fully qualified name trusts that one cask and nothing else. Tapping first and then installing the short name needs a separate `brew trust --cask vahapogut/tap/trustdiff`, and `brew trust vahapogut/tap` accepts everything this tap will ever hold, which is more than anyone should hand a third party.

## What is in here

One generated file, `Casks/trustdiff.rb`, beside this README and the license. It is written by [goreleaser](https://goreleaser.com) from `.goreleaser.yaml` in the trustdiff repository and committed here by the release workflow every time a version tag is pushed. The first two versions, v0.4.0 and v0.4.1, were committed by hand instead, because the release job had no token for this repository at the time: they are the same generated files, with every digest taken from the release's own cosign-verified `checksums.txt` and every archive downloaded and checked against it first. Nothing here is edited by hand for any other reason, so a pull request against it would be overwritten by the next release. Changes belong in [vahapogut/trustdiff](https://github.com/vahapogut/trustdiff), where the cask is generated from.

A release candidate, meaning a tag with a suffix such as `v1.2.3-rc.1`, is deliberately not published here. That is what makes one safe to push: it exercises the whole release pipeline without moving what `brew upgrade` would hand to somebody.

## Verifying a download yourself

The cask installs the same archive the releases page serves, and Homebrew checks it against the sha256 recorded in the cask. That is a real check, but the sha256 and the archive it describes were produced by the same job, so it proves the download was not altered in transit and not much more.

Every trustdiff release also ships `checksums.txt`, a cosign signature over it, an SBOM per archive and GitHub build provenance. To check the chain rather than trust this repository, download the archive from the [releases page](https://github.com/vahapogut/trustdiff/releases) and follow the three steps in the trustdiff README. They verify the signature against the release workflow's own identity, which is the part a tap cannot do for you.

## License

trustdiff is Apache-2.0, and so is the cask generated from it. See [LICENSE](LICENSE).
