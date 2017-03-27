# Update cBioPortal seed database files 
To update the seed database files to a recent version you should follow these steps:

1. Start a new instance of the cBioPortal database with the previous seed database ([more information](https://github.com/cbioportal/datahub/blob/master/seedDB/README.md)).

2. Run the migration script from a branch that includes the new database schema ([more information](https://github.com/cBioPortal/cbioportal/blob/master/docs/Updating-your-cBioPortal-installation.md#running-the-migration-script)).

3. Move to the folder where you want to save the seed files. Use the following commands (assuming that the database is running on port 8306) to generate the new seed files. Please specify the new schema version in the file name (i.e. `v2.0.1`).
```shell
mysqldump -u cbio -pP@ssword1 -P 8306 --host 127.0.0.1 --ignore-table cbioportal.pdb_uniprot_alignment --ignore-table cbioportal.pdb_uniprot_residue_mapping --ignore-table cbioportal.info --no-create-info --complete-insert cbioportal > seed-cbioportal_hg19_v2.0.1.sql
mysqldump -u cbio -pP@ssword1 -P 8306 --host 127.0.0.1 --no-create-info cbioportal pdb_uniprot_alignment pdb_uniprot_residue_mapping --complete-insert > seed-cbioportal_hg19_v2.0.1_only-pdb.sql
```
:warning: The database schema is not included in these dump files.

4. Zip the generated mysql dump files:
```shell
gzip seed-cbioportal_hg19_v2.0.1.sql
gzip seed-cbioportal_hg19_v2.0.1_only-pdb.sql
```

5. New files are ready to be uploaded to datahub.

:warning: The database schema itself is found at: `$PORTAL_HOME/db-scripts/src/main/resources/db/cgds.sql`
