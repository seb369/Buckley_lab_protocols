# Temporary directory full

## Old sequence analysis pipeline (screed step)

In the old sequence analysis pipeline, there is a step after merging your fastq files with PEAR that you create as screed database. This step uses a program called SQLite3 which needs to make a huge temporary file (>10GB). This usually goes in `/tmp` but since we updated the server OS, we have partitioned `/tmp` to have only space for ~12GB, some of which is in use by other programs, most notably RStudio. Because of this, you will get an error saying that the disk is full.

To fix this you need to change the directory that SQLite3 is using for its temporary directories to a temp directory in your home (ie `/home/sam/tmp`).

The easy way to do this is to add the following to your `.bashrc` file:
  `export SQLITE_TMPDIR=/home/USERNAME/tmp`

Remember to replace USERNAME with your username.

You might need to reinitialize your jupyter notebook after this too.

