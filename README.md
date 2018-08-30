# CMSSW Pre-Exercises

CMSSW is the CMS SoftWare framework used in our collaboration to process and analyze data. In order to use it, you need to set up your environment and set up a local CMSSW release. We will start with the CMSSW pre-exercices, we have six sets of exercises. The fifth set we did at the first before (GitHub config.), now we start with the first set of exercises and follow the CMSDAS.

## First Set

### Exercise 1 - Cut and Paste 

Login in the SPRACE Cluster:

`ssh -XY user@access.sprace.org.br`

Copy the python files in the folder:

`/home/denerslemos/public/CMSDAS-pre/Set1/`

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

`edmEventSize -v ``edmFileUtil -d root://cmsxrootd.fnal.gov//store/user/cmsdas/2018/pre_exercises/0EE14BA8-41BB-E611-AD2F-0CC47A4D760A.root`` > EdmEventSize.txt`

NOTE: Use only one apostrophe (between -v and edmFileUtil e the same between ...root and EdmEventSize.txt).

- 3) What is the number of events?

Open and look at file EdmEventSize.txt and locate the line containing the text `patJets_slimmedJetsPuppi__RECO`. There are two numbers following this text that measure the plain and the compressed size of this branch. 

- 4) What are these two numbers? 


### Exercise 6 - MiniAOD

Analyzing physics data at CMS is a very complicated task involving multiple steps, sharing of expertise, cross checks, and comparing different analysis. To maximize physics productivity, CMS developed a new high-level data tier MiniAOD in Spring 2014 to serve the needs of the mainstream physics analyses while keeping a small event size (30-50 kb/event), with easy access to the algorithms developed by Physics Objects Groups (POGs) in the framework of the CMSSW offline software. The production of MiniAODs will be done centrally for common samples. Its goal is to centralize the production of PAT tuple which were used among the Physics Analysis Groups (PAGs) in Run 1. (Information about PAT can be found in [SWGuidePAT](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuidePAT) and in a [CMS conference note](http://cdsweb.cern.ch/record/1196152).) MiniAOD samples will be used in the Run 2 analysis. Hence it is important to know about this tool. More information about MiniAOD can be found in [WorkBookMiniAOD](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookMiniAOD). 

The main contents of the MiniAOD are: 

- High level physics objects (leptons, photons, jets, E<sub>T</sub><sup>miss</sup>), with detailed information in order to allow e.g. retuning of identification criteria, saved using [PAT dataformats](https://twiki.cern.ch/twiki/bin/view/CMS/WorkBookPATDataFormats). Some pre=selection requirements are applied on the objects, and objects failing these requirements are either not stored or stored only with a more limited set of information.
Some high level corrections are applied: L1+L2+L3(+residual) corrections to jets, type1 corrections to E<sub>T</sub><sup>miss</sup>. 

- The full list of particles reconstructed by the ParticleFlow, though only storing the most basic quantities for each object (4-vector, impact parameter, pdg id, some quality flags), and with reduced numerical precision; these are useful to recompute isolation, or to perform jet substructure studies.
For charged particles with p<sub>T</sub> > 0.9 GeV, more information about the associated track is saved, including the covariance matrix, so that they can be used for b-tagging purposes. 

- MC Truth information: a subset of the genParticles enough to describe the hard scattering process, jet flavour information, and final state leptons and photons; GenJets with p<sub>T</sub> > 8 GeV are also stored, and so are the other mc summary information (e.g event weight, LHE header, PDF, PU information).
In addition, all the stable [genParticles](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookGenParticleCandidate) with mc status code 1 are also saved, to allow reclustering of GenJets with different algorithms and substructure studies. 

- Trigger information: MiniAOD contains the trigger bits associated to all paths, and all the trigger objects that have contributed to firing at least one filter within the trigger. In addition, we store all objects reconstructed at L1 and the L1 global trigger summary, and the prescale values of all the triggers. 

Please note that the files used in the following are from older releases, but they still illustrate the points they intended to.

The Z to dimoun MC file `root://cmseos.fnal.gov//store/user/cmsdas/2018/pre_exercises/CMSDataAnaSch_MiniAODZMM730pre1.root` is made in `CMSSW_7_3_0_pre1` release and the datafile `root://cmseos.fnal.gov//store/user/cmsdas/2018/pre_exercises/CMSDataAnaSch_Data_706_MiniAOD.root` made from the collisions dataskim `/DoubleMu/CMSSW_7_0_6-GR_70_V2_AN1_RelVal_zMu2011A-v1/MINIAOD`.

In your working directory, try to open the MC root file `root://cmseos.fnal.gov//store/user/cmsdas/2018/pre_exercises/CMSDataAnaSch_MiniAODZMM730pre1.root`.To do that we will use the [ROOT framework](https://root.cern.ch/).

`root -l`

`gSystem->Load("libFWCoreFWLite.so");`

`FWLiteEnabler::enable();`

`gSystem->Load("libDataFormatsFWLite.so");`

`gROOT->SetStyle ("Plain");`

`gStyle->SetOptStat(111111);`

`TFile *theFile = TFile::Open("root://cmseos.fnal.gov//store/user/cmsdas/2018/pre_exercises/CMSDataAnaSch_MiniAODZMM730pre1.root");`

`TBrowser b;`

TBrowser is a graphical browser. It runs on the computer, where you started ROOT. Its graphical interface needs to be forwarded to your computer. This can be very slow. You either need a lot of patience, a good connection or you can try to run ROOT locally, copying the root files that are to be inspected.

In TBrowser open the root file and go to:

`Events -> patMuons_slimmedMuons__PAT -> patMuons_slimmedMuons__PAT.obj -> pt()`

To quit the TBrowser use `.q`.

- 0) What is the mean value of the muon pt() for the MC data? 

Do the same for the datafile (/home/denerslemos/public/CMSDAS-pre/Set1/MiniAOD_data.root) and answer:

- 1) What is the mean value of the muon pt() for the collision data? 

End of the First Set.


## Second Set

### Exercise 7 - Slim MiniAOD sample from Exercise 6 to reduce its size by keeping only Muon and Electron branches 

In order to reduce the size of the MiniAOD we would like to keep only the slimmedMuons and slimmedElectrons objects and drop all others. Copy the configuration (python) files in `/home/denerslemos/public/CMSDAS-pre/Set2/`.  To work with this config. files and make the slim MiniAOD, execute the following steps in the directory CMSSW_9_3_2/src/

Now run the commands:

`cmsRun slimMiniAOD_MC_MuEle_cfg.py`

This produces an output file called slimMiniAOD_MC_MuEle.root

`cmsRun slimMiniAOD_data_MuEle_cfg.py`

This produces an output file called slimMiniAOD_data_MuEle.root

You can use the EDM tools to extract some information. Also you can open this files using TBrowser.

- 0) What is the size of the MiniAOD slimMiniAOD_MC_MuEle.root? 

- 1) What is the size of the MiniAOD slimMiniAOD_data_MuEle.root? 

- 2) What is the mean eta of the muons for MC? 

- 3) What is the mean eta of the muons for data? 

- 4) What is the size of the output file compared to the original sample?

- 5) Is the mean eta for muons for MC and data the same as in the original sample in Exercise 6? 

### Exercise 8 - Use FWLite on the MiniAOD created in Exercise 7 and make a Z Peak (applying pt and eta cuts)

FWLite (pronounced "framework-light") is basically a ROOT session with CMS data format libraries loaded. CMS uses ROOT to persistify data objects. CMS data formats are thus "ROOT-aware"; that is, once the shared libraries containing the ROOT-friendly description of CMS data formats are loaded into a ROOT session, these objects can be accessed and used directly from within ROOT like any other ROOT class! 

 In this exercise we will make a ZPeak using our data and MC sample. We will use the corresponding slim MiniAOD created in Exercise 7. To read more about FWLite, have a look at Section 3.5 of Chapter 3 of the [WorkBook](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBook). We will first make a ZPeak. We will loop over the slimmedMuons in the MiniAOD and get the mass of oppositely charged muons. These are filled in a histogram that is written to an output ROOT file. 
 
 Make sure that you get github setup properly as in obtain a GitHub account and key.
 
 To check out the package, run: 
 
 `git cms-addpkg PhysicsTools/FWLite`
 
 Then to compile the packages, do 
 
`scram b -j 8`

`cmsenv`

To make a Z peak, we will use the FWLite executable called FWLiteHistograms. The corresponding code should be in $CMSSW_BASE/src/PhysicsTools/FWLite/bin/FWLiteHistograms.cc

To make a ZPeak from this executable, using the MC MiniAOD, run the following command:

`FWLiteHistograms inputFiles=slimMiniAOD_MC_MuEle.root outputFile=ZPeak_MC.root maxEvents=-1 outputEvery=100`


This will not work. This error occurs because your input files slimMiniAOD_MC_MuEle.root is a MiniAOD and does not contain reco::Muon whose label is muons. It contains, however, slimmedMuons (check yourself by opening the root file with ROOT browser).

To solve that, go to FWLiteHistograms.cc and change:

`using reco::Muon -> using pat::Muon`

and 

`event.getByLabel(std::string("muons"), muons); -> event.getByLabel(std::string("slimmedMuons"), muons);`

Now you need to re-compile and run again.

You can see that now it runs successfully and you get a ROOT file with a histogram called ZPeak_MC.root. Open this ROOT file and see the Z mass peak histogram called mumuMass.

- 0) What is mean mass of the ZPeak for your MC MiniAOD? 

- 1) How can you increase statistics in your ZPeak histogram? 

If you look at the code FWLiteHistograms.cc, it also contains the defaults corresponding to the above command line options. Answer the following question: 

- 2) What is the default name of the output file? 

### Exercise 9 - Re-run the above executable with the data MiniAOD

After that, re-run for the data file:

`FWLiteHistograms inputFiles=slimMiniAOD_data_MuEle.root outputFile=ZPeak_data.root maxEvents=-1 outputEvery=100`

and answer:

- 0) What is mean mass of the ZPeak for your data MiniAOD? 

- 1) How can you increase statistics in your ZPeak histogram? 

#### Exercise 10 and 11 - Fireworks - CMS Event Display 

First copy the python file in `/home/denerslemos/public/` in your $CMSSW_BASE/src and run:

`cmsRun copy_CMSDAS_cfg.py`

This will copy 100 events to a file called DYJetsToLL_n100.root. To also copy the data file, open copy_CMSDAS_cfg.py and replace DYJetsToLL with DoubleMuon everywhere, there should be two occurrences of DYJetsToLL and run again.

After that copy both root files inyour local machine using scp.

Download the event display in your local machine:

Linux

`wget http://cern.ch/cmsshow/cmsShow-9.4-1.linux.tar.gz`

Mac

`wget http://cern.ch/cmsshow/cmsShow-9.2.mac.tar.gz`

Unzip

Linux

`tar xzf  cmsShow-9.4-1.linux.tar.gz`

Mac

`gunzip -c foo.tar.gz | tar xopf -`

and than run with your both root files, using:

`./cmsShow --no-version-check file.root`

and answer:

- 0) What is pT of the highest pT muon that you see in the first event? 

- 1) What is Run number? 

- 2) What is the LS number? 

- 3) How many tracks does the first event have? 

- 4) How many primary vertices are in the first event of DoubleMuon_n100.root? 

End of the Second Set.

## Third Set

#### Exercise 12 - Verify your grid certificate is OK

This exercise depends on obtaining a grid certificate and VOMS membership, but does not depend on any previous exercises. 

`voms-proxy-init -voms cms`

`voms-proxy-info -all | grep -Ei "role|subject"`

- 0) Copy the output.

#### Exercise 13 - Setup CRAB

##### CRAB Introduction 

In this exercise, you will learn an important tool [CRAB](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideCrab), which is used in all the data analysis at CMS. CRAB is a utility to submit CMSSW jobs to distributed computing resources. By using CRAB you will be able to access CMS data and Monte-Carlo which are distributed to CMS aligned centres worldwide and exploit the CPU and storage resources at CMS aligned centres.

HELP or QUESTIONS about CRAB3: Follow the [FAQ](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideCrab#Getting_support) to get help with CRAB3. 

The most recent CRAB3 tutorial which is always in the [WorkBook](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBook) under [WorkBookCRABTutorial](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookCRAB3Tutorial). This tutorial provides complete instructions for beginner and expert user to use CRAB3 in their studies. We strongly recommend you to learn the CRAB3 tutorial after you finish these exercises.In this exercise, you will use CRAB3 to generate a MC sample yourself and publish it to the [DBS](https://twiki.cern.ch/twiki/bin/view/CMS/DBS-TDR?redirectedfrom=CMS.DBS). 

##### Setup CRAB

Go to

`CMSSW_9_3_2/src`

`cmsenv`

Setup CRAB:

`source /cvmfs/cms.cern.ch/crab3/crab.sh`

see the CRAB version:

`which crab`

or 

`crab --version`

 - 0) Which CRAB version are you using?

Give the following command

`crab checkwrite --site=T2_BR_SPRACE`

 - 1) What is name of your directory name in store?
 
 #### Exercise 14 - Generate a QCD dataset with CRAB
 
 ##### CMSSW configuration file to generate MC events
 
 In this section we provide an example of a CMSSW parameter-set configuration file to generate minimum bias events with the Pythia MC generator. We call it CMSDAS_MC_generation.py. Using CRAB to generate MC events requires some special settings in the CRAB configuration file, as we will show later. 
 
 We use the [cmsDriver](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideCmsDriver) tool to generate our configuration file (in your folder CMSSW_9_3_2/src/): 
 
 `cmsDriver.py MinBias_13TeV_pythia8_TuneCUETP8M1_cfi  --conditions auto:run2_mc -n 10 --era Run2_2016 --eventcontent FEVTDEBUG --relval 100000,300 -s GEN,SIM --datatier GEN-SIM --beamspot Realistic50ns13TeVCollision --fileout file:step1.root --no_exec --python_filename CMSDAS_MC_generation.py`
 
 Feel free to browse the newly outputted `CMSDAS_MC_generation.py`.
 
  ##### Generating MC events locally
  
  Use:
  
  `cmsRun CMSDAS_MC_generation.py &> out.txt &`
  
 - 0) What is the file size of step1.root? 
 
 
  ##### Generate MC dataset using CRAB
  
  CRAB is handled by a configuration file. In CRAB3, the configuration file is in Python language. Here we give an example CRAB configuration file to run the `CMSDAS_MC_generation.py` MC event generation code. We name it `crabConfig_MC_generation.py` (`/home/denerslemos/public/CMSDAS-pre/Set3/`). Copy and paste this file in your CMSSW folder.
  
   All available CRAB configuration parameters are defined at [CRAB3Configuration](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookCRAB3Tutorial#CRAB_configuration_file).

Now let us try to submit this job via crab by 

`crab submit -c crabConfig_MC_generation.py`

For the detail of the crab command, you can find them from [CRAB3Commands](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookCRAB3Tutorial#CRAB_commands).

Now you might notice a directory called crab_projects is created under CMSSW_9_3_2/src/. See what is under that directory. After you submitted the job successfully, you can check the status of a task by executing the following CRAB command: 

`crab status crab_projects/crab_CMSDAS_MC_generation_test0`

 - 1) Where do you save the results?
 
 #### Exercise 15 - Running on dataset with CRAB

Do the same using data. Copy the file `crabConfig_data_slimMiniAOD.py` (`/home/denerslemos/public/CMSDAS-pre/Set3/`) and run:

`crab submit -c crabConfig_data_slimMiniAOD.py`

Now you can take a break and have some fun. Come back after couple hours and check the status again. 

When each of the sets of jobs is complete, all the output is staged, etc., run crab status and crab report one final time: 

`crab status`

`crab report`

 - 2) How many events were analyzed? 
 
 #### Exercise 16 - View the reconstructed Z peak in the combined data
 
Use the FWLiteHistograms executable you were using in the previous exercises to aggregate the data from all the CRAB output files. Download the files in the Access machine using [srm](https://github.com/denerslemos/CMSSW_SPRACE_2018/blob/Linux_SSH_Git/README.md). And view the reconstructed Z peak in the combined data using:

`FWLiteHistograms inputFiles=File1.root, File2.root, File3.root, File4.root outputFile=ZPeak_data.root maxEvents=-1 outputEvery=100`

## Fourth Set

In this set of exercises, we will analyze the MiniAOD file that was made in Third Set of Exercise. You must have this skimmed MiniAOD stored locally (at your Tier-2) in order to access them. We will use different options of analyzing the MiniAOD, namely, EDAnalyzer, FWLite executable, FWLite Macro and FWLite PyROOT. We will basically re-make the Zpeak and few other histograms and store them in an output root file. In the exercise in the end we will try to fit with a Gaussian, Breit-Wigner function etc. 


 #### Exercise 17 - Analyzing MiniAOD with an EDAnalyzer
 
 In this exercise we will analyze the MiniAODs created in Third Set of Exercise using an EDAnalyzer. In these MiniAODs, if you recall, we saved only the Muons and Electrons. So do not look for Jets or Photons or other objects as they were simply not saved. We will use a python config file and an EDAnalyzer ( a .cc file) to make a Z mass peak. 
 
 First we will add the PhysicsTools/PatExamples package as follows to YOURWORKINGAREA/CMSSW_9_3_2/src. The PatExamples package has lot of examples for a user to try. However, we will add our own code and config file to it and then compile. To add this package, do this (in your `$CMSSW_BASE/src/`):
 
`git cms-addpkg PhysicsTools/PatExamples`

 The python config file `analyzePatBasics_cfg.py` should be in PhysicsTools/PatExamples/test/ directory. The EDAnalyzer named `PatBasicAnalyzer.cc` should be in your PhysicsTools/PatExamples/plugins/ directory.
 
 
 First cut and paste the following two files (both in `/home/denerslemos/public/CMSDAS-pre/Set4/`. Save MyZPeakAnalyzer.cc in PhysicsTools/PatExamples/src/ and MyZPeak_cfg.py in CMSSW_9_3_2/src/. 
 
 Now, go back to `src/` and compile
 
 `scram b -j 8`
 
 After successful compilation, you must run the config file as follows: 
 
 `cmsRun MyZPeak_cfg.py`
 
 - 0) What is the number of entries in the mumuMass plot ?
 
 - 1) What is the mean mass in the mumuMass plot ?
 
 - 2) What is the mean pT, eta and phi for muons?
 
 - 3) What is the mean pT, eta and phi for electrons?

 Re-run using your crab results and answer: 
 
 - 4) What is the number of entries in the mumuMass plot using data sample?
 
 - 5) What is the mass in the mumuMass plot using data sample ?
 
 - 6) What is the mean pT, eta and phi for muons using data sample ?
 
 - 7) What is the mean pT, eta and phi for electrons using data sample ?
 
 - 8) What is the number of entries in the mumuMass plot using MC sample?
 
 - 9) What is the mass in the mumuMass plot using MC sample ?
 
 - 10) What is the mean pT, eta and phi for muons using MC sample ?

 - 11) What is the mean pT, eta and phi for electrons using MC sample ?
 
 #### Exercise 18 - Analyzing MiniAOD with an FWLite executable 

In this exercise we will make the same ROOT file `myZPeak.root` as in Exercise 17, but we call it `myZPeak_fwlite.root` so that you do not end of overwriting the file previously made in Exercise 17.

First make sure you have checked the following two packages: 

`git cms-addpkg PhysicsTools/FWLite`

`git cms-addpkg PhysicsTools/UtilAlgos`

Cut and paste the following two files (both in `/home/denerslemos/public/CMSDAS-pre/Set4/`). Replace the $CMSSW_BASE/src/PhysicsTools/FWLite/bin/FWLiteWithPythonConfig.cc with this new `FWLiteWithPythonConfig.cc`. 

Paste `parameters.py` in $CMSSW_BASE/src/

Now go to $CMSSW_BASE/src/ re-compile and `cmsenv`. Run using 

`FWLiteWithPythonConfig parameters.py`

 A successful running of the FWLite executable FWLiteWithPythonConfig results in an output file called myZPeak_fwlite.root.

The output ROOT file myZPeak_fwlite.root is a bit different from myZPeak.root made in Exercise 17 since we did not make any of the electron histograms. The histograms do have the mumuMass, besides, muonEta, muonPhi and muonPt. 

 - 0) What is the number of entries in the mumuMass plot ?
 
 - 1) What is the mean mass in the mumuMass plot ?
 
 - 2) What is the mean pT, eta and phi for muons?
 
 
 Re-run using your crab results and answer: 
 
 - 3) What is the number of entries in the mumuMass plot using data sample ?
 
 - 4) What is the mean mass in the mumuMass plot using data sample ?
 
 - 5) What is the mean pT, eta and phi for muons using data sample ?
 
 - 6) What is the number of entries in the mumuMass plot using MC sample ?
 
 - 7) What is the mean mass in the mumuMass plot using MC sample ?
 
 - 8) What is the mean pT, eta and phi for muons using MC sample ?
 
 
  #### Exercise 19 - Fitting the Z mass peak 
  
  The main intention of fitting the Z mass peak is to show how to fit a distribution. To do this exercise will need the root file that you made in Exercises 17 and 18. Let us take the root file myZPeakCRAB.root for this exercise. Yo can use myZPeakCRAB_fwlite.root also, but just make sure to have the right name of the ROOT file. Both of these have the histogram mumuMass and that is what is important. The different distribution that we would fit to the Z mass peak are: 
  
 `Gaussian`
 
 ![gauss](http://latex.codecogs.com/gif.latex?G%28x%3B%5Cmu%2C%5Csigma%29%3D%5Cfrac%7B1%7D%7B%5Csqrt%7B2%5Cpi%7D%5Csigma%7D%5Cexp%5Cleft%5B-%5Cfrac%7B%28x-%5Cmu%29%7D%7B2%5Csigma%5E%7B2%7D%7D%20%5Cright%20%5D)
 
 `Relativistic Breit-Wigner`
 ![BW](http://latex.codecogs.com/gif.latex?B%28m%3BM%2C%5CGamma%29%3DN%5Ccdot%5Cfrac%7B2%7D%7B%5Cpi%7D%5Ccdot%5Cfrac%7B%5CGamma%5E%7B2%7DM%5E%7B2%7D%7D%7B%28m%5E%7B2%7D-M%5E%7B2%7D%29%5E%7B2%7D&plus;m%5E%7B4%7D%28%5CGamma%5E%7B2%7D/M%5E%7B2%7D%29%7D)
 
 `Convolution of relativistic Breit-Wigner plus interference term with a Gaussian`
 
 Some general remarks about fitting a Z peak:

To fit a generator-level Z peak a Breit-Wigner fit makes sense. However, reconstructed-level Z peaks have many detector resolutions that smear the Z mass peak. If the detector resolution is relatively poor, then it is usually good enough to fit a gaussian (since the gaussian detector resolution will overwhelm the inherent Briet-Wigner shape of the peak). If the detector resolution is fairly good, then another option is to fit a Breit-Wigner (for the inherent shape) convoluted with a gaussian (to describe the detector effects).This is in the "no-background" case. If you have backgrounds in your sample (Drell-Yan, cosmics, etc...), and you want to do the fit over a large mass range, then another function needs to be included to take care of this - an exponential is commonly used. 





