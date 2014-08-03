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

1. Create the necessary tables using https://github.com/soluvas/sanad SQL schema migration tools.
2. Import data using `psql` and `COPY` command.

## How to Generate These Files

1. Prepare Hadith files from https://github.com/ceefour/hadith-islamware
2. Use `org.soluvas.sanad.cli.qurandatabase.ImportHadithDatabase` from https://github.com/soluvas/sanad project.
3. Dump from PostgreSQL to TSV files:

```bash
psql -hlocalhost -Upostgres sanad_sanad_dev
```

```sql
COPY (SELECT * FROM sanad.hadithcollection) TO '/tmp/hadithcollection.tsv';
COPY (SELECT * FROM sanad.hadith) TO '/tmp/hadith.tsv';
COPY (SELECT * FROM sanad.literal WHERE id LIKE 'hadith%') TO '/tmp/literal-hadith.tsv';
COPY (SELECT * FROM sanad.transliteration WHERE id LIKE 'hadith%') TO '/tmp/transliteration-hadith.tsv';
COPY (SELECT * FROM sanad.spellingproperty WHERE id LIKE 'hadith%') TO '/tmp/spellingproperty-hadith.tsv';
COPY (SELECT * FROM sanad.authenticityproperty WHERE id LIKE 'hadith%') TO '/tmp/authenticityproperty-hadith.tsv';
```

```bash
cp -v /tmp/hadith*.tsv /tmp/*-hadith.tsv ~/git/sanad-hadith/
xz -2e -v literal-hadith.tsv   # GitHub's file size limit is 100 MB
```
