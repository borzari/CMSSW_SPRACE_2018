# CMSSW Pre-Exercises

CMSSW is the CMS SoftWare framework used in our collaboration to process and analyze data. In order to use it, you need to set up your environment and set up a local CMSSW release. We will start with the CMSSW pre-exercices, we have six sets of exercises. The fifth set we did at the first before (GitHub config.), now we start with the first set of exercises and follow the CMSDAS.

## First Set

### Exercise 1 - Cut and Paste 

Enter in the SPRACE Cluster:

`ssh -XY user@access.sprace.org.br`

Copy the python files in the folder:

`/home/denerslemos/public/CMSDAS-pre/`

Once copied, change the permission using:

`chmod +x *.py`

and than run:

`./runThisCommand.py`

- 0) What is wrong?

Run again using:

`./runThisCommand.py "asdf;klasdjf;kakjsdf;akjf;aksdljf;a" "sldjfqewradsfafaw4efaefawefzdxffasdfw4ffawefawe4fawasdffadsfef"`

- 1) Post the alphanumeric string of characters unique to your username.


### Exercise 2 - Simple Edit Exercise 

Run the code

`./editThisCommand.py`

- 0) Which error did you find?

Change the code and run again.

- 1) Paste the line beginning with "success" into the form provided.  


### Exercise 3 - Setup a CMSSW release

You will first want to set up the proper environment by entering the following command.

`source /cvmfs/cms.cern.ch/cmsset_default.sh`

Actually you should edit your ~/.bash_profile or ~/.bashrc, create it if you do not have one, to include the above command so that you do not have to execute each time you log into the cluster.

We will use the realease CMSSW_9_3_2. Let's setup that

First we set the structure:

`export SCRAM_ARCH=slc6_amd64_gcc630`
This also can be included in the ~/.bash_profile or ~/.bashrc, the slc6 meanning that you set a machine with scientific linux 6 with c++ (gcc) 630.

You can find out the existing releases installed on the local user interface by typing

`scram list -a`

or you can set first the SCRAM_ARCH and see which realease are avaiable using

`scram list CMSSW`


