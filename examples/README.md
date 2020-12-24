# General Use Scripts

The scripts in this directory are used for testing and exploring [PySpark][], [Apache Arrow][],
and other frameworks while the main [wsprana][] application is being reworked.

All of the example scripts will be incorporated into the main app. Some of the
scripts in this folder will just be test scripts, like the `pandas_convert_csv.py`
and `pyarrow_read.py`, but they provide some insight as to what can be done
to reduce processing time and imporve file storage footprints.

## Environment Setup

If you are on `Windows -10` It's highly recommended that you use
`Windows Subsystem Linux v2`. Doing so will be far easier than setting up
[Apache Spark][] and you can follow the directions below to get things
going.

You need a `Python` Environment, either from [Anaconda Python][] or the standard
[Python][] installer. Either way, you should run the tests in a virtual
environment to keep package bloat to a minimum.

## Running The Tests

The first two tests will illistrate the speed increase in using [Apache Arrow][]
to process both CSV and [Apache Parquet][] Compressed binaries. The major difference
between the native CSV file, and those compressed by the `pandas_convert_csv.py`
script is, the CSV file has no schema nor header information accompanying
the file whereas the compressed binaries have full headers and types included.

[Pandas][], buy default, is a single thread reader/writer. It can be made to
pool, but it's not configured to do so out of the box. You will see the
difference in reading the Raw CSV file using [Pandas][] during the compression
run and that of [PyArrow][] running in parallel doing the same task.

To run the two test scripts, perform the following:

- Download the [wsprana repository][]
- Change directories into the testing directory `wsprana-spark-python/testing`
- Using pip, install the requires dependencies
- Make a data directory and download the wsprspots-2020-02.csv.gz file to it
- Unzip the wsprspot archiive
- Now you can run the conversion and read test scripts

Here's the commands from the shell

```bash

# Clone the repo
cd $USER/Downlaods

# Change directories and install dependencies
cd $HOME/Downlaods/wsprana-spark-python/examples

pip install -r requirements.txt

# Set the path of the downloaded and extracted CSV file
# I am using the $USER Downlaods folder as an example
csvfile="$HOME/Downloads/wsprspots-2002-02.csv"

# Now run the converter script
python pandas_convert_csy.py $csvfile
```

### Pandas Compression Test Results

The follwing data shows the results of converting several [Apache Parquet][]
formats. Substantial disk space conservation can be achived with little
very impact using as you'll see in the read tests. As the compression
increases, so does the length of time it takes to create the file. However,
the disk savings are substantial. Using [Apache Spark][], read times are on par
with the results you'll see form the [Apache Arrow][] read tests ( Very Fast !! ), 

>NOTE : make note of the CSV Read Time while using [Pandas] a Single Thead 

```bash
Pandas CSV Conversion Method
Parquet Compression Types : ['SNAPPY', 'LZ4', 'ZSTD', 'GZIP', 'BROTLI']
Sit back and relax, this takes a while!!

* Reading file  : wsprspots-2020-02.csv
* Spot Count    : 47,310,649
* File Size     : 3780.94 MB
* Elapsed Time  : 80.42 sec

* Converting CSV to -> snappy
* File Size     : 667.07 MB
* Elapsed Time  : 30.039 sec

* Converting CSV to -> lz4
* File Size     : 627.88 MB
* Elapsed Time  : 30.442 sec

* Converting CSV to -> zstd
* File Size     : 520.19 MB
* Elapsed Time  : 31.384 sec

* Converting CSV to -> gzip
* File Size     : 467.55 MB
* Elapsed Time  : 107.864 sec

* Converting CSV to -> brotli
* File Size     : 446.58 MB
* Elapsed Time  : 90.93 sec

NOTE : The File Sizes Are Approximated = (file bytes / 1048576)

 Finished !!
```

### PyArrow Read Tests Results

These results are using [Apache Arrow][] straight from the box. No Spark
engines are deplyed yet.

To say it's fast is an understatement.

> NOTE : check the CSV Read Time and Compare it to [Pandas][] from above.

```bash
Running Read Tests Using Apache Arrow
Compression Types : ['CSV', 'SNAPPY', 'ZSTD', 'GZIP', 'BROTLI']

* Reading file  : wsprspots-2020-02.csv
* File Size     : 3780.94 MB
* Elapsed Time  : 2.213

* Reading file  : wsprspots-2020-02.snappy
* File Size     : 667.07 MB
* Elapsed Time  : 2.031

* Reading file  : wsprspots-2020-02.zstd
* File Size     : 520.19 MB
* Elapsed Time  : 1.758

* Reading file  : wsprspots-2020-02.gzip
* File Size     : 467.55 MB
* Elapsed Time  : 3.603

* Reading file  : wsprspots-2020-02.brotli
* File Size     : 446.58 MB
* Elapsed Time  : 2.096

 Finished !!
```

# Whats Nest

The next phase it to run read and query tests with [Spark and Scala][] and 
PySPak DataSet queries via Python.


[PySpark]: https://databricks.com/glossary/pyspark
[wsprana]: https://github.com/KI7MT/wsprana-spark-python
[Apache Spark]: https://spark.apache.org/PySpark
[Anaconda Python]: https://www.anaconda.com/
[Python]: https://www.python.org
[Pandas]: https://pandas.pydata.org/
[Apache Parquet]: https://parquet.apache.org/
[wsprana repository]: https://github.com/KI7MT/wsprana-spark-python
[Spark and Scala]: https://github.com/KI7MT/wsprana-spark-scala