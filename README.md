
Project Goal

The project is related to development of Monte Carlo simulation model for portfolio of COVID-19 vaccines. The model utilizes data on current COVID-19 vaccines in development across technology platforms. Vaccines are in various stages of clinical trials. Outcome of a clinical trial is defined by probability of success (POS) by using random generation. The model predicts how many vaccines will seek regulatory approval in certain time period, e.g. end of 2021 and their production and risk.  Also, the model predicts how much time is needed to produce 11.2B doses to eradicate pandemic and corresponding risk. The model includes interdependence rules for vaccines within a platform. If a trial is successful, POS increases by a %. Otherwise, decreases by a %. Also, in order to accelerate development, selected vaccines reaching Ph3 trials get additional financing. They can compress clinical trials cycle times and overlap them. 
Detailed overview of the methodology, modeling results and data presented in 
https://www.medrxiv.org/content/10.1101/2020.11.01.20214122v1
and 
https://www.appliedclinicaltrialsonline.com/view/simulation-model-for-productivity-risk-and-gdp-impact-forecasting-of-the-covid-19-portfolio-vaccines

The results of the project allow to predict outcome and risk of the portfolio of COVID-19 vaccines. It also allows to analyze various risk mitigation strategies (e.g. scaling up of the Operation Warp Speed (OWS)), and make assessments about global GDP impact of effective policies. 

Why the project is useful
The results of the project allow to predict outcome and risk of the portfolio of COVID-19 vaccines. It also allows to analyze various risk mitigation strategies (e.g. scaling up of the Operation Warp Speed (OWS)), and make assessments about global GDP impact of effective policies. 

Vaccine Pipeline Modelling

--------------------------

The model takes data on existing COVID-19 vaccines in various stages of clinical trials and expert opinions as to their likely success and predicts how many vaccines will get proper regulatory approval and on what timescales. The model uses Monte Carlo techniques to randomly decide an outcome given the input parameters.

High level algorithm overview
The model was coded in GPSS/H – general purpose simulation language. GPSS/H is a commercial tool. 

The code is presented in 
https://github.com/vovash1948/Portfolio-of-COVID-vaccines/blob/main/COVID_091120_C3.gps

The modeling code in GPSS/H language is grouped in sections. Each section relates to the specific model functionality. 

SECTION #1. Input data, variables, output data. 
SECTION #2. At the beginning of each simulation cycle, main transaction is originated. It is cloned (block SPLIT, SECTION #3). Numbers of cloned transactions = number of vaccines. Then multiple parameters are assigned to each transaction characterizing phase of a trial, platform, cycle time, lead vs. non-lead, etc. (SECTION #4)
Simulation time progresses on monthly basis. Cycle time for current phase is reduced. When is became zero, random variable from (0,1) interval is assigned to some value. (SECTION #5). If it exceeds probability of success (POS) for a platform and phase (INV2.SAV) then a trial is successful. Otherwise, a trial is failure. 

If a trial is a success, there are two options. 
1.	Trial successfully passed all three phases – approved (SECTION #7), and manufacturing of a vaccine started until cumulative production for all vaccines reaches demand (SECTION #8).
2.	Trial successfully passed a phase. Then the phase increases (e.g. from Ph1 to Ph2), new parameters including cycle time assigned (SECTION #9)

If a trial is failure (SECTION #6), after collecting corresponding statistics a transaction terminated. 
Interdependency rule.  If a trial fail, POS for all trials in the same phase and a platform will be reduced by some %. If a trial succeeds, POS for all trials in the same phase and a platform will be increased by some %. 
Scaling of Operation Warp Speed rule. For selected candidates, if they entered Ph3 trial, their cycle times will be compressed. 
Time counting and the end of simulation cycle (SECTION #10)
Simulation end – (SECTION #11) 
Reporting (SECTION #12). Information about trial failure or success is stored in the file. After simulation completed, information is sent to output files.
Model execution
The model can be run from an executable file on “PC-Lenovo” server. Remote access to the server is provided via Chrome remote desktop in several steps. 

https://support.google.com/chrome/answer/1649523

Share your computer with someone else
You can give others remote access to your computer. They’ll have full access to your apps, files, emails, documents and history.
1.	On your computer, open Chrome.
2.	In the address bar at the top, type remotedesktop.google.com/support, and press Enter.
3.	Under “Get Support”, click Download  .
4.	Follow the onscreen directions to download and install Chrome Remote Desktop.
5.	Under “Get Support,” select Generate Code.  
6.	Copy the code and send to the person you want to have access to your computer.
7.	When that person enters your access code on the site, you will see a dialog with their e-mail address. Select Share to allow them full access to your computer.
8.	To end a sharing session, click Stop Sharing.
The access code will only work one time. If you are sharing your computer, you will be asked to confirm that you want to continue to share your computer every 30 minutes.
When remote access to the server established, go to the drive G, directory C3. Click on “hpro” file. In Command Prompt window dialog type file name “COVID_091120_C3.gps” and press “Enter”. Execution time is about two seconds. Then in the same C3 directory, click on output files (please, see OUTPUT FILES for the list of names) 







