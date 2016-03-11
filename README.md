sanad-hadith
============

Hadith SQL database dump for Sanad, collected from various sources including Islam Ware
Compiled by [Hendy Irawan](http://www.hendyirawan.com/).

Sources:

1. [Islam Ware](https://www.islamware.com/app/downloads)

Copyright (C) 2006-2014 Islam Ware

Hadith files signed by [Hendy Irawan](http://www.hendyirawan.com)
using Hendy Irawan <ceefour666@gmail.com> [key 5A9AC703](https://keyserver.pgp.com/vkd/DownloadKey.event?keyid=0xFEDB960B5A9AC703) 
are available at https://github.com/ceefour/hadith-islamware

## Usage

1. Install [PostgreSQL 9.5 or later](http://www.postgresql.org/).
2. Extract `literal-hadith.tsv.xz`. You can use [7-Zip](http://www.7-zip.org/) or [XZ Utils](http://tukaani.org/xz/).
3. Create the necessary tables using https://github.com/soluvas/sanad SQL schema migration tools.
    For PostgreSQL you can quickly use https://github.com/soluvas/sanad/blob/master/export/sanad.schema.sql

4. Import data using `psql` and `COPY` (PostgreSQL server's) or `\copy` (locally) command:

        \copy sanad.hadithcollection from 'hadithcollection.tsv' (format csv, delimiter E'\t', header false, escape E'\\', encoding 'UTF-8')
        \copy sanad.hadith from 'hadith.tsv' (format csv, delimiter E'\t', header false, escape E'\\', encoding 'UTF-8')
        \copy sanad.literal from 'literal-hadith.tsv' (format csv, delimiter E'\t', header false, escape E'\\', encoding 'UTF-8')
        \copy sanad.spellingproperty from 'spellingproperty-hadith.tsv' (format csv, delimiter E'\t', header false, escape E'\\', encoding 'UTF-8')
        \copy sanad.authenticityproperty from 'authenticityproperty-hadith.tsv' (format csv, delimiter E'\t', header false, escape E'\\', encoding 'UTF-8')
