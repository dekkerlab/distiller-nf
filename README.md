# distiller-nf

[![Build Status](https://travis-ci.org/mirnylab/distiller-nf.svg?branch=master)](https://travis-ci.org/mirnylab/distiller-nf)
[![Join the chat at https://gitter.im/mirnylab/distiller](https://badges.gitter.im/mirnylab/distiller.svg)](https://gitter.im/mirnylab/distiller?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![DOI](https://zenodo.org/badge/89316568.svg)](https://zenodo.org/badge/latestdoi/89316568)

## A modular Hi-C mapping pipeline for reproducible data analysis.

The `distiller` pipeline aims to provide the following functionality:

- Align the sequences of Hi-C molecules to the reference genome
- Parse .sam alignment and form files with Hi-C pairs
- Filter PCR duplicates
- Aggregate pairs into binned matrices of Hi-C interactions

### Installation

Requirements:

- java 8
- [nextflow](https://www.nextflow.io/)
- docker (should be able to run w/o root privileges, 
[tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04))

To setup a new project, execute the following line in the project folder:

```sh
$ nextflow clone mirnylab/distiller-nf ./
```

This will download the distiller pipeline and the configuration files.

Then:
- configure the location of the input files and other project details
in `project.yml`
- configure additional parameters in `nextflow.config`
- use provided hardware configurations using `local` and `cluster` profiles, or provide your own using `custom` profile

Launch distiller depending on your usage scenario:

1. default hardware settings `./configs/local.config` with your `project.yml`:
```sh
$ nextflow run distiller.nf -params-file project.yml
```
2. `cluster` hardware profile `./configs/cluster.config` with your `project.yml`:
```sh
$ nextflow run distiller.nf -params-file project.yml -profile cluster
```
3. `custom` hardware profile with your own configuration file and your `project.yml`:
```sh
$ nextflow run distiller.nf -params-file project.yml -profile custom --custom_config /full/path/to/your.config
```


### Test example

In a new project folder, execute:

```sh
$ nextflow clone mirnylab/distiller-nf  ./
$ bash setup_test.sh
$ nextflow distiller.nf -params-file ./test/test_project.yml 
```

### blah blah - this is a temporary branch
### aws related stuff

That's how one would launch this branch of distiller on awsbatch:
```sh
nextflow run -bucket-dir s3://nf_bucket/run_data -profile custom,docker,awsbatch --custom_config /full/path/realaws.config --aws_config /full/path/aws_credentials.config -params-file project.yml distiller.nf
```

