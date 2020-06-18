# nf-core/tools: Changelog

## v1.10dev

### Tools helper code

* Allow multiple container tags in `ci.yml` if performing multiple tests in parallel

### Template

* Add `--publish_dir_mode` parameter [#585](https://github.com/nf-core/tools/issues/585)
* Isolate R library paths to those in container [#541](https://github.com/nf-core/tools/issues/541)
* Added new style of pipeline parameters JSON schema to pipeline template
* Add ability to attach MultiQC reports to completion emails when using `mail`
* Update `output.md` and add in 'Pipeline information' section describing standard NF and pipeline reporting.
* Build Docker image using GitHub Actions, then push to Docker Hub (instead of building on Docker Hub)
* New Slack channel badge in pipeline readme
* Add AWS CI tests and full tests GitHub Actions workflows
* Update AWS CI tests and full tests secrets names
* Replace and improve `check_max()` with `set_resource()`, which is already used in `nf-core/sarek`

### Linting

* Refactored PR branch tests to be a little clearer.
* Linting error docs explain how to add an additional branch protecton rule to the `branch.yml` GitHub Actions workflow.
* Adapted linting docs to the new PR branch tests.
* Failure for missing the readme bioconda badge is now a warn, in case this badge is not relevant
* Added test for template `{{ cookiecutter.var }}` placeholders
* Fix failure when providing version along with build id for Conda packages
* New `--json` and `--markdown` options to print lint results to JSON / markdown files
* Linting code now automatically posts warning / failing results to GitHub PRs as a comment if it can
* Added AWS GitHub Actions workflows linting

### Other

* Added CI test to check for PRs against `master` in tools repo
* CI PR branch tests fixed & now automatically add a comment on the PR if failing, explaining what is wrong
* Describe alternative installation method via conda with `conda env create`
* Move some of the issue and PR templates into HTML `<!-- comments -->` so that they don't show in issues / PRs
* Added `macs_gsize` for danRer10, based on [this post](https://biostar.galaxyproject.org/p/18272/)
* nf-core/tools version number now printed underneath header artwork
* Bumped Conda version shipped with nfcore/base to 4.8.2
* Added log message when creating new pipelines that people should talk to the community about their plans

## v1.9

### Continuous integration

* Travis CI tests are now deprecated in favor of GitHub Actions within the pipeline template.
  * `nf-core bump-version` support has been removed for `.travis.yml`
  * `nf-core lint` now fails if a `.travis.yml` file is found
* Ported nf-core/tools Travis CI automation to GitHub Actions.
* Fixed the build for the nf-core/tools API documentation on the website

### Template

* Rewrote the documentation markdown > HTML conversion in Python instead of R
* Fixed rendering of images in output documentation [#391](https://github.com/nf-core/tools/issues/391)
* Removed the requirement for R in the conda environment
* Make `params.multiqc_config` give an _additional_ MultiQC config file instead of replacing the one that ships with the pipeline
* Ignore only `tests/` and `testing/` directories in `.gitignore` to avoid ignoring `test.config` configuration file
* Rephrase docs to promote usage of containers over Conda to ensure reproducibility
* Stage the workflow summary YAML file within MultiQC work directory

### Linting

* Removed linting for CircleCI
* Allow any one of `params.reads` or `params.input` or `params.design` before warning
* Added whitespace padding to lint error URLs
* Improved documentation for lint errors
* Allow either `>=` or `!>=` in nextflow version checks (the latter exits with an error instead of just warning) [#506](https://github.com/nf-core/tools/issues/506)
* Check that `manifest.version` ends in `dev` and throw a warning if not
  * If running with `--release` check the opposite and fail if not
* Tidied up error messages and syntax for linting GitHub actions branch tests
* Add YAML validator
* Don't print test results if we have a critical error

### Other

* Fix automatic synchronisation of the template after releases of nf-core/tools
* Improve documentation for installing `nf-core/tools`
* Replace preprint by the new nf-core publication in Nature Biotechnology :champagne:
* Use `stderr` instead of `stdout` for header artwork
* Tolerate unexpected output from `nextflow config` command
* Add social preview image
* Added a [release checklist](.github/RELEASE_CHECKLIST.md) for the tools repo

## v1.8

### Continuous integration

* GitHub Actions CI workflows are now included in the template pipeline
  * Please update these files to match the existing tests that you have in `.travis.yml`
* Travis CI tests will be deprecated from the next `tools` release
* Linting will generate a warning if GitHub Actions workflows do not exist and if applicable to remove Travis CI workflow file i.e. `.travis.yml`.

### Tools helper code

* Refactored the template synchronisation code to be part of the main nf-core tool
* `nf-core bump-version` now also bumps the version string of the exported conda environment in the Dockerfile
* Updated Blacklist of synced pipelines
* Ignore pre-releases in `nf-core list`
* Updated documentation for `nf-core download`
* Fixed typo in `nf-core launch` final command
* Handle missing pipeline descriptions in `nf-core list`
* Migrate tools package CI to GitHub Actions

### Linting

* Adjusted linting to enable `patch` branches from being tested
* Warn if GitHub Actions workflows do not exist, warn if `.travis.yml` and circleCI are there
* Lint for `Singularity` file and raise error if found [#458](https://github.com/nf-core/tools/issues/458)
* Added linting of GitHub Actions workflows `linting.yml`, `ci.yml` and `branch.yml`
* Warn if pipeline name contains upper case letters or non alphabetical characters [#85](https://github.com/nf-core/tools/issues/85)
* Make CI tests of lint code pass for releases

### Template pipeline

* Fixed incorrect paths in iGenomes config as described in issue [#418](https://github.com/nf-core/tools/issues/418)
* Fixed incorrect usage of non-existent parameter in the template [#446](https://github.com/nf-core/tools/issues/446)
* Add UCSC genomes to `igenomes.config` and add paths to all genome indices
* Change `maxMultiqcEmailFileSize` parameter to `max_multiqc_email_size`
* Export conda environment in Docker file [#349](https://github.com/nf-core/tools/issues/349)
* Change remaining parameters from `camelCase` to `snake_case` [#39](https://github.com/nf-core/hic/issues/39)
  * `--singleEnd` to `--single_end`
  * `--igenomesIgnore` to `--igenomes_ignore`
  * Having the old camelCase versions of these will now throw an error
* Add `autoMounts=true` to default singularity profile
* Add in `markdownlint` checks that were being ignored by default
* Disable ansi logging in the travis CI tests
* Move `params`section from `base.config` to `nextflow.config`
* Use `env` scope to export `PYTHONNOUSERSITE` in `nextflow.config` to prevent conflicts with host Python environment
* Bump minimum Nextflow version to `19.10.0` - required to properly use `env` scope in `nextflow.config`
* Added support for nf-tower in the travis tests, using public mailbox nf-core@mailinator.com
* Add link to [Keep a Changelog](http://keepachangelog.com/en/1.0.0/) and [Semantic Versioning](http://semver.org/spec/v2.0.0.html) to CHANGELOG
* Adjusted `.travis.yml` checks to allow for `patch` branches to be tested
* Add Python 3.7 dependency to the `environment.yml` file
* Remove `awsbatch` profile cf [nf-core/configs#71](https://github.com/nf-core/configs/pull/71)
* Make `scrape_software_versions.py` compatible with Python3 to enable miniconda3 in    [base image PR](https://github.com/nf-core/tools/pull/462)
* Add GitHub Actions workflows and respective linting
* Add `NXF_ANSI_LOG` as global environment variable to template GitHub Actions CI workflow
* Fixed global environment variable in GitHub Actions CI workflow
* Add `--awscli` parameter
* Add `README.txt` path for genomes in `igenomes.config` [nf-core/atacseq#75](https://github.com/nf-core/atacseq/issues/75)
* Fix buggy ANSI codes in pipeline summary log messages
* Add a `TODO` line in the new GitHub Actions CI test files

### Base Docker image

* Use miniconda3 instead of miniconda for a Python 3k base environment
  * If you still need Python 2 for your pipeline, add `conda-forge::python=2.7.4` to the dependencies in your `environment.yml`
* Update conda version to 4.7.12

### Other

* Updated Base Dockerfile to Conda 4.7.10
* Entirely switched from Travis-Ci.org to Travis-Ci.com for template and tools
* Improved core documentation (`-profile`)

## v1.7

### Tools helper code

* The tools `create` command now sets up a `TEMPLATE` and a `dev` branch for syncing
* Fixed issue [379](https://github.com/nf-core/tools/issues/379)
* nf-core launch now uses stable parameter schema version 0.1.0
* Check that PR from patch or dev branch is acceptable by linting
* Made code compatible with Python 3.7
* The `download` command now also fetches institutional configs from nf-core/configs
* When listing pipelines, a nicer message is given for the rare case of a detached `HEAD` ref in a locally pulled pipeline. [#297](https://github.com/nf-core/tools/issues/297)
* The `download` command can now compress files into a single archive.
* `nf-core create` now fetches a logo for the pipeline from the nf-core website
* The readme should now be rendered properly on PyPI.

### Syncing

* Can now sync a targeted pipeline via command-line
* Updated Blacklist of synced pipelines
* Removed `chipseq` from Blacklist of synced pipelines
* Fixed issue [#314](https://github.com/nf-core/tools/issues/314)

### Linting

* If the container slug does not contain the nf-core organisation (for example during development on a fork), linting will raise a warning, and an error with release mode on

### Template pipeline

* Add new code for Travis CI to allow PRs from patch branches too
* Fix small typo in central readme of tools for future releases
* Small code polishing + typo fix in the template main.nf file
* Header ANSI codes no longer print `[2m` to console when using `-with-ansi`
* Switched to yaml.safe_load() to fix PyYAML warning that was thrown because of a possible [exploit](https://github.com/yaml/pyyaml/wiki/PyYAML-yaml.load(input)-Deprecation)
* Add `nf-core` citation
* Add proper `nf-core` logo for tools
* Add `Quick Start` section to main README of template
* Fix [Docker RunOptions](https://github.com/nf-core/tools/pull/351) to get UID and GID set in the template
* `Dockerfile` now specifically uses the proper release tag of the nfcore/base image
* Use [`file`](https://github.com/nf-core/tools/pull/354) instead of `new File`
  to avoid weird behavior such as making an `s3:/` directory locally when using
  an AWS S3 bucket as the `--outdir`.
* Fix workflow.onComplete() message when finishing pipeline
* Update URL for joining the nf-core slack to [https://nf-co.re/join/slack](https://nf-co.re/join/slack)
* Add GitHub Action for CI and Linting
* [Increased default time limit](https://github.com/nf-core/tools/issues/370) to 4h
* Add direct link to the pipeline slack channel in the contribution guidelines
* Add contributions and support heading with links to contribution guidelines and link to the pipeline slack channel in the main README
* Fix Parameters JSON due to new versionized structure
* Added conda-forge::r-markdown=1.1 and conda-forge::r-base=3.6.1 to environment
* Plain-text email template now has nf-core ASCII artwork
* Template configured to use logo fetched from website
* New option `--email_on_fail` which only sends emails if the workflow is not successful
* Add file existence check when checking software versions
* Fixed issue [#165](https://github.com/nf-core/tools/issues/165) - Use `checkIfExists`
* Consistent spacing for `if` statements
* Add sensible resource labels to `base.config`

### Other

* Bump `conda` to 4.6.14 in base nf-core Dockerfile
* Added a Code of Conduct to nf-core/tools, as only the template had this before
* TravisCI tests will now also start for PRs from `patch` branches, [to allow fixing critical issues](https://github.com/nf-core/tools/pull/392) without making a new major release

## v1.6

### Syncing

* Code refactoring to make the script more readable
* No travis build failure anymore on sync errors
* More verbose logging

### Template pipeline

* awsbatch `work-dir` checking moved to nextflow itself. Removed unsatisfiable check in main.nf template.
* Fixed markdown linting
* Tools CI testing now runs markdown lint on compiled template pipeline
* Migrated large portions of documentation to the [nf-core website](https://github.com/nf-core/nf-co.re/pull/93)
* Removed Gitter references in `.github/` directories for `tools/` and pipeline template.
* Changed `scrape_software_versions.py` to output `.csv` file
* Added `export_plots` parameter to multiqc config
* Corrected some typos as listed [here](https://github.com/nf-core/tools/issues/348) to Guidelines

### Tools helper code

* Drop [nf-core/rnaseq](https://github.com/nf-core/rnaseq]) from `blacklist.json` to make template sync available
* Updated main help command to sort the subcommands in a more logical order
* Updated readme to describe the new `nf-core launch` command
* Fix bugs in `nf-core download`
  * The _latest_ release is now fetched by default if not specified
  * Downloaded pipeline files are now properly executable.
* Fixed bugs in `nf-core list`
  * Sorting now works again
  * Output is partially coloured (better highlighting out of date pipelines)
  * Improved documentation
* Fixed bugs in `nf-core lint`
  * The order of conda channels is now correct, avoiding occasional erroneous errors that packages weren't found ([#207](https://github.com/nf-core/tools/issues/207))
  * Allow edge versions in nf-core pipelines
* Add reporting of ignored errored process
  * As a solution for [#103](https://github.com/nf-core/tools/issues/103))
* Add Bowtie2 and BWA in iGenome config file template

## [v1.5](https://github.com/nf-core/tools/releases/tag/1.5) - 2019-03-13 Iron Shark

### Template pipeline

* Dropped Singularity file
* Summary now logs details of the cluster profile used if from [nf-core/configs](https://github.com/nf-core/configs)
* Dockerhub is used in favor of Singularity Hub for pulling when using the Singularity profile
* Changed default container tag from latest to dev
* Brought the logo to life
* Change the default filenames for the pipeline trace files
* Remote fetch of nf-core/configs profiles fails gracefully if offline
* Remove `params.container` and just directly define `process.container` now
* Completion email now includes MultiQC report if not too big
* `params.genome` is now checked if set, to ensure that it's a valid iGenomes key
* Together with nf-core/configs, helper function now checks hostname and suggests a valid config profile
* `awsbatch` executor requires the `tracedir` not to be set to an `s3` bucket.

### Tools helper code

* New `nf-core launch` command to interactively launch nf-core pipelines from command-line
  * Works with a `parameters.settings.json` file shipped with each pipeline
  * Discovers additional `params` from the pipeline dynamically
* Drop Python 3.4 support
* `nf-core list` now only shows a value for _"is local latest version"_ column if there is a local copy.
* Lint markdown formatting in automated tests
  * Added `markdownlint-cli` for checking Markdown syntax in pipelines and tools repo
* Syncing now reads from a `blacklist.json` in order to exclude pipelines from being synced if necessary.
* Added nf-core tools API description to assist developers with the classes and functions available.
  * Docs are automatically built by Travis CI and updated on the nf-co.re website.
* Introduced test for filtering remote workflows by keyword.
* Build tools python API docs
  * Use Travis job for api doc generation and publish

* `nf-core bump-version` now stops before making changes if the linting fails
* Code test coverage
  * Introduced test for filtering remote workflows by keyword
* Linting updates
  * Now properly searches for conda packages in default channels
  * Now correctly validates version pinning for packages from PyPI
  * Updates for changes to `process.container` definition

### Other

* Bump `conda` to 4.6.7 in base nf-core Dockerfile

## [v1.4](https://github.com/nf-core/tools/releases/tag/1.4) - 2018-12-12 Tantalum Butterfly

### Template pipeline

* Institutional custom config profiles moved to github `nf-core/configs`
  * These will now be maintained centrally as opposed to being shipped with the pipelines in `conf/`
  * Load `base.config` by default for all profiles
  * Removed profiles named `standard` and `none`
  * Added parameter `--igenomesIgnore` so `igenomes.config` is not loaded if parameter clashes are observed
  * Added parameter `--custom_config_version` for custom config version control. Can use this parameter to provide commit id for reproducibility. Defaults to `master`
  * Deleted custom configs from template in `conf/` directory i.e. `uzh.config`, `binac.config` and `cfc.config`
* `multiqc_config` and `output_md` are now put into channels instead of using the files directly (see issue [#222](https://github.com/nf-core/tools/issues/222))
* Added `local.md` to cookiecutter template in `docs/configuration/`. This was referenced in `README.md` but not present.
* Major overhaul of docs to add/remove parameters, unify linking of files and added description for providing custom configs where necessary
* Travis: Pull the `dev` tagged docker image for testing
* Removed UPPMAX-specific documentation from the template.

### Tools helper code

* Make Travis CI tests fail on pull requests if the `CHANGELOG.md` file hasn't been updated
* Minor bugfixing in Python code (eg. removing unused import statements)
* Made the web requests caching work on multi-user installations
* Handle exception if nextflow isn't installed
* Linting: Update for Travis: Pull the `dev` tagged docker image for testing

## [v1.3](https://github.com/nf-core/tools/releases/tag/1.3) - 2018-11-21

* `nf-core create` command line interface updated
  * Interactive prompts for required arguments if not given
  * New flag for workflow author
* Updated channel order for bioconda/conda-forge channels in environment.yaml
* Increased code coverage for sub command `create` and `licenses`
* Fixed nasty dependency hell issue between `pytest` and `py` package in Python 3.4.x
* Introduced `.coveragerc` for pytest-cov configuration, which excludes the pipeline template now from being reported
* Fix [189](https://github.com/nf-core/tools/issues/189): Check for given conda and PyPi package dependencies, if their versions exist
* Added profiles for `cfc`,`binac`, `uzh` that can be synced across pipelines
  * Ordering alphabetically for profiles now
* Added `pip install --upgrade pip` to `.travis.yml` to update pip in the Travis CI environment

## [v1.2](https://github.com/nf-core/tools/releases/tag/1.2) - 2018-10-01

* Updated the `nf-core release` command
  * Now called `nf-core bump-versions` instead
  * New flag `--nextflow` to change the required nextflow version instead
* Template updates
  * Simpler installation of the `nf-core` helper tool, now directly from PyPI
  * Bump minimum nextflow version to `0.32.0` - required for built in `manifest.nextflowVersion` check and access to `workflow.manifest` variables from within nextflow scripts
  * New `withName` syntax for configs
  * Travis tests fail if PRs come against the `master` branch, slightly refactored
  * Improved GitHub contributing instructions and pull request / issue templates
* New lint tests
  * `.travis.yml` test for PRs made against the `master` branch
  * Automatic `--release` option not used if the travis repo is `nf-core/tools`
  * Warnings if depreciated variables `params.version` and `params.nf_required_version` are found
* New `nf-core licences` subcommand to show licence for each conda package in a workflow
* `nf-core list` now has options for sorting pipeline nicely
* Latest version of conda used in nf-core base docker image
* Updated PyPI deployment to  correctly parse the markdown readme (hopefully!)
* New GitHub contributing instructions and pull request template

## [v1.1](https://github.com/nf-core/tools/releases/tag/1.1) - 2018-08-14

Very large release containing lots of work from the first nf-core hackathon, held in SciLifeLab Stockholm.

* The [Cookiecutter template](https://github.com/nf-core/cookiecutter) has been merged into tools
  * The old repo above has been archived
  * New pipelines are now created using the command `nf-core create`
  * The nf-core template and associated linting are now controlled under the same version system
* Large number of template updates and associated linting changes
  * New simplified cookiecutter variable usage
  * Refactored documentation - simplified and reduced duplication
  * Better `manifest` variables instead of `params` for pipeline name and version
  * New integrated nextflow version checking
  * Updated travis docker pull command to use tagging to allow release tests to pass
  * Reverted Docker and Singularity syntax to use `ENV` hack again
* Improved Python readme parsing for PyPI
* Updated Travis tests to check that the correct `dev` branch is being targeted
* New sync tool to automate pipeline updates
  * Once initial merges are complete, a nf-core bot account will create PRs for future template updates

## [v1.0.1](https://github.com/nf-core/tools/releases/tag/1.0.1) - 2018-07-18

The version 1.0 of nf-core tools cannot be installed from PyPi. This patch fixes it, by getting rid of the requirements.txt plus declaring the dependent modules in the setup.py directly.

## [v1.0](https://github.com/nf-core/tools/releases/tag/1.0) - 2018-06-12

Initial release of the nf-core helper tools package. Currently includes four subcommands:

* `nf-core list`: List nf-core pipelines with local info
* `nf-core download`: Download a pipeline and singularity container
* `nf-core lint`: Check pipeline against nf-core guidelines
* `nf-core release`: Update nf-core pipeline version number
