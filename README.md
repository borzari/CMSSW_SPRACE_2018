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

This also can be included in the ~/.bash_profile or ~/.bashrc, the slc6 meanning that you set a machine with scientific linux 6 with gcc structure 630.

You can find out the existing releases installed on the local user interface by typing

`scram list -a CMSSW`

or you can set first the SCRAM_ARCH and see which realease are avaiable. How choose the CMSSW version you can see [here](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookWhichRelease#CmsswReleases)

After setted the structure we can cal the CMSSW realease using:

`cmsrel CMSSW_9_3_2`

Now go to `CMSSW_9_3_2/src/` and use

`cmsenv`

`git cms-init`

This last command will take some time to execute and will produce some long output, be patient. 

After that you are ready to go! 

To finish uses the command

`echo $CMSSW_BASE`

- 0) Paste the result of executing the above command in the form.


### Exercise 4 - Find data in the DAS ( Data Aggregation Service) 

In this exercise we will locate the MC dataset RelValZMM (Z -> μμ) and the collision dataset /DoubleMuon/Run2017C-PromptReco-v3/MINIAOD using the Data Aggregation Service.

Go to the url [DAS](https://cmsweb.cern.ch/das/). Need the certificate in your browser.

Search for:

`dataset release=CMSSW_9_3_0_pre5 dataset=/RelValZMM*/*CMSSW_9_3_0*/MINIAOD*`

This will search for datasets, processed with release CMSSW_9_3_0_pre5, which is named like /RelValZMM*/\*CMSSW_9_3_0\*/MINIAOD*. The syntax for searches is found [here](https://cmsweb.cern.ch/das/faq), with many useful common search patterns under "CMS Queries".

Look for /RelValZMM_13/CMSSW_9_3_0_pre5-93X_mc2017_realistic_v2-v1/MINIAODSIM and answer:

- 0) What is the size of this dataset? 

- 1) Click on "Sites" to get a list of sites hosting this data. Is this data at FNAL? Is this data at DESY? 

Back in the main dataset page, click on the link "Files" to get a list of the root files in our selected dataset. One of the files it contains should look like this: 

`/store/relval/CMSSW_9_3_0_pre5/RelValZMM_13/MINIAODSIM/93X_mc2017_realistic_v2-v1/00000/96FBB6F5-0E92-E711-841B-0025905B85C0.root`

If you want to know the name of the dataset from the name of a file, one can go to [DAS](https://cmsweb.cern.ch/das/) and type

`dataset file=/store/relval/CMSSW_9_3_0_pre5/RelValZMM_13/MINIAODSIM/93X_mc2017_realistic_v2-v1/00000/96FBB6F5-0E92-E711-841B-0025905B85C0.root`

Now we will locate a collisions dataset skim using the keyword search which is sometimes more convenient if you know the dataset you are looking for. In [DAS](https://cmsweb.cern.ch/das/) type:

`dataset=/DoubleMu*/*Run2017C*/MINIAOD*`

- 2) What release was the dataset containing 12Sep2017 collected in?

Having set your CMSSW environment one can also search for the dataset `/DoubleMuon/Run2017C-PromptReco-v3/MINIAOD` by invoking the DAS command in your WORKING DIRECTORY. The DAS commands das_client and dasgoclient are in the path for CMSSW_9 versions and above, so you do not need to download anything additional.

First, set your certificate

`voms-proxy-init --voms cms`

 Then you can execute the query with: 
 
 `das_client.py --query="dataset=/DoubleMuon*/Run2017C-PromptReco-v3/MINIAOD" --format=plain`
