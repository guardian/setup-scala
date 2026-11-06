# Setup Scala

_Combining [`setup-java`](https://github.com/actions/setup-java) & [`setup-sbt`](https://github.com/sbt/setup-sbt) with good defaults for the Guardian_

### How to use

Get rid of this:

```yaml
      - name: Setup JDK
        uses: actions/setup-java@v4
        with:
          distribution: corretto
          java-version: 21
          cache: sbt
```

and replace it with this:

```yaml
      - uses: guardian/setup-scala@v2
```

Specifically:

* In your GitHub Action workflow definition (eg `ci.yml`), under `steps:`:
  * Remove the `setup-java` step and its config (and `setup-sbt` if you have it)
  * Add `- uses: guardian/setup-scala@v2` where the `actions/setup-java` config was ([example](https://github.com/guardian/prout/blob/1bee0f158601d85697739151c4d4dce1bf28062b/.github/workflows/ci.yml#L18))
* Add a `.tool-versions` file if you don't already have one, specifying the version of Java you want to use ([example](https://github.com/guardian/setup-scala/blob/56ec952f11409b28f4f7ae8d442e4d6deb87fc68/.tool-versions#L1))

[Example PR](https://github.com/guardian/etag-caching/pull/60) removing `setup-java` and installing `setup-scala`.

### Java version

* Java distribution used: always the [AWS Corretto](https://aws.amazon.com/corretto/) distribution of Java,
  the standard Java distro used at the Guardian.

Note that (like [`gha-scala-library-release-workflow`](https://github.com/guardian/gha-scala-library-release-workflow/pull/36)) `guardian/setup-scala`
requires that projects specify their Java version with an [`asdf`](https://asdf-vm.com/)-formatted `.tool-versions` file.

##### Only Java _major_ version is respected

Although `asdf` requires a fully-specified Java version (eg `21.0.3.9.1`) in the `.tool-versions` file,
currently the workflow will only match the *major* version of Java specified in the file (eg `21`).

This is due to [limitations](https://github.com/actions/setup-java/issues/615) in [`actions/setup-java`](https://github.com/actions/setup-java).
