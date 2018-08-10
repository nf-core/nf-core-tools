# {{ cookiecutter.pipeline_name }}

{{ cookiecutter.pipeline_short_description }}

[![Build Status](https://travis-ci.org/{{ cookiecutter.github_repo }}.svg?branch=master)](https://travis-ci.org/{{ cookiecutter.github_repo }})
[![Nextflow](https://img.shields.io/badge/nextflow-%E2%89%A50.30.0-brightgreen.svg)](https://www.nextflow.io/)
[![install with bioconda](https://img.shields.io/badge/install%20with-bioconda-brightgreen.svg)](http://bioconda.github.io/)
[![Docker](https://img.shields.io/docker/automated/{{ cookiecutter.dockerhub_slug }}.svg)](https://hub.docker.com/r/{{ cookiecutter.dockerhub_slug }})
![Singularity Container available](
https://img.shields.io/badge/singularity-available-7E4C74.svg)

### Introduction
{{ cookiecutter.pipeline_name }}: {{ cookiecutter.pipeline_short_description }}

The pipeline is built using [Nextflow](https://www.nextflow.io), a workflow tool to run tasks across multiple compute infrastructures in a very portable manner. It comes with docker / singularity containers making installation trivial and results highly reproducible.


# {{ cookiecutter.pipeline_name }} Documentation

 The {{ cookiecutter.pipeline_name }} documentation is split into the following files:
 1. [Installation](installation.md)
2. Pipeline configuration
    * [Local installation](configuration/local.md)
    * [Adding your own system](configuration/adding_your_own.md)
3. [Running the pipeline](usage.md)
4. [Output and how to interpret the results](output.md)
5. [Troubleshooting](troubleshooting.md)

### Credits
This pipeline was written by {{ cookiecutter.author_name }} ([{{ cookiecutter.author_github_username }}]({{ cookiecutter.author_homepage }})) at [{{ cookiecutter.author_affiliation }}]({{ cookiecutter.author_affiliation_homepage }}).

