# Hendy's Internal Notes

## How to Generate DB Files from IslamWare dataset

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
COPY (SELECT * FROM sanad.spellingproperty WHERE id LIKE 'hadith%') TO '/tmp/spellingproperty-hadith.tsv';
COPY (SELECT * FROM sanad.authenticityproperty WHERE id LIKE 'hadith%') TO '/tmp/authenticityproperty-hadith.tsv';
```

```bash
cp -v /tmp/hadith*.tsv /tmp/*-hadith.tsv ~/git/sanad-hadith/
xz -2e -v literal-hadith.tsv   # GitHub's file size limit is 100 MB
```

## Other Hadith Datasets

1. [kutubuhadits-sql](https://bitbucket.org/soluvas/kutubuhadits-sql) (private) containing 1 Quran + 9 Hadits Compilation with Indonesian translation.
