# SNP filtering JupyterLab Notebook

This repo contains a JupyterLab notebook allowing individual SNPs to be filtered from the UKB genotyping data.  A few approaches to filtering are provided, including options to filter by individual SNP rsIDs or by genomic regions of interest.



# How to run this notebook
Follow the steps below to run this Jupyter Notebook:

* Click on the Tools menu and select "JupiterLab"
* Click on the "New JupyterLab" button to start a JupiterLab instance.
* Select a name and a project from the dropdown meny for your JupiterLab environment.
* Select the priority for you JupyterLab environment; "Normal" of "High" is recommended.
* Under "Cluster Configuration", select Single Node.
* Set instance type and duration for you environment.If the chromosomes where SNPs of interest are known in advance and a small number of chromosomes files are selected for download, an instance type with such as mem1_hdd1_v2_x8 or mem1_hdd1_v2_x4 should be sufficient. If all chromosome files are selected for download, instance type with more computational resources may be needed (mem1_hdd1_v2_x16 or above).
* Click on "Start Environment"
* You will see your environment go from "Initialising" to "Launching" and then "Ready". This may take some time depending on the priority selected; at busy times, it may be necessary to select high priority to avoid long initialising times. Once the environment is ready, click on "Open".
* A JupyterLab session will open. On the left side of the screen, you will see a a "DNA Nexus" tab, allowing you to open notebooks directly from your project environment. If you have saved this notebook under you project environment, just double click to open it.
* Press "Ctrl" + "Enter" to run code cells. An hourglass icon on the JupireLab tab in your browser indicates that the code is running. Please note that depending on number of chromosomes and SNPs and your instance type, code may take some time to run.

