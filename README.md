# WSPR Analytics CSV Utilities

In the early days (March 2008), [WSPR Spots][] measured in the hundreds of thousands per month. Today,
that number has increased to over 46 Million at last count, and shows no sign of abatment.
By any reasonable definition, it is safe to say, [WSPR] has entered the realm of [Big Data][].

With this entry comes a unique set of challanges to draw meaningful results in a timely manner.
The `WSPR Analytics` project will contain a seris of documents, small modules, example
applications, code snippets and various utilities centerd around [Apache Spark][], [Apache Hadoop][],
[PySpark][], [PyArrow][], [Anaconda Python][], [Jupyter Notebooks][], [Scala][] and other [Big Data][] tooling to
help with this challange.

## Basic Tool Requirments

The original festures of this project performed basic file transformations with a few select
`R` script to render vvisualizations, this tool will be moved to it's on set of scripts and
packages.

>NOTE: During development, this package **is not** intended for pip installaiton.
> It should be checked out and run from source.

You must have Python, Java, PySpark/Spark available from the command line.

- Java openjdk version 1.8.0_275 or later
- Spark 3.0.1
- Python 3.7+
- PySpark from PyPi (optional)

An easy way (on Linux / MacOS) to mange Java, Spark, Scala and SBT is
through an management tool called [sdkman][]. This tool allows
one to install virtually any combination of tools you need without
affecting your root file system. With the exception of Python,
All the above requirements can be installed and managed via [sdkman][].

For Python, the recomendation is to use [Anaconda Python][], the full version,
as it provides all the analytics tooling you'll need for this project and more.

## Data Sources and Processing

The primary data source will be the monthly [WSPRNet Archives][]. At present, there is no plan to pull
nightly updates. That could change if a reasonble API is identified.

The WSPR CSV tools will be used to convert the raw CSV files into a format better suited for parallel processing,
namely, [Parquet][]. Read speeds, storage footprints, and ingestion improve dramativaly with this storage format.
However, there is a drawback, one cannot simply view a binary file as they can with raw text files. The
original CSV will remain in place, but all bulk processing will be pulled from [Parquet][].
During these transformations is where [PyArrow][] + [PySpark][] will earn it's keep.

A [PostgreSQL][] database server will be beeded. There are many ways to perform this installation (local, remote,
[Dockerize PostgreSQL][], [PostgreSQL with Vagrant][], etc). Whichever method you chose, it will be used extensively
by many of the apps and scripts.

[WSPR Spots]: http://www.wsprnet.org/drupal/wsprnet/activity
[WSPR]: https://www.physics.princeton.edu/pulsar/k1jt/wspr.html
[Big Data]: https://www.oracle.com/big-data/what-is-big-data.html
[Amazon AWS EBR]: https://aws.amazon.com/emr/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc
[Microsoft Cloud Analytics]: https://azure.microsoft.com/en-us/solutions/big-data/#products
[Google Smart Analytics]: https://cloud.google.com/solutions/smart-analytics/
[Apache Spark]: https://spark.apache.org/PySpark
[PySpark]: https://databricks.com/glossary/pyspark
[Anaconda Python]: https://www.anaconda.com/
[Scala]: https://docs.scala-lang.org
[Open Source Tools]: https://apache.org/index.html#projects-list
[AWS]: https://aws.amazon.com/
[Azure]: https://azure.microsoft.com/en-us/
[GCP]: https://cloud.google.com/
[Apache Hadoop]: http://hadoop.apache.org/
[Jupyter Notebooks]: https://jupyter.org/
[IntelliJ IDEA]: https://www.jetbrains.com/idea/
[Dockerize PostgreSQL]: https://docs.docker.com/engine/examples/postgresql_service/
[PostgreSQL]: https://www.postgresql.org/
[PostgreSQL with Vagrant]: https://wiki.postgresql.org/wiki/PostgreSQL_For_Development_With_Vagrant
[Parquet]: https://parquet.apache.org/
[Flask-Pandas-App]: https://github.com/the-akira/Flask-Pandas-App
[Full Stack Flask]: https://www.fullstackpython.com
[WSPRNet Archives]: http://www.wsprnet.org/drupal/downloads
[Anaconda Python]: https://www.anaconda.com/
[sdkman]: https://sdkman.io/
[PyArrow]: https://towardsdatascience.com/distributed-processing-with-pyarrow-powered-new-pandas-udfs-in-pyspark-3-0-8f1fe4c15208
