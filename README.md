# Setup Scala

_Combining [`setup-java`](https://github.com/actions/setup-java) & [`setup-sbt`](https://github.com/sbt/setup-sbt) with good defaults for the Guardian_

### Java version

* Java distribution used: always the [AWS Corretto](https://aws.amazon.com/corretto/) distribution of Java,
  the standard Java distro used at the Guardian.

Note that (like [`gha-scala-library-release-workflow`](https://github.com/guardian/gha-scala-library-release-workflow/pull/36)) `guardian/setup-scala`
requires that projects specify their Java version with an [`asdf`](https://asdf-vm.com/)-formatted `.tool-versions` file.

##### Only Java _major_ version is respected

Although `asdf` requires a fully-specified Java version (eg `21.0.3.9.1`) in the `.tool-versions` file,
currently the workflow will only match the *major* version of Java specified in the file (eg `21`).

This is due to [limitations](https://github.com/actions/setup-java/issues/615) in [`actions/setup-java`](https://github.com/actions/setup-java).
