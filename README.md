<!-- dx-header -->

# Extract SNPs from genetic data 

This repository provides tools for filtering individual SNPs from UK Biobank genotyping data using the UK Biobank Research Analysis Platform (UKB-RAP) on DNAnexus. It includes two methods: a DNAnexus applet and a Jupyter Notebook. Additional documentation is provided below.

# 1. DNAnexus Platform App

The **SNP_extract** folder includes the source code for an app that runs on the UK Biobank Research
Analysis Platform (UKB-RAP). For more information about how to run or
modify it, see <https://documentation.dnanexus.com/>. Documentation on
building applets can be found in the DNAnexus documentation at
<https://documentation.dnanexus.com/developer/apps/intro-to-building-apps>.

This app allows you to extract SNPs from the BED (PLINK) files in the UK
Biobank genetic data. The app accepts a list of variants/SNPs in two
formats: either a list of rs identifiers or a list of genomic regions to
search for variants within.

The app filters from the Genotype data, i.e. field
[22418](https://biobank.ndph.ox.ac.uk/showcase/field.cgi?id=22418). 
Please note that positions are in GRCh37 coordinates.

## Inputs

The app requires `SNP_list` as a mandatory input. This is a text/csv/tsv file that 
should be uploaded onto your project prior to running the app and can be in 1 of 2 formats: 


### 1. List of rsIDs 

A text/csv/tsv file containing as list of rsIDs corresponding to the SNPs of interest. 
The file should include a single column of data, with one rsID per line and no header, in the following format:

~~~~
rs28659788
rs116587930
rs116720794
rs3131972
rs12184325
rs313196
~~~~

### 2. List of genomic regions 

**N.B.**: Genotype calls positions are based on the GRCH37 coordinates, whereas the UK Biobank 
whole-genome sequencing (WGS) and whole-exome sequencing (WES) data use GRCH38 coordinates. 
Please make sure that the list of variant coordinates corresponds to the field id of interest.

A text/csv/tsv file containing four columns:
1. **chromosome** ( e.g. 1, 15, X), 
2. **region start** (in base pair coordinates)
3. **region end** (also in base pair coordinates) 
4. A user-selected **identifier** for the region. 
Each chromosome region of interest should be included on a separate line:

|     |          |          |     |
|-----|----------|----------|-----|
| 1   | 30000000 | 35000000 | R1  |
| 4   | 60000000 | 62000000 | R2  |
| X   | 10000000 | 20000000 | R3  |

### Uploading input files

Input files need to be uploaded into your project space in the RAP
before they can be used with the SNP extraction app. To upload a file,
follow the steps below:

1.  Navigate to your project and click on the “Add” button in the top
    left corner.
2.  Navigate to Upload Data in the Dropdown menu.
3.  Click on Select Files and navigate to the input file on your
    computer or use the Drag and Drop function. Once the correct file
    has been selected, click on “Upload".


## Building the app

The applet is built and run in the command line with the
[dx-toolkit](https://documentation.dnanexus.com/downloads#dnanexus-platform-sdk).
You can find more information on the [dx-toolkit command line
utilities](https://documentation.dnanexus.com/user/helpstrings-of-sdk-command-line-utilities)
and options available in the documentation.

1.  Clone this repo.
2.  Login to the DNAnexus platform with `dx login` and select the
    UKB-RAP project you want to work in with `dx select`.
3.  From the SNP_extract folder, enter `dx build`.
4.  Run the applet on the UKB-RAP with the command
    `dx run SNP_extract -iSNP_list=<snps_list.txt>`.
    -i is used to give inputs to the applet. \<snps_list.txt\> should be
    replaced with the text file listing the SNPs of interest.The cost to run this applet depends on how extensive the list
    of variants is and the field id provided. In general, the costs is
    less than 0.50£.

### Running the app interactively

Alternatively, you can run the app interactively after building it in
your project.

1.  Navigate to your project on the UKB-RAP
2.  Find the SNP_extract applet and click in the checkbox next to the
    app name. The "Run" button will appear in the top right corner of
    the webpage.
3.  Click "Run"
4.  On the "Run" screen, select Execution Output Folder. This is the
    folder where your results file will appear. You can also change the
    the priority and set spending limits. In general, extracting a small
    number of SNPs ( 10 or fewer) should take under 10 minutes with a
    Normal priority setting and should cost less than £0.20. The runtime
    and costs may increase if a large number of SNPs are extracted or if
    large genomic regions are specified in the input files.
5.  To specify the inputs, click on the Analysis Inputs 1 tab. Click on
    Select File and select the input file uploaded.
6.  Click on "Start Analysis".
7.  You can monitor app progression under the **MONITOR** tab.
8.  Once the run is complete, you will receive an email indicating the
    app has finished running. Your results file will appear in the
    selected output folder.

## Output file

The output file will be named <input_file_name>_SNP_results_22418.raw. 
EIDs (Column is FID) will be specified in the first column of the output 
and SNP genotypes in the subsequent columns, with headers indicating the 
Variant ID, as well as the counted allele (e.g. rs28659788_G). The values
 in the column refer to the allelic dosage for the counted 
 allele: e.g. 2 indicates an individual is homozygous for the counted allele, 
 1 indicates heterozygosity and 0 indicates homozygosity for the alternative allele. 
 Further information on the plink raw format can be found on the [Plink 1.9
webpage](https://www.cog-genomics.org/plink/1.9/formats#raw).

## Troubleshooting

Error messages in the app are most likely to result from incorrectly
formatted input files or from attempts to run the app from projects
which have no access to the genetic data. Please ensure you have access
to the genetic data in plink format (located in the Bulk folder) before
using the app. If the app is terminated due to a runtime error, you will
receive an email with an error code.

# 2. Jupyter Notebook

A JupyterLab notebook is included for filtering SNPs from UKB genotyping data via UKB-RAP on DNAnexus. You can find the notebook in the **SNP_extract_notebook** folder. 
A few approaches to filtering are provided, including options to filter by individual SNP rsIDs or by genomic regions of interest.

# How to run this notebook
Follow the steps below to run this Jupyter Notebook:

* Click on the Tools menu and select "JupyterLab"
* Click on the "New JupyterLab" button to start a JupyterLab instance.
* Select a name and a project from the dropdown meny for your JupyterLab environment.
* Select the priority for you JupyterLab environment; "Normal" of "High" is recommended.
* Under "Cluster Configuration", select Single Node.
* Set instance type and duration for you environment.If the chromosomes where SNPs of interest are known in advance and a small number of chromosomes files are selected for download, an instance type with such as mem1_hdd1_v2_x8 or mem1_hdd1_v2_x4 should be sufficient. If all chromosome files are selected for download, instance type with more computational resources may be needed (mem1_hdd1_v2_x16 or above).
* Click on "Start Environment"
* You will see your environment go from "Initialising" to "Launching" and then "Ready". This may take some time depending on the priority selected; at busy times, it may be necessary to select high priority to avoid long initialising times. Once the environment is ready, click on "Open".
* A JupyterLab session will open. On the left side of the screen, you will see a a "DNA Nexus" tab, allowing you to open notebooks directly from your project environment. If you have saved this notebook under you project environment, just double click to open it.
* Install plink using the simple instructions at the top of the notebook.
* Press "Ctrl" + "Enter" to run code cells. An hourglass icon on the JupyterLab tab in your browser indicates that the code is running. Please note that depending on number of chromosomes and SNPs and your instance type, code may take some time to run.




