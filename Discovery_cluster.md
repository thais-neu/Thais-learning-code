Notes from jobs run on Northeastern's Discovery.


Globus - used as an interface to upload files and check that new files are being created. Can access my home dir and any folder inside it, and also the scratch folder.

## Discovery

### 1) Access

### Access: ways to access/log into the Discovery cluster (assuming you already have access granted by Research Compupting).

a) On your browser type ood.discovery.neu.edu - go to Clusters - Discovery Shell Access - enter PW

or 

b) Open your local terminal, type ssh tbittar@login.discovery.neu.edu - enter PW

When successfully logged in, you'll see something like [tbittar@ood \~] indicating you're in the home dir (\~). Next step, request resources.

### 2) Resources

### Resources: ways to request resources. 

a) type `srun -p debug -N1 --pty /bin/bash` this gives 20 min to work

or

b) `srun -p lotterhos -N 1 --pty /bin/bash` this gives 24h to work (only for users authorized to use the lotterhos partiotion)

When successful, you'll see a message saying "job ##### has been allocated resources" and base will change to [tbittar\@d3037 \~], where @3037 is the node being used.

### 3) Creating working environments (this is mainly copied from the Lotterhos Wiki page, with my notes added).

3.1) Install and update Bioconda: Install conda by typing one of the following options at a command prompt

a) curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh

or:

b) wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3.sh
cd ~; bash miniconda3.sh –b -y –p ~/miniconda3
The options -b -y will install miniconda3 in batch mode (no prompts) and the option -p ~/miniconda3 will install miniconda3 in that path.

3.2) Update the conda version by typing: `conda update conda`

3.3) Set up channels: after installing conda you will need to add the Bioconda channel as well as the other channels Bioconda depends on. It is important to add them in the following order so that the priority is set correctly. Type the following at the command prompt:

conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

To check on the steps above, look in your home dir (maybe using globus) and you should see a folder "Miniconda3" and a file "Miniconda3-latest-Linux-x86_64.sh". If no errors come up and you see this folder and file, it should have worked fine.

3.4) Create envs (environments) and install tools using the following commands. The example environment here is `lotterhos_utils`

Create a conda env to use packages inside lotterhos_utils by typing `conda create -n lotterhos_utils` **this did not work for me**

Instead, I had to dowload the lotterhos_utils.yml file. To do that, I did:

- go to the github page where the yml file is (https://github.com/northeastern-rc/lotterhos_group/tree/main/env_yml_files) and open the desired file 
- click 'raw' on top right then copy the path from the browser (https://raw.githubusercontent.com/northeastern-rc/lotterhos_group/main/env_yml_files/lotterhos_utils.yml?token=AMO6NTJVYDEMXUA3B2I3QQDA4NVEC)

- then open your local terminal, navigate to a Documents folder of your choice, and type `curl -O` plus paste the path to the raw file. Full command looks like:
https://raw.githubusercontent.com/northeastern-rc/lotterhos_group/main/env_yml_files/lotterhos_utils.yml?token=AMO6NTJVYDEMXUA3B2I3QQDA4NVEC

- then upload the file to your home dir (or a folder of your choice inside it) using Globus.

Check that the file inside your home dir is about the same size as the file in Github.

Steps 3.1, 3.2, 3.3 and 3.4 above (install, update, add channels, create) - you should only have to do this once (create once for each environment).

### 4) Activate the env: type `conda activate lotterhos_utils`
Install required tools in your activated env: conda install -y vcftools plink
Update the tools as required: conda update vcftools plink

### 5) type the desired command, in this example we will:

a) Transform the vcf format into a tped plink format

Step 1: vcftools --vcf yournameoffile.vcf --plink-tped --out yournameoffile 

Results: several warnings (ask Katie); "unrecognized value sused for CHROM: NC_035780.1 9to 789.1) - Replace with 0."; "writing PLINK TFAM file....Done" "After filtereing kept 2526535 out of a possible 2526535 sites; "run time = 675.00 seconds"

b) Then transform the plink format to a raw format by re-running the following command on your terminal.

Step 2: plink --tped yournameoffile.tped --tfam yournameoffile.tfam --recodeA --out yournameoffile
