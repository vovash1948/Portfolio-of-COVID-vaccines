
README file 
What the project does
The project is related to development of Monte Carlo simulation model for portfolio of COVID-19 vaccines. The model utilizes data on current COVID-19 vaccines in development across technology platforms. Vaccines are in various stages of clinical trials. Outcome of a clinical trial is defined by probability of success (POS) by using random generation. The model predicts how many vaccines will seek regulatory approval in certain time period, e.g. end of 2021 and their production and risk.  Also, the model predicts how much time is needed to produce 11.2B doses to eradicate pandemic and corresponding risk. The model includes interdependence rules for vaccines within a platform. If a trial is successful, POS increases by a %. Otherwise, decreases by a %. Also, in order to accelerate development, selected vaccines reaching Ph3 trials get additional financing. They can compress clinical trials cycle times and overlap them. 
Detailed overview of the methodology, modeling results and input data presented in https://www.medrxiv.org/content/10.1101/2020.11.01.20214122v1
and https://www.appliedclinicaltrialsonline.com/view/simulation-model-for-productivity-risk-and-gdp-impact-forecasting-of-the-covid-19-portfolio-vaccines
Why the project is useful
The results of the project allow to predict outcome and risk of the portfolio of COVID-19 vaccines. It also allows to analyze various risk mitigation strategies (e.g. scaling up of the Operation Warp Speed (OWS)), and make assessments about global GDP impact of effective policies. 
Vaccine Pipeline Modeling

The model takes data on existing COVID-19 vaccines in various stages of clinical trials and expert opinions as to their likely success and predicts how many vaccines will get proper regulatory approval and on what timescales. The model uses Monte Carlo simulation technique to randomly decide an outcome given the input parameters. Also the model calculates production output for vaccines portfolio and corresponding risk. 

High level algorithm overview
The model was coded in GPSS/H – general purpose simulation language. GPSS/H is a commercial tool, however, it is possible to get access to the model (please, see instructions below)

The code is presented in 
https://github.com/vovash1948/Portfolio-of-COVID-vaccines/blob/main/COVID_091120_C3.gps

The modeling code in GPSS/H language is grouped in sections. Each section relates to the specific model functionality. 

SECTION #1. Input data, variables, output data. 
SECTION #2. At the beginning of each simulation cycle, main transaction is originated. It is cloned (block SPLIT, SECTION #3). Numbers of cloned transactions = number of vaccines. Then multiple parameters are assigned to each transaction characterizing phase of a trial, platform, cycle time, lead vs. non-lead, etc. (SECTION #4)
Simulation time progresses on monthly basis. Cycle time for current phase is reduced. When is became zero, random variable from (0,1) interval is assigned to some value. (SECTION #5). If it exceeds probability of success (POS) for a platform and phase (INV2.SAV) then a trial is successful. Otherwise, a clinical trial is failure. 

If a trial is a success, there are two options. 

1.	Trial successfully passed all three phases – approved (SECTION #7), and manufacturing of a vaccine started until cumulative production for all vaccines reaches demand (SECTION #8).
2.	Trial successfully passed a phase. Then the phase increases (e.g. from Ph1 to Ph2), new parameters including cycle time assigned (SECTION #9)

If a trial is failure (SECTION #6), then after collecting corresponding statistics a transaction is terminated. 
Interdependency rule.  If a trial fail, POS for all trials in the same phase and a platform will be reduced by some % down to minimum probability. If a trial succeeds, POS for all trials in the same phase and a platform will be increased by some % up to maximum probability. Minimum and maximum probabilities were defined by experts. 
Scaling of Operation Warp Speed rule. For selected candidates, if they enter Ph3 clinical trial, their cycle times will be compressed. 
Time counting and the end of simulation cycle (SECTION #10)
Simulation end – (SECTION #11) 
Reporting (SECTION #12). Information about trial failure or success is stored in output files.
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

When remote access to the server established, go to the drive G, directory C3 (G:\C3). Click on “hpro” file. In Command Prompt window dialog type file name “COVID_091120_C3.gps” and press “Enter”. Execution time is about two seconds. Then open MS Excel, select an output file you need in G:\C3 directory, open it and convert it into .csv format using the following prompts. (Please, see OUTPUT_FILES.xls for the list of names).  
If you have any questions, please, email me at vladimir.shnaydman@orbeeconsulting.com 
Example: After execution of the model, MS Excel needs to be opened. Then, if you would like to present graph “Vaccine approvals output vs. development risk” in Excel environment, click on file MSSB15.out. In the box, click NEXT two times, and then FINISH. MSSB15.out will open in the csv format. MSSB15.out file represents vaccine approvals for each platform and each simulation cycle. Columns are technology platforms listed in OUTPUT_FILES.xls. Rows represent number of vaccines approvals for different technology platforms for each simulation cycle. 

In order to replicate Figure 2 (Approvals across platforms vs. development risk “Descriptive paper”), all columns related to technology platforms need to be sorted from minimum to maximum number of approvals, and then presented as a graph in MS Excel.  







Input files
All files are text format. Originally, all files are in MS Excel, but then, converted to text files (currently manually). All data for the model is in the https://www.medrxiv.org/content/10.1101/2020.11.01.20214122v1
and in Input data file in the Github. 
INV1.SAV   - # vaccines, number of months in planning horizon,  # cycles, number phases, platforms, # leading vaccines, vaccine demand, # in-licencing deals, % increase or decrease manufacturing capacity
INV1A2.SAV – min probability for each platform
INV1A3.SAV - max probability for each platform
INV1A4.SAV - interdependence coefficients for each platform (success > 1)
INV1A5.SAV - interdependence coefficients for each platform, failure <1
INVB1.SAV - production capacity for each platform
INV2.SAV – probabilities of success for each phase and platform. 
INV4.SAV - lead vaccine (Operation Warp Speed (OWS)) vs. non-lead
INV5A.SAV – trials allocation across platforms
INV6.SAV – start phase for each candidate
INV7.SAV – number of trials per phase and platform
INV10.SAV – platform # for each vaccine
INV13.SAV- leading vaccine candidates (OWS) – numbers
INV14A.SAV – duration of a clinical trial
INV14B.SAV – accelerated duration of a clinical trial
INV16.SAV – number to start next platform (vaccine group)
INV17.SAV – number to calculate end of the group (for interdependence) 

Output files
Text format manually converted to csv and then to MS Excel for the processing. 
MSSB1.OUT – Lead approved vaccines
MSSB2.OUT - Time for approval
MSSB3.OUT - Priority vaccines numbers
MSSB4.OUT – Manufacturing allocation across platforms
MSSB5.OUT – R&D allocation across platforms
MSSB7.OUT – total approvals R&D and manufacturing
MSSB8.OUT – R&D time across platforms
MSSB9.OUT – Production dynamic, cycle, month 1-20 (current limitations) 
MSSB10.OUT - Production dynamic, cycle, month 21-40
MSSB10A.OUT 	- Production dynamic, cycle, month 41-60
MSSB10B.OUT 	- Production dynamic, cycle, month 61-80
MSSB10C.OUT 	- Production dynamic, cycle, month 81-100
MSSB11.OUT - total approvals
MSSB12.OUT – lead approvals in a given interval		
MSSB13.OUT – total approvals in a given interval		
MSSB15.OUT - lead approvals allocation across platforms
MSSB16.OUT - Max manufacturing time
KSSB1.OUT – KSSB8.OUT – production allocation across eight platforms
More details about output files are in output_files.xls 




