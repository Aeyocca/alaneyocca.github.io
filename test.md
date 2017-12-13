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
<img src="/ll_networkCalcPackage.png" alt"ll_networkCalcPackage">
