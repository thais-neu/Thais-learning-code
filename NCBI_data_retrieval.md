Get the data from NCBI

You will need: Accession List and SRA toolkit package

## Get the accession list.

*Option 1.*

Go to ncbi.nlm.nih.gov/bioproject/

In the search bar (top of page) enter the accession number, e.g., PRJNA356786

In the Project Data table, click in the number of links e.g., 221

On top of the page, there is a box “View Results as an Expanded Interactive Table using the Run Selector” – click the link “Send Results to run Selector”.

*Option 2.*

Go to ncbi.nlm.nih.gov/Traces/study/?

Type the accession number on the accession search box and select ‘Runs’.

**Both options 1 and 2 will land at the SRA Run Selector page.**

Under “Found (221) Items” (orange ribbon), select the files you want (or select all, by clicking on the check mark - first column in Found 221 Items).

Under “Select” (blue ribbon), Click on Accession List for Total (if you want all files) or selected (if you want only the selected files under “Found Items”. 

> This will create and download the accession list file, a text file that contains a list of file names that correspond to the SRA files from NCBI that will be downloaded. Save this file in the location from which you are running the SRA Toolkit. You can also download the metadata corresponding to those files.

**Now you have the accession list, you will need to use the SRA toolkit package to download the files.**

## Get the SRA toolkit package.

*Option 1.*

Use your local computer, desktop or laptop.

Download and install the SRA Toolkit for your OS following instructions at: github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit

Make sure to install the latest release!

Make sure to use the correct release number and platform, e.g., in step 2 of the Mac OSX install, the correct command would be tar -vxzf sratoolkit.2.10.8.mac64.tar.gz (for the current release on July 2020 for Mac).

Configure SRA toolkit, following instructions at: github.com/ncbi/sra-tools/wiki/03.-Quick-Toolkit-Configuration

Test that the toolkit is functional, following instructions at: github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit

*Option 2.*

Use Discovery.

Login to discovery. SRA toolkit is an available module in the Lotterhos cluster.

*Here, I downloaded, installed and configured the SRA toolkit on my desktop and used it to download the SRA files to my desktop, then I uploaded the files to Discovery through Globus (see below). But the  SRA toolkit is available on Discovery so should be able to get it from NCBI directly to Discovery folder.*
