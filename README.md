# Exercise 6 - Data analysis with Pandas

In this week's exercise we will continue developing our skills using Pandas to analyze climate data.

After making your changes, you will need to upload your files to GitHub.
The answers to the questions in this week's exercise should be given by modifying the document in the requested places.

If you are uncertain about **the style of your code**, take a look at the **[PEP 8 - Style guide for Python code](https://www.python.org/dev/peps/pep-0008/)**.  

 - **Exercise 6 is due by the start of lecture on 18.10.**
 - Don't forget to check out the [hints for this week's exercise](https://geo-python.github.io/2017/lessons/L6/exercise-6-hints.html) if you're having trouble.
 - Scores on this exercise are out of 20 points.
 - There are altogether 4 problems that you should solve. The fifth problem is optional (Problem 2.1) for more advanced students (does not affect grading)

# Data

For problems 1-3 in this exercise we will be using climate data from the Helsinki-Vantaa airport station.
For these problems, we have daily observations obtained from the [NOAA Global Historical Climatology Network](https://www.ncdc.noaa.gov/cdo-web/search?datasetid=GHCND).
The file was downloaded using the "Custom GHCN-Daily Text" output format, including the geographic location, precipitation (`PRCP`), average temperature (`TAVG`), maximum temperature (`TMAX`), and minimum temperature (`TMIN`).
The file for this problem is exactly as available from the NOAA website.
You should start by downloading [a copy of the data file](1091402.txt).
Note once again that temperatures in this dataset are given in degrees Fahrenheit, as noted in the [sample data file](ftp://ftp.ncdc.noaa.gov/pub/data/cdo/samples/GHCND_sample_pdf.pdf).
Additional information about the data format can be found in the [hints for Exercise 6](https://geo-python.github.io/2017/lessons/L6/exercise-6-hints.html).

# Problem 1 - Reading in a tricky data file (6 points)

You first task for this exercise is to read in the data file to a variable called `data`.
This should be done using the `read_csv()` function in Pandas, and the resulting DataFrame should have the following attributes:

  - The numerical values for rainfall and temperature read in as numbers
  - The second row of the datafile should be skipped, but the text labels for the columns should be from the first row
  - The no-data values should properly be converted to `NaN`

You can find hints about how to do these things in the [description of Exercise 5](https://github.com/Geo-Python-2017/Exercise-5) and the [hints for Exercise 6](https://geo-python.github.io/2017/lessons/L6/exercise-6-hints.html).

- How many non-NaN values are there for `TAVG`?
- What about for `TMIN`?
- How many days total are covered by this data file?
- When is the first observation?
- When is the last?
- What was the average temperature of the whole data file (all years)?
- What was the average temperature of the ``Summer 69`` (i.e. including months May, June, July, August of the year 1969)?

**For this problem**

1. Create a new script file called `temperature_anomalies.py`
2. Make sure the script can read in the data file
3. Have the script print out the requested values for the questions above to the screen
4. Upload a copy to your repository for this week's exercise.

# Problem 2 - Calculating monthly average temperatures (5 points)

For this problem our goal is to calculate monthly average temperature values in degrees Celsius from the daily values we have in the data file.
You can use the approaches taught during the Lesson 6 to solve this .
You can again consult the [hints for Exercise 6](https://geo-python.github.io/2017/lessons/L6/exercise-6-hints.html) if you are stuck.

**For this problem modify your `temperature_anomalies.py` script to**

1. Calculate the monthly average temperatures for the entire data file using the approaches taught during the lecture
2. Save the output to a new Pandas Series called `dataMonths`
3. Create a second Series called `dataMonthsC` that has the monthly temperatures in Celsius.
4. Merge the two data Series into a single Pandas DataFrame called `monthlyData` using the `pd.concat()` function (see the [documentation of Pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.concat.html) or hints if needed).
4. Upload the updated script to your repository for this week's exercise.

## Problem 2.1 (optional)

You goal is to figure out how to use the datetime functionalities of Pandas shortly mentioned in the [Lesson 6 materials](https://geo-python.github.io/2017/lessons/L6/lessons/L6/pandas-analysis.html#string-manipulation-in-pandas.html).
You should find out how to create a DataTime index in Pandas and use the `DataFrame.resample()` function to directly calculate the mean monthly temperatures from the daily observation values.

# Problem 3 - Calculating temperature anomalies (4 points)

Our goal in this problem is to calculate monthly temperature anomalies in order to see how temperatures have changed over time, relative to the observation period between 1952-1980.
We will again do this by modifying your `temperature_anomalies.py` script.
In order to complete the problem, you must do two things:

- You need to calculate a mean temperature *for each month* for the period 1952-1980 using the data in the data file.
    Note that the monthly mean here is slightly different than the monthly mean temperatures calculated earlier.
    Here, we are looking to find the mean temperature for January in the period 1952-1980, February for the same period, etc.
    You should end up with 12 values, 1 mean temperature for each month in that period, and store them in a Pandas Series called `referenceTemps`.
    Remember, these temperatures should be in degrees Celsius.

- Once you have the monthly mean values for each of the 12 months, you can then calculate a temperature anomaly for every month in the `monthlyTemps` DataFrame.
    The temperature anomaly we want to calculate is simply the temperature for one month in `monthlyTemps` minus the corresponding monthly average temperature from the `referenceTemps` data Series.
    You should thus end up with a new column in the `monthlyTemps` DataFrame showing the temperature anomaly, the difference in temperature for a given month (e.g., February 1960) compared to the average (e.g., for February 1952-1980).

- Upload the updated script to your repository for this week's exercise.


## Problem 4

Download your own data (daily summaries for years **1959-2017 August**) for **Rovaniemi Lentoasema**, from [NOAA Climate Data Online Search](https://www.ncdc.noaa.gov/cdo-web/search?datasetid=GHCND).
Make sure to click on starting day (and ending day) in the date selection panel after changing year!
After you have searched, click “Add to cart” for a selected station, then go to cart. Select the ``Custom GHCN-Daily Text`` -format for the resulting output file and hit continue.
From ``Station Detail & Data Flag Options`` choose all available attributes, i.e. Station Name, Geographic Location, Include Data Flags (and optionally Precipitation which is a separate button below).
Use **Standard** units. From the next page, add your own email address where the weather data will be sent after a short moment.

Write your codes into a separate `weather_comparisons.py` file.

After you have downloaded the data. You should use the approaches learned during this week and the same approaches as in Problem 3 to answer / do:

- Were there weather anomalies in Rovaniemi?
- Calculate the monthly temperature differences between Rovaniemi and Helsinki stations
- How different the summer temperatures (June, July, August) have been between Helsinki (used in Problems 1-3) and Rovaniemi station?
    - Calculate the monthly differences into a DataFrame and save it into your own Exercise repository for this week
    - What were the summer mean temperatures for both of these stations?
    - What were the summer standard deviations for both of these stations?
- Upload your script and data to GitHub.


1. Calculate the mean values for the temperatures for each month in the years 1952-1980 in a data Series
2. Determine temperature anomalies for every month in the `monthlyTemps` DataFrame
3. Print out the temperature anomalies for the month of February 2015
4. Upload your updated script to your repository for this week's exercise
