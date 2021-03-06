## PEcAn in a nutshell

PEcAn provides an interface to a variety of ecosystem models and attempts to standardize and automate the processes of model parameterization, execution, and analysis. First, you choose an ecosystem model, then the time and location of interest (a site), the plant community (or crop) that you are interested in simulating, and a source of atmospheric data from the BETY database (LeBauer et al, 2010). These are set in a "settings" file, commonly named `pecan.xml` which can be edited manually if desired. From here, PEcAn will take over and set up and execute the selected model using your settings. The key is that PEcAn uses models as-is, and all of the translation steps are done within PEcAn so no modifications are required of the model itself. Once the model is finished it will allow you to create graphs with the results of the simulation as well as download the results. It is also possible to see all past experiments and simulations.


## Quick Start

There are two ways of using PEcAn, via the web interface and directly within R. Even for users familiar with R, using the web interface is a good place to start because it provides a high level overview of the PEcAn workflow.The quickest way to get started is to download the virtual machine or use an AWS instance.

### Working with the PEcAn VM

1.    PEcAn consists of a set of scripts and code that is compiled within a Linux operating system and saved in a “virtual machine (VM)”. Virtual machines allow for running consistent set-ups without worrying about differences between operating systems, library dependencies, compiling the code, etc. 

2.  To run the PEcAn VM you will need to install VirtualBox, the program that runs the virtual machine [http://www.virtualbox.org](http://www.virtualbox.org). On Windows you may see a warning about Logo testing, it is okay to ignore the warning. 

3.	After you have Virtual Box installed you’ll need to download the PEcAn virtual machine: [http://opensource.ncsa.illinois.edu/projects/artifacts.php?key=PECAN](http://opensource.ncsa.illinois.edu/projects/artifacts.php?key=PECAN). The virtual machine is available under the "**Files**" header. Click the 32 or 64 bit ".ova" file and note that the download is ~5 GB so will take from several minutes to hours depending on the connection speed.

4.	To open up the virtual machine you'll first want to open up VirtualBox. 

5. The first time you use the VM you'll want to use File → Import Appliance in VirtualBox in order to import the VM. This will create a virtual machine from the disk image. When asked about the Appliance Import Settings make sure you select "Reinitialize the MAC address of all network cards". This is not selected by default and can result in networking issues since multiple machines might claim to have the same network MAC Address. That said, users who have experienced network connection difficulties within the VM have sometimes had better luck after reinstalling without reinitializing.
  ![](../../pic1.jpg)
6.  Next, click “Import”. You only have to do this Import step once, in the future you can just skip to the next step. 	

7.	Start Pecan by double clicking on the icon for the VM. A terminal window will pop up showing the machine booting up which may take a minute. It is done booting when you get to the “pecan32 login:” prompt. You do not need to login as the VM behaves like a server that we will be accessing through you web browser. Feel free to minimize the VM window.

#### Using AmazonWeb Services(AWS)
Login to Amazon Web Services (AWS), http://console.aws.amazon.com/ and select the EC2 Dashboard. If this is your first time using AWS you will need to set up an account before you are able to access the EC2 Dashboard. Important: You will need a credit card number and access to a phone to be able to verify AWS account registration. AWS is free for one year.

1.    Choose AMI
  a.  On the top right next to your name, make sure the location setting is on U.S. East (N. Virginia), not U.S. West (Oregon)
  b.	On the left click, click on EC2 (Virtual servers), then click on “AMIs”, also on the left
  c.	In the search window toggle to change “Owned by me” to “Public images”
  d.	Type “pecan” into the search window
  e.	Click on the toggle button on the left next to PEcAn1.4.6
  f.	Click on the “Launch” button at the top
2.	Choose an Instance Type 
  a.	Select what type of machine you want to run. For this demo the default, t2.micro, will be adequate. Be aware that different machine types incur very different costs, from 1.3 cents/hour to over $5/hr https://aws.amazon.com/ec2/pricing/   
    Select t2.micro, then click “Next: Configure Instance Details”
3.	Configure Instance Details 
  a.	The defaults are OK. Click “Next: Add Storage”
4.	Add Storage 
  a.	The defaults are OK. Click “Next: Tag Instance”
5.	Tag Instance 
  a.	You can name your instance if you want. Click “Next: Configure Security Group”
6.	Configure Security Group
  a.	You will need to add two new rules:
    i.	Click “Add Rule” then select “HTTP” from the pull down menu. This rule allows you to access the webserver on PEcAn.
    ii.	Click “Add Rule”, leave the pull down on “Custom TCP Rule”, and then change the Port Range from 0 to 8787. Set “Source” to Anywhere. This rule allows you to access RStudio Server on PEcAn.
  b.	Click “Review and Launch”  . You will then see this pop-up: 
     ![](../../pic2.jpg)
Select the default drive volume type and click Next
7.    Review and Launch
  a.  Review the settings and then click “Launch”, which will pop up a select/create Key Pair window.
8.	Key Pair 
  a.	Select “Create a new key pair” and give it a name. You won’t actually need this key unless you need to SSH into your PEcAn server, but AWS requires you to create one. Click on “Download Key Pair” then on “Launch Instances”. Next click on “View Instances” at the bottom of the following page.
9.	Instances 
![](../../pic3.jpg)
  a.    You will see the status of your PEcAn VM, which will take a minute to boot up. Wait until the Instance State reads “running”. The most important piece of information here is the Public IP, which is the URL you will need in order to access your PEcAn instance from within your web browser (see Demo 1 below). 
  b.  Be aware that it often takes ~1 hr for AWS instances to become fully operational, so if you get an error when you put the Public IP in you web browser, most of the time you just need to wait a bit longer.
  Congratulations! You just started a PEcAn server in the “cloud”!

10.    When you are done using PEcAn, you will want to return to the “Instances” menu to turn off your VM.
  a.  To STOP the instance (which will turn the machine off but keep your work), select your PEcAn instance and click Actions > Instance state > Stop. Be aware that a stopped instance will still accrue a small storage cost on AWS. To restart this instance at any point in the future you do not want to repeat all the steps above, but instead you just need to select your instance and then click Actions > Instance state > Start
  b.	To TERMINATE the instance (which will DELETE your PEcAn machine), select your instance and click Actions > Instance state > Terminate. Terminated instances will not incur costs. In most cases you will also want to go to the Volumes menu and delete the storage associated with your PEcAn VM.Remember, AWS is free for one year, but will automatically charge a fee in second year if account is not cancelled.


### Using PEcAn

#### Site-level Runs
The most basic function of PEcAn is run a model at the site level. The [Demo](http://pecanproject.github.io/tutorials.html) describes the basics of running the model at an existing sit and the following links will advise you on your options, diagnosis of potential issues, and will give you more in depth information about the interface.

* [Choose a model](Choose-a-model.md)
* [Choose a site](Choose-a-site.md)
* [Choosing PFTs](Choosing-PFTs.md)
* [Choosing meteorology](Choosing-meteorlogy.md)
* [Choosing initial vegetation](Coosing-initial-vegetation.md)
* [Choosing soils](Choosing-soils.md)


### Additional PEcAn Modules and Tools
The packages listed below were developed by the PEcAn team. Some are used within the workflow itself and others stand alone for now. Please take a look through their documentation to get a better feel for the utilities of PEcAn.

| Package name | documentation | source code | description |
|:---|:---|:---|:---|
|**Utilities**| | |
|PEcAn.all| [all](https://pecanproject.github.io/pecan//all/inst/web/index.html) | [all](https://github.com/PecanProject/pecan/tree/master/all)  | Wrapper to facilitate loading of core packages|
| PEcAn.DB| [db](https://pecanproject.github.io/pecan//db/inst/web/index.html)|[db](https://github.com/PecanProject/pecan/tree/master/db)  |Interface to database containing data, provenance, and results|
|PEcAn.settings| [settings](https://pecanproject.github.io/pecan//settings/inst/web/index.html)| [settings](https://github.com/PecanProject/pecan/tree/master/settings)  | Package to read PEcAn settings files|
| PEcAn.utils | [utils](https://pecanproject.github.io/pecan//utils/inst/web/index.html)| [utils](https://github.com/PecanProject/pecan/tree/master/utils)  | Utility functions used by many PEcAn packages|
|PEcAn.visualization| [visualization](https://pecanproject.github.io/pecan//visualization/inst/web/index.html)| ||
|**Workflow Modules**| | |
|PEcAn.allometry | [allometry](https://pecanproject.github.io/pecan//modules/allometry/inst/web/index.html) |  [allometries ](https://github.com/PecanProject/pecan/tree/master/modules/allometry)  | Bayesian synthesis of allometric equations|
|PEcAn.assim.batch| [assim.batch](https://pecanproject.github.io/pecan//modules/assim.batch/inst/web/index.html) | [assim.batch ](https://github.com/PecanProject/pecan/tree/master/modules/assim.batch) | Batch data assimilation tools (e.g. MCMC)
|PEcAn.assim.sequential| [assim.sequential](https://pecanproject.github.io/pecan//modules/assim.sequential/inst/web/index.html)| [assim.sequential ](https://github.com/PecanProject/pecan/tree/master/modules/assim.sequential) | Sequential data assimilation tools (e.g. EnKF, particle filter)
|PEcAn.benchmark| |  [benchmark ](https://github.com/PecanProject/pecan/tree/master/modules/benchmark)  | Model benchmarking
|PEcAn.data.atmosphere| [data.atmosphere](https://pecanproject.github.io/pecan//modules/data.atmosphere/inst/web/index.html)| [data.atmosphere ](https://github.com/PecanProject/pecan/tree/master/modules/data.atmosphere) | Meteorology workflow|
|PEcAn.data.land| [data.land](https://pecanproject.github.io/pecan//modules/data.land/inst/web/index.html)| [data.land ](https://github.com/PecanProject/pecan/tree/master/modules/data.land/R) | Tools for land and vegetation data. At the moment predominantly Bayesian state-space tree-ring models.|
|PEcAn.data.remote| [data.remote](https://pecanproject.github.io/pecan//modules/data.remote/inst/web/index.html)| [data.remote ](https://github.com/PecanProject/pecan/tree/master/modules/data.remote/R) | Tools for remotely sensed data|
|PEcAn.emulator| [emulator](https://pecanproject.github.io/pecan//modules/emulator/inst/web/index.html)| [emulator ](https://github.com/PecanProject/pecan/tree/master/modules/emulator/R) | Tools for emulating models. Used in parameter data assimilation|
|PEcAn.MA | [meta.analysis](https://pecanproject.github.io/pecan//modules/meta.analysis/inst/web/index.html)| [meta.analysis ](https://github.com/PecanProject/pecan/tree/master/modules/meta.analysis) | Trait assimilation workflow & hierarchical Bayes meta-analysis|
|PEcAn.photosynthesis | [photosynthesis](https://pecanproject.github.io/pecan//modules/photosynthesis/inst/web/index.html)|  [photosynthesis ](https://github.com/PecanProject/pecan/tree/master/modules/photosynthesis) | Hierarchical Bayes fitting of the Farquhar model |
|PEcAn.priors | [priors](https://pecanproject.github.io/pecan//modules/priors/inst/web/index.html) | [priors ](https://github.com/PecanProject/pecan/tree/master/modules/priors)  | tools for fitting priors to data and expert constraint|
|PEcAnRTM | [rtm](https://pecanproject.github.io/pecan//modules/rtm/inst/web/index.html)| [rtm ](https://github.com/PecanProject/pecan/tree/master/modules/rtm)   | Radiative Transfer Modeling tools; hierarchical Bayes inversion of PROSPECT |
|PEcAn.uncertainty | [uncertainty](https://pecanproject.github.io/pecan//modules/uncertainty/inst/web/index.html) | [uncertainty ](https://github.com/PecanProject/pecan/tree/master/modules/uncertainty) | Sensitivity and Uncertainty Analysis workflow. Variance Decomposition|
|**Model Wrappers** | | | 
|PEcAn.BIOCRO| [biocro](https://pecanproject.github.io/pecan//models/biocro/inst/web/index.html) | [biocro](https://github.com/PecanProject/pecan/tree/master/models/biocro)|
|PEcAn.CLM| [clm45](https://pecanproject.github.io/pecan//models/clm45/inst/web/index.html) |[clm45](https://github.com/PecanProject/pecan/tree/master/models/clm45) |
|PEcAn.DALEC| [dalec](https://pecanproject.github.io/pecan//models/dalec/inst/web/index.html) |[dalec](https://github.com/PecanProject/pecan/tree/master/models/dalec) |
|PEcAn.ED| [ed](https://pecanproject.github.io/pecan//models/ed/inst/web/index.html) | [ed](https://github.com/PecanProject/pecan/tree/master/models/ed)|
|PEcAn.GDAY| [gday](https://pecanproject.github.io/pecan//models/gday/inst/web/index.html) |[gday](https://github.com/PecanProject/pecan/tree/master/models/gday) |
|PEcAn.LINKAGES| [linkagers](https://pecanproject.github.io/pecan//models/linkages/inst/web/index.html) |[linkages](https://github.com/PecanProject/pecan/tree/master/models/linkages) |
|PEcAn.LPJGUESS| [lpjguess](https://pecanproject.github.io/pecan//models/lpjguess/inst/web/index.html) |[lpjguess](https://github.com/PecanProject/pecan/tree/master/models/lpjguess) |
|PEcAn.MAAT| [maat](https://pecanproject.github.io/pecan//models/maat/inst/web/index.html) |[maat](https://github.com/PecanProject/pecan/tree/master/models/maat) |
|PEcAn.MAESPA| [maespa](https://pecanproject.github.io/pecan//models/maespa/inst/web/index.html) |[maespa](https://github.com/PecanProject/pecan/tree/master/models/maespa) |
|PEcAn.PRELES| [preles](https://pecanproject.github.io/pecan//models/preles/inst/web/index.html) |[preles](https://github.com/PecanProject/pecan/tree/master/models/preles) |
|PEcAn.SIPNET| [sipnet](https://pecanproject.github.io/pecan//models/sipnet/inst/web/index.html) |[sipnet](https://github.com/PecanProject/pecan/tree/master/models/sipnet) |




### Beyond the Basics

If you are interested in learning more about configuring PEcAn to fit your usage needs, continue on to the [Advanced user section](../advanced_users_guide.md)


