# seeker

[![check-coverage-deploy](https://github.com/hugheylab/seeker/workflows/check-coverage-deploy/badge.svg)](https://github.com/hugheylab/seeker/actions)
[![codecov](https://codecov.io/gh/hugheylab/seeker/branch/master/graph/badge.svg)](https://codecov.io/gh/hugheylab/seeker)

`seeker` is an R package for fetching and processing sequencing data, especially RNA-seq data. Hopefully it helps you get what you're after, before the day you die.

## Installation

These instructions are for Linux. Slight modifications may be necessary for macOS. If you're using Windows, you're doing it wrong.

1. Download and install [Aspera Connect for Linux](https://www.ibm.com/aspera/connect/). You will likely have to download a tar.gz file (`wget`), untar it (`tar -zxvf`), then run the resulting shell script.

1. Install and set up Miniconda. See [here](https://bioconda.github.io/user/install.html#set-up-channels).

    ```sh
    curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    sh Miniconda3-latest-Linux-x86_64.sh
    
    conda config --add channels defaults
    conda config --add channels bioconda
    conda config --add channels conda-forge
    ```

1. Install the other command-line tools.

    ```sh
    conda install mamba -c conda-forge
    mamba install refgenie trim-galore fastqc fastq-screen salmon multiqc
    ```

1. Optionally, fetch the genomes for fastq-screen. This takes a long time, so don't bother unless you actually plan to run fastq-screen.

    ```sh
    fastq_screen --get_genomes
    ```

1. Configure refgenie. For example:

    ```sh
    mkdir /home/ubuntu/genomes
    refgenie init -c /home/ubuntu/genomes/genome_config.yaml
    printf "\nexport REFGENIE=/home/ubuntu/genomes/genome_config.yaml\n" >> ~/.bashrc
    source ~/.bashrc
    refgenie init
    ```

1. Fetch the salmon index files using refgenie. For example:

    ```sh
    refgenie pull hg38/salmon_sa_index
    refgenie pull mm10/salmon_sa_index
    ```

1. Install the `biomaRt` and `tximport` packages from Bioconductor.

    ```r
    if (!requireNamespace('BiocManager', quietly = TRUE))
      install.packages('BiocManager')
    BiocManager::install(c('biomaRt', 'tximport'))
    ```

1. Clone the git repo, build the source package, then do something like

    ```r
    install.packages('seeker_0.0.0.9001.tar.gz', type = 'source', repos = NULL)
    ```
