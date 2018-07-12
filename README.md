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

If you don't install the certificate yet click [here](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookStartingGrid) or [here-2](https://ca.cern.ch/ca/help/?kbid=024010)

 Then you can execute the query with: 
 
 `das_client --query="dataset=/DoubleMuon*/Run2017C-PromptReco-v3/MINIAOD" --format=plain`

### Exercise 5 - EDM (Event Data Model framework)

`edmFileUtil, edmDumpEventContent, edmProvDump, edmEventSize`

The overall collection of CMS software, referred to as [CMSSW](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookCMSSWFramework), is built around a Framework, an Event Data Model ([EDM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookCMSSWFramework#EdM)), and Services needed by the simulation, calibration and alignment, and reconstruction modules that process event data so that physicists can perform analysis. The primary goal of the Framework and EDM is to facilitate the development and deployment of reconstruction and analysis software. The CMS Event Data Model (EDM) is centered around the concept of an Event. An Event is a C++ object container for all RAW and reconstructed data related to a particular collision.To understand what is in a data file and more, several EDM utilities are available. In this exercise, one will use three of these EDM utilities. They will be very useful at CMSDAS and after. More about these EDM utilities can be found at [WorkBookEdmUtilities](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookEdmUtilities). These together with the [Github web interface for CMSSW](https://github.com/cms-sw/cmssw) and the [CMS LXR Cross Referencer](http://cmslxr.fnal.gov/source) are very useful to understand and write CMS code. 

#### edmFileUtil 

Use edmFileUtil to find the physical file name (PFN) corresponding to the logical file name (LFN) from a MiniAOD file.

`edmFileUtil -d /store/relval/CMSSW_9_3_0_pre5/RelValZMM_13/MINIAODSIM/93X_mc2017_realistic_v2-v1/00000/96FBB6F5-0E92-E711-841B-0025905B85C0.root`

#### edmDumpEventContent

Next we will use edmDumpEventContent to dump a summary of the products that are contained within the file we're interested. Use edmDumpEventContent to see what class names etc. to use in order to access the objects in the MiniAOD file. If you want to look at a specific object (say, slimmedMuons) then execute

`edmDumpEventContent --all --regex slimmedMuons root://cmsxrootd.fnal.gov//store/user/cmsdas/2018/pre_exercises/0EE14BA8-41BB-E611-AD2F-0CC47A4D760A.root`

The output of edmDumpEventContent has information divided into four variable width columns. The first column is the C++ class type of the data, the second is module label, the third is product instance label and the fourth is process name. More information is available at Identifying Data in the Event.

Run again using:

`edmDumpEventContent root://cmsxrootd.fnal.gov//store/user/cmsdas/2018/pre_exercises/0EE14BA8-41BB-E611-AD2F-0CC47A4D760A.root > EdmDumpEventContent.txt`

and answer:

- 0) How many modules produce products of type vector ? 

- 1) What are the names of three of the modules that produce products of type vector? 

#### edmProvDump 

To aid in understanding the full history of an analysis, the framework accumulates provenance for all data stored in the standard ROOT output files. Using the command edmProvDump one can print out all the tracked parameters used to create the data file. For example, one can see which modules were run and the CMSSW version used to make the MiniAOD file. In executing the command below it is important to follow the instructions carefully, otherwise a large number of warning messages may appear. The ROOT warning messages can be ignored. 

`edmProvDump root://cmsxrootd.fnal.gov//store/user/cmsdas/2018/pre_exercises/0EE14BA8-41BB-E611-AD2F-0CC47A4D760A.root > EdmProvDump.txt`

EdmProvDump.txt is a very large file of the order of 40000-60000 lines. Open and look at this file and locate Processing History.

- 2) Which version of CMSSW_?_?_? was used to produce the MiniAOD file? 

#### edmEventSize 

Finally we will execute edmEventSize to determine the size of different branches in the data file. Further details may be found here: [SWGuideEdmEventSize](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideEdmEventSize). edmEventSize isn't actually a 'Core' helper function (anyone can slap 'edm' on the front of a program in CMSSW). You can use edmFileUtil to get a PFN from an LFN (as shown above) so you could combine the call 

` edmEventSize -v \`edmFileUtil -d /store/user/cmsdas/2018/pre_exercises/0EE14BA8-41BB-E611-AD2F-0CC47A4D760A.root\` > EdmEventSize.txt `
