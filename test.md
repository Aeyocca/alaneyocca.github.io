# dGCNA troubleshooting

This is a quick, in no way comprehensive guide to get the differential Gene Coexpression Network Analysis written by Henry Priest https://github.com/hdpriest/dGCNA

<img src="/Japan.png" alt="Japan">

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
DISCLAIMER: I am no expert in java programming, my next suggestions about how to get the java package up and running may be flawed and affect downstream analyses, but following what I propose here will successfully get you to the end of this troubleshooting guide.  
Inside the folder downloaded from the internet for each of the five packages, there should be a /lib/ directory. In there you should find the executable .jar file for the package. I chose to copy this jar file to the NetworkCalculator/src/ directory.  
Now you should have these five package .jar files in your src/ directory:  
<img src="/packages.png" alt="packages">  




