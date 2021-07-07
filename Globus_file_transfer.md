Get the data to Discovery using Globus

If you used option 1 above and your data are in your local computer, or you are getting a hard drive with your data from the sequencing facility, you will need to transfer your data files to the Discovery folder.

You will need: a Discovery account, a Globus account and an endpoint computer.

## Login to Discovery.

In Terminal, login to discovery:

`ssh tbittar@login.discovery.neu.edu`

then enter your password

## Login to Globus.

Open your browser and go to Globus.org, then login or authenticate:

tbittar

Password

> This will get you to “File Manager” in Globus. 

## Get your files into your Discovery folder using Globus.

In File Manager, top right corner, select the 2-panel icon. This is so you can open 2 collections (= folders), 1 to determine the origin folder and 1 to determine the destination folder.

On the first panel, in the box Collection search box, find northeastern#discovery (you might have to login/authenticate), then on the Path box type /~/ or select from you bookmarks northeastern#discovery /~/ (your home folder) – this is your **destination folder**.

On the second panel, in the search box, find your endpoint computer and on the Path box, go to the folder where your files are – this is the **origin folder**.

With the origin and destination folders open in each panel, drag and drop the files or folder that you want to transfer.

**Tip:** Files that need to be kept on backup (such as the original SRA and FASTQ files) should be stored in your home directory. When working on those files, it is best to use the scratch folder than the home folder on Discovery because you have more space there to work when you are creating a lot of large intermediate files. However, the scratch folder is not backed up, so transfer the output files or any other files you want to keep safe to the home directory on Discovery.

**Tip:** Look at “Activity” (left menu) or hit “refresh list” (on the panel corresponding to destination folder) to check progress of transfer.

**Now that all files are in the destination folder, you can close the origin panel.**

**Tip**: Bookmark your home and scratch folders to make it easier to find them in the future in Globus > Bookmarks list (left side panel).
