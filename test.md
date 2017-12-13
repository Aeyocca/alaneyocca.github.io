# dGCNA troubleshooting

This is a quick, in no way comprehensive guide to get the differential Gene Coexpression Network Analysis written by Henry Priest https://github.com/hdpriest/dGCNA
  
## Downloading

Download the entire NetworkCalculator directory from https://github.com/hdpriest/dGCNA to your hpcc account.
I first downloaded it to my computer, then used the following commands to upload it to the hpcc:

`$ scp -r NetworkCalculator yoccaala@hpcc.msu.edu`

## Getting started

To get the java scripts to run, A few steps need to be taken:
#### 1.)

Navigate to the NetworkCalculator/src/networkCalcPackage directory, load java developers toolkit, then compile the .jar files.   
`$ cd NetworkCalculator/src/networkCalcPackage`  
`$ module load Java/jdk1.8.0`  
`$ javac *java`  

This should create a list of .class files for each .java file:  
<img src="/networkCalcPackage.png" alt="ll_networkCalcPackage">

#### 2.)

Download the dependencies. Five java packages are required to run these scripts. To install a java package onto the hpcc, simply upload the .jar file for the java package. Again, I did this by downloading first to my computer, unzipping it locally, then uploading to the decompressed folder to the hpcc.  
  
**DISCLAIMER: I am no expert in java programming, my next suggestions about how to get the java package up and running may be flawed and affect downstream analyses, but following what I propose here will successfully get you to the end of this troubleshooting guide.  
  
Inside the folder downloaded from the internet for each of the five packages, there should be a /lib/ directory. In there you should find the executable .jar file for the package. I chose to copy this jar file to the NetworkCalculator/src/ directory.  
Now you should have these five package .jar files in your src/ directory:  
<img src="/packages.png" alt="packages">  
Next, these .jar files need to be added to the environmental variable $CLASSPATH. This variable is used by the java interpreter to search for the files to be run. That terminology may not be entirely correct, but that is how I understand it:  
`$ export CLASSPATH=${CLASSPATH}:commons-lang3-3.6.jar`  
`$ export CLASSPATH=${CLASSPATH}:commons-math3-3.6.1.jar`  
`$ export CLASSPATH=${CLASSPATH}:commons-cli-1.4.jar`  
`$ export CLASSPATH=${CLASSPATH}:jcommon-1.0.23.jar`  
`$ export CLASSPATH=${CLASSPATH}:jfreechart-1.0.19.jar`  
*Remember to run these commands in the /src/ directory where these jar file are, otherwise, the java interpreter might not be able to find them*  
Adding ${CLASSPATH}: to the command allows you to append these jar files to the $CLASSPATH variable instead of just overwritting the current contents.  
  
In addition to these .jar files, you need to add the current directory (specified by a dot) to the $CLASSPATH variable so the java interpreter can identify all scripts found in the NetworkCalculator package:  
`$ export CLASSPATH=${CLASSPATH}:.`  
  
To check everything was added corrected, check it out:
  
<img src="/classpath.png" alt="classpath">  
  
Now you are ready to run the scripts!  
## dGCNA Construct
Again, I am not claiming to comprehensively understand this program. The only thing I can promise is this guide will help you to get this to run. Whether it has run correctly, I leave to you. I will simply share my experience, inputs, and outputs.  
  
Here is the help message from the NetworkCalculator package:  
<img src="/help_all.png" alt="help_all">  
  
This section will discuss the input and outputs from the construct command.  
  
#### 1.) Inputs  
Here is the help message for the compare function:  
<img src="/help_construct" alt="help_construct">  
  
###### -a -m
Admittedly, I have no idea what any of these parameters are or what they mean. The values I arbitrarily chose is shown below in the job sumbission script.  
###### -c <correlation>    
The options for this command I have seen are `-c pcc` (pearson's correlation coefficient), `-c spearman` (Spearman's rank coefficient), or `-c gini` (Gini coefficient).  
I use `-c pcc` as I am more familiar with that.  
###### -d  
The data file lists the geneIDs in the first column. Each additional column is a datapoint (in my case time) with an expression value in each cell. The following is an example with some additional information about the expression frames.  
*The construct command must be run for EACH treatment considered. Here, I was comparing CAM and C3 photsynthesis, so I had to run the compare command twice, once for CAM and once for C3 dataframes*  
  
<img src="/df_stats.png" alt="df_stats">  
  
This dataframe has: 44,488 lines, 13 columns, and is 5.3 Mb large.  
  
###### -M  
Mask values below a certain threshold.  
###### -o  
Specify the name of the output directory.  
###### -t  
Specify the number of computer threads to utilize. I try to get this value to be close to the number of processors requested in the submission script, leaving a little room in case another processor is needed for something.  

Here is an example submission script for constructing a gene coexpression network for the C3 dataframe:  
  
  
