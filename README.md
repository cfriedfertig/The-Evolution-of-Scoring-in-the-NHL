# The-Evolution-of-Scoring-in-the-NHL
CSCI 334 (Data Mining) Final Project
By: Chase Friedfertig and Charles Fuller
Welcome to the github for our final project, The Evolution of Scoring in the NHL!
Necessary softwares: RapidMiner Studio 
Dataset(copy and paste into search bar): quanthockey.com

**What is this?**
We compared statistics of the top 10 National Hockey League (NHL) point scorers in the following seasons: 1998-1999 (the first season that all the data we need was all collected), 2008-2009, and 2018-2019. We are going to use these statistics to find patterns in based on the year and develop a thesis regarding the evolution of scoring. We used this data and our knowledge of the game to pick variables that we thought had a high effect on scoring.

**First Step** Scraping the Data
Download the data. Go to quanthockey.com and select year-by-year (2018-2019, 2008-2009, 1999-1998) and click export to excel for each (you should have 3 excel files). Once downloaded, we recommend renaming them by the year and putting them all in one folder so you can keep track of it. 

**Second Step** Cleaning the Data
Open one of the excel sheets:
  Step 1 (Delete the first row): Select 1 on the left side (highlighting the whole row), right click and click delete
  Step 2 (Delete the bottom 40): Select and Delete the entirety of cells 13-52
    REFERENCE: Look at lefthand side and click your shift button, and then on 13, and then continue to hold onto shift and click 52, then right click and       click delete. 
  Step 3 (Delete the useless variabels): Now you need to clear out variables that we won't use. Delete the following columns from the excel file:
  -PIM, ES, PP, SH, ESG, PPG, SHG, GWG, OTG, ESA, PPA, SHA, GWA, OTA, ESP, PPP, SHP, GWP, OTP, PPP%, G/60, A/60, P/60,  ESG/60, ESA/60, ESP/60, PPG/60,        PPA/60, PPP/60, G/GP, A/GP, P/GP, SH%, Hits, BS, FOW, FOL, FO%
  
  Great! Now that you have done this, you can repeat these steps for your other 2 sheets (Tip: It may be easier to throw the top 10 from each year all in     one excel file and do the steps once then reseparate the data to save time!)

**Third Step** Creating a Process
Open up RapidMiner Studio and create a blank process, save it early and name it referring to the year (i.e. "2018-2019 Model)
REFERENCE: If you aren't immediately prompted to start a new process, go to "File", "New Process", "Blank Process". Now you are ready to get started.

**Fourth Step** Importing the Dataset
After creating a new process in RapidMiner, you'll need to import your data. In the top left part of your server, you'll see an option to "Import Data". Click this and select one of your excel sheets. From here, you will want to make sure that you define the header row (the option will pop up when you import the data) as the row that contains the variable names(Rank, GP, G, etc.) and continue moving forward until you get asked where to save your data.

Here, you'll want to select "Local Repository" and then the subfolder "data" so you can easily find it

**Fifth Step** Creating the Model
First, we retrieved the data for each year
  HOW TO: Find the dataset in subfolder "data" and drag it into the middle of the process. Congrats! You got your dataset imported!

Second, we used the ”Set Role” function and set points as a label.
  HOW TO: 
        1) Go to the operators section in the bottom left corner of the server. Search for "Set Role" and drag it into the process. 
        2) You will see a small bubble to the right of your retrieved data, click on this and you'll be able to drag it to the "Set Role" operator. You                will want to connect it to the input port labeled "exa" on the left side of it. 
        3) Click on the "Set Role" operator and look at the options to the right of the process. 
        4) Change "attribute name" to P (representing Points) and change "target role" to label.
  
Third, we used the ”Split Data” function and set enumerations at 0.7 and 0.3 to split the training model from the real model.
  HOW TO: 
        1) Go back to the operators section and search for "Split Data" and drag it into the process.
        2) Similarly to the first connection, connect the exa output of the "Set Role" operator to the exa input of the "Split Data" operator.
        3) Click on the "Split Data" operator and go to the options to the right of the process.
        4) Next to partitions, click "Edit Enumerations". From here, you will want to click "add entry" and add 2 entries for 0.7 and 0.3
           a) This will split the data having 70% of it be in a training set.
           
  
Fourth, we connected the ”Split Data” to both a ”Deep Learning” operator and an ”Apply Method” operator sending the higher percentage through a deep learning model.
  HOW TO: 
        1) Search operators for "Deep Learning" and "Apply Method" and drag both operators into the process. 
        2) Connect your first par output from your "Split Data" operator to the tra (short for training) input of the "Deep Learning" operator. 
        3) Connect your second par output from your "Split Data" operator to the unl input of the "Apply Model" operator.
        4) Connect your mod output from your "Deep Learning" operator to the mod input of your "Apply Model" operator.
        
        You have now successfully split your data into the model.
  
Fifth, we added a performance operator testing for root mean squared error (RMSE) and absolute Error.
  HOW TO: 
        1) Search operators for "Performance" and select the "Performance" operator for regression. 







