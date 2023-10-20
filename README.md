# rmats2sashimiplot

[![Latest Release](https://img.shields.io/github/release/Xinglab/rmats2sashimiplot.svg?label=Latest%20Release)](https://github.com/Xinglab/rmats2sashimiplot/releases/latest)
[![Total Bioconda Installs](https://img.shields.io/conda/dn/bioconda/rmats2sashimiplot.svg?label=Total%20Bioconda%20Installs)](https://anaconda.org/bioconda/rmats2sashimiplot)
[![PyPI Installs](https://img.shields.io/pypi/dm/rmats2sashimiplot.svg?label=PyPI%20Installs)](https://pypi.org/project/rmats2sashimiplot/)
[![Total Docker Pulls](https://img.shields.io/docker/pulls/xinglab/rmats2sashimiplot.svg?label=Total%20Docker%20Pulls)](https://hub.docker.com/r/xinglab/rmats2sashimiplot)

## About

This is a fork of the [rmats2sashimiplot](https://github.com/Xinglab/rmats2sashimiplot) repository by the Xing lab. It contains a quick fix for producing plots with unlimited amounts of samples and colours.

--- Still under development! If you want to contribute, please feel free to do so! ---

## Table of contents

- [Dependencies](#dependencies)
- [Install](#install)
- [Usage](#usage)
- [Output](#output)
- [Contacts and bug reports](#contacts-and-bug-reports)
- [Copyright and License Information](#copyright-and-license-information)

## Dependencies

- Python 2.7 (Python 3 can be used after running [2to3.sh](2to3.sh))
  * numpy
  * scipy
  * matplotlib
  * pysam
- Samtools
- bedtools

I recommend setting up a conda environment with the respective dependencies. This can be easily done using the provided environment file `conda.yaml`:
```
conda env create -f conda.yaml
```
Or for mamba users:
```
mamba env create -f conda.yaml
```

## Install

After cloning the repo, rmats2sasmimiplot can be run without installing:
```
python ./src/rmats2sashimiplot/rmats2sashimiplot.py
```

I recommend running rmats2sashimiplot without installing.

rmats2sashimiplot can be installed with:
```
python ./setup.py install
```

If installed, rmats2sashimiplot can be run with just:
```
rmats2sashimiplot
```

## Usage

**BAM files must be sorted before visualization/indexing.**

### Examples

#### BAM files with coordinate and annotation

The fix lets you specify multiple input samples with colors for each tracks:
 - `--b1` takes input bam files as a comma-separated list
 - `--l1` takes track labels as comma-separated list (lengths of `b1` and `l1` must match)
 - `--color` takes comma-separated list of colors in hex code, one color per track
 - `-c` takes the genome region coordinates and a GFF3 annotation file (format see below)
 - `--exon_s` and `--intron_s` take scale factors on how much to scale down exons/introns respectively.

```
cols=#ff8d17,#e77600,#b95e00,#8b4600
bams=./bams/sample1.bam,./bams/sample2.bam,./bams/sample3.bam,./bams/sample4.bam
labels=sample1,sample2,sample3,sample4
outdir=/path/to/outdir/
mkdir -p $outdir

python ./src/rmats2sashimiplot/rmats2sashimiplot.py \
    --b1 $bams \
    -c {chromosome}:{strand}:{start}:{end}:{/path/to/gff3} \
    --l1 $labels \
    --color $cols \
    --exon_s 1 \
    --intron_s 5 \
    --fig-height 12 \
    -o $outdir
```

## Output

All output is written to the directory specified by `-o`. Under that directory:

- `Sashimi_index/`: contains intermediate files used to create the plot
- `Sashimi_index_{Gene}_{event_id}/`: like `Sashimi_index/` but one directory for each rMATS event plotted
- `Sashimi_plot/`: contains the generated sashimi plots in .pdf format


## Contacts and bug reports

If you encounter a bug using this modified version, feel free to open an [issue]() and I will respond as soon as I can.

## Copyright and License Information

See [here](https://github.com/Xinglab/rmats2sashimiplot/#copyright-and-license-information).
