# Uniprot and `blastx` tutorial

In this tutorial, students will familiarize themselves with the [UniProt Swiss-Prot database](https://www.uniprot.org/uniprot/?query=reviewed:yes) and run the`blastx` program from the Terminal. Students should work from within the current Github repository.

1. Navigate to the [UniProt Swiss-Prot database](https://www.uniprot.org/uniprot/?query=reviewed:yes). Click on the "Columns" button to edit columns.
2. Add the following columns UniProtKB results and click "Save": 
	- Gene ontology IDs
	- Gene ontology (biological process)
	- Gene ontology (cellular component)
	- Gene ontology (molecular function)
3. Download the modified UniProtKB table as a tab-delimited file. This version will include additional GOterm columns and can be joined with `blastx` output. However, this file will not be compatible with `blastx` input requirements.
4. Download a `blastx`-compatible Uniprot database from [this link](ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_sprot.fasta.gz) using `curl`. Unzip the file using `gunzip *gz`.
5. Download the latest version of `blast` from [this link](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) and install on your machine.
6. Create a `blast` database. `{blastDirectory}` should be the specific path to the `blast` directory on your machine. If you do not know what the absolute path is, you can drag the `makeblastdb` program from the Finder window into the Terminal window. The Terminal will automatically produce the absolute path to this program. When running the commands below in the computer, do not include `\`. Those are included below solely for demonstration purposes.
	- Path to `makeblastdb`
	- Path to input file. The input file is the Uniprot database downloaded from the FTP link.
	- Database type desired. We are doing a blastx matching nucleotides to proteins, so we want a protein database.
	- Name of the database to be created. Always include the date the database was created in the file name.
	```
	{blastDirectory}makeblastdb \ #Path to makeblastdb
	-in uniprot_sprot.fasta \
	-dbtype prot \
	-out uniprot_sprot_database_DATE
	```
    After running `makeblastdb`, check what files were created using `ls`.

7. To run `blastx`, the following arguments are needed (note: you can generate a list of all arguments for the `blastx` program by running `blastx -h`):
	- Path to `blastx`
	- Path to query sequence. You can use the sequence downloaded in the [Github and Linux tutorial](https://github.com/eimd-2019/tutorials/blob/master/2019-07-05-Github-Linux-Tutorial.md)
	- Path to database created in step 6
    - Output file name. It is best practice to include the date the file was generated in the name.
    - Maximum e-value to use for hits. The lower the e-value, the better.
    - Number of CPUs to use. Optional argument when running `blastx` on a more powerful computer.
    - Output format 6 specifies tabular format
	```
    {blastDirectory}blastx \
    -query Colleen.fasta \
    -db uniprot_sprot_database_DATE \
    -out 2010-07-09-Colleen-uniprot-blastx.tab \
    -evalue 1E-10 \
    -num_threads 4 \
    -outfmt 6
    ```
    Once the `blastx` finishes running, check the output with `head`.
