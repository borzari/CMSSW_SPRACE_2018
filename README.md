# PyRoot

 This exercise is intended to provide you with basic familiarity with pyROOT provides bindings for all classes within the ROOT libraries and allows for replacing the usual C++ with the often less cumbersome python. The goal is to obtain a general understanding of the syntax required to import and make use of the ROOT libraries within a basic python script. Various examples are provided in order to demonstrate TH1 histogram manipulation including; reading from a .root file, creating, binning, re-binning, scaling, plotting and fitting to a Gaussian.

Whether you use python or C++ to complete your analysis is a personal preference however with the current lack of documentation on pyROOT many students stick with C++ in order to ensure their access to coding examples and experts. It is our hope that through providing you with this basic introduction and Github repository of example scripts, which you are encouraged to add to, that we can bring together the existing pyROOT community within CMS and foster its growth. 

You can look [pyROOT tutorial](https://www-zeuthen.desy.de/~middell/public/pyroot/pyroot.html).

First, we can open a TBrowser in python:

`python -i`

`>>> import ROOT`

`>>>tb = ROOT.TBrowser()`

### Exercise 21 - Introduction to pyROOT

Clone in your $CMSSW_BASE/src/ this git folder:

`https://github.com/denerslemos/pyROOTforCMSDAS.git`

After this, you can check the contents of the test directory :

`cd pyROOTforCMSDAS/test`

`ls -l`

##### Example 1 - Make a histogram

We begin with a very short example illustrating an efficient way to import the ROOT libraries, read a histogram from a .root file, then plot it on a canvas. First have a look in:

`hist1.py`

So let's run the script to produce the same histogram that we just viewed from the TBrowser: 

`python -i hist1.py`

If you do not want to keep the graphical display of the histogram open when you run the script, and only run the script (to produce the output file) while suppressing the graphics: 

`python hist1.py -b`


##### Example 1 - Fit a histogram

We proceed with another short example which builds on the first but also illustrates some commonly used histogram manipulations such as; creating, binning, re-binning, scaling, fitting to a Gaussian and saving to various file types.

First, lets have a look at the file: 

`hist2.py`

Now if we run the script we see the following output with information about the fit for each histogram.  

`python -i hist2.py`


- 0) What is the mean value of the Gaussian fit of the jet mass spectrum for jets of pt 300-400 GeV ? 

 Hopefully this extremely brief introduction has peaked your interest in pyROOT and encouraged you to learn more about this versatile tool. 
