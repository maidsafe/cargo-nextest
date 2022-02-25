# cargo-nextest

Github action for performing a test run using [Nextest](https://nexte.st/index.html).

This action will install the Nextest runner, perform a test run, then upload Junit reports as
artifacts.

Right now, it only supports a certain subset of the options exposed by the `run` command.

The action is used by specifying a name for the test run, the Nextest profile (which should be added
to your repository), and the Junit path specified in the profile, along with various other optional
values. The name for the run is used to name the Junit reports artifacts that are uploaded, so that
the caller can then reference and publish them at some later stage in the workflow.

Example:
```
- name: Run client tests
  uses: jacderida/cargo-nextest@initial
  with:
    test-run-name: e2e-client-${{ matrix.os }}
    profile: ci
    junit-path: junit.xml
    package: safe_network
    release: true
    features: test-utils
    filters: client
    test-threads: 2
  timeout-minutes: 25
```
