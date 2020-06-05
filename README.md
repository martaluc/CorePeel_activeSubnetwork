# CorePeel_activeSubnetwork
This repository was made with the intent to get reproducible the results of  “Finding disease modules for cancer and COVID-19 in gene co-expression networks with the Core&Peel method”.
 
This repository contains:

• the complete tables of the enrichment analysis performed for the three COVID-19 datasets.

• the input files to get the active subnetworks (see below for much details). For each case study there are three files:
	
1)  Core&Peel.txt = output of Core&Peel algorithm available here: http://bioalgo.iit.cnr.it/index.php?pg=ppin. Remember to convert the node numbers to gene symbols. 

2) genes_rna_network.txt = list of genes included in the network and in the expression matrix.

3) DEGs.txt = list of differentially expressed genes.

In Asthma and Rheumatoid_arthritis folders, the Core&Peel.txt file corresponds to Core&Peel-r1-nl10-d0.5-f1-j0.8. Instead in Prostate_cancer and Colorectal_cancer folders, Core&Peel.txt corresponds to Core&Peel-r1-nl10-d0.7-f1-j0.8. For COVID-19 data, the user can decide which configurations of Core&Peel want to use, since they both were used in the article.

N.B. The names of the input files must not be changed.


## Docker Image

The active subnetwork detection algorithm based on the Core&Peel method is available as Docker Image.

The image can be obtained from Docker Hub: https://hub.docker.com/repository/docker/ma10r02t90a/corepeel_active-subnet/general


#### Instructions:

1) move to your working directory.

2) create the directory “data” on your working directory.

3) copy in "data" the three input files (not rename the files).

4) pull the Docker image:

          docker pull ma10r02t90a/corepeel_active-subnet:latest

5) running the Docker image:
	
- default p-value = 0.01:
		
	  docker run -v path/data:/data ma10r02t90a/corepeel_active-subnet

- different p-value can be added at end of the command:

           docker run -v path/data:/data ma10r02t90a/corepeel_active-subnet 0.05

Notes:

• docker run is the main command to run the command in the container.

•  -v says what follows is to be the volume. Write the absolute path of the directory /data.
A volume is a directory that lives on the host file system. A container is capable of reading/saving data within the volume. 
In this case the directory /data created in your working directory is the volume where the output files will be saved.
The output files are three:
	
	1)  DEGs_enrich.txt includes the p-value for each module.
	
	2) MultipleModules.txt contains all the significant modules according to the p-value threshold (defaulf 0.01).
	
	3) SingleModule.txt includes all the genes of the active subnetwork after merging all the significant modules.

• ma10r02t90a/corepeel_active-subnet is the image to be used for the container.
