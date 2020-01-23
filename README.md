# gtdb-ident - rapid taxonomic classification against the GTDB

The `gtdb-ident` script performs quick and dirty taxonomic assignment of
genomic sequences to the [GTDB taxonomy](https://gtdb.ecogenomic.org/).

Home: <https://github.com/zwets/gtdb-ident>


## Background

[GTDB-Tk](https://github.com/Ecogenomics/GTDBTk) (see
[Chaumeil et al. (2019)](https://doi.org/10.1093/bioinformatics/btz848)),
performs highly accurate taxonomic assignment of genomes to the GTDB (see
[Parks et al. (2018)](https://www.nature.com/articles/nbt.4229))
but at the cost of high memory and run-time requirements.

`gtdb-ident` is a wrapper script that invokes
[Kmer-db](https://github.com/refresh-bio/kmer-db) to rapidly find the GTDB
representative genome (see
[Parks et al. (2019)](https://www.biorxiv.org/content/10.1101/771964v2))
closest to the query genome.


## Running

```bash
./gtdb-ident examples/genome.fna.gz examples/myreads.fq.gz ...
```


## Installation

* Install the GTDB-Tk reference data

  Follow <https://github.com/Ecogenomics/GTDBTk#gtdb-tk-reference-data> to
  download and unpack the GTDB reference data.  If you have already installed
  GTDB-Tk, you will have this data at `GTDBTK_DATA_PATH`.

  Either point `GTDBTK_DATA_PATH` at the unpacked data (as for GTDB-Tk), or
  create a symlink named `gtdb-data` to it in `gtdb-ident`'s directory:

      ln -sfT /path/to/releaseXX ./gtdb-data

* Install Kmer-db

  Follow the [Kmer-db](https://github.com/refresh-bio/kmer-db) instructions
  to install Kmer-db.

  Either put the `kmer-db` binary on the `PATH`, or create a symlink to it in
  `gtdb-ident`'s directory:

      ln -sfT /path/to/kmer-db/kmer-db ./kmer-db

* \[Optional\] Pre-index the database

  When you run `gtdb-ident` the first time, or whenever it detects that its
  index is older than the files at `GTDBTK_DATA_PATH` or `./gtdb-data/`, then
  it (re)creates its index in `./data/`.

      ./gtdb-ident  # Generates index

  The indexing process takes a while time and generates a large (15G) file
  in `./data/`.

* \[Optional\] Remove the GTDB-Tk data reference data

  Once indexing is done you may remove the GTDB-Tk reference data, as
  `gtdb-ident` retains all information in its index at `./data`.


#### Licence

gtdb-ident - rapid taxonomic classification against the GTDB
Copyright (C) 2019  Marco van Zwetselaar <io@zwets.it>  

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

