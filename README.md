# Covid-19-Spread-Tracker✔
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/Nidhi786sharma/Covid-19-Spread-Tracker/graphs/commit-activity) [![GitHub issues](https://img.shields.io/github/issues/Nidhi786sharma/Covid-19-Spread-Tracker)](https://github.com/Nidhi786sharma/Covid-19-Spread-Tracker/issues)[![GitHub fork](https://img.shields.io/github/forks/Nidhi786sharma/Covid-19-Spread-Tracker?style=social)](https://github.com/Nidhi786sharma/Covid-19-Spread-Tracker/network) [![GitHub stars](https://img.shields.io/github/stars/Nidhi786sharma/Covid-19-Spread-Tracker?style=social)](https://github.com/Nidhi786sharma/Covid-19-Spread-Tracker/stargazers) [![Open Source Love svg1](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badges/)


A very warm welcome to all those who are here!✨ This Repository is made to ease the work of those coders who are working on tracking the COVID-19 spread.
This code helps you all in finding the spread of COVID-19 through a graph. This graph shows the Total no. of Covid-19 Patients, including No. of deaths, No. of recovered of each state and each country.


You can also get the code from below.
## Code
    import pycountry
    import plotly.express as px
    import pandas as pd

## ----------- Step 1 ------------

    URL_DATASET = r'https://raw.githubusercontent.com/datasets/covid-19/master/data/countries-aggregated.csv'

      df1 = pd.read_csv(URL_DATASET)
      # print(df1.head) # Uncomment to see what the dataframe is like

## ---------- Step 2 ------------

    list_countries = df1['Country'].unique().tolist()

    # print(list_countries) # Uncomment to see list of countries

    d_country_code = {}  # To hold the country names and their ISO

     for country in list_countries:

    try:
        country_data = pycountry.countries.search_fuzzy(country)
        #country_data is a list of objects of class pycountry.db.Country
        #The first item  ie at index 0 of list is best fit
        #object of class Country have an alpha_3 attribute
        country_code = country_data[0].alpha_3 
        d_country_code.update({country: country_code})
    except:
    print('could not add ISO 3 code for ->', country)
        # If could not find country, make ISO code ' '
        d_country_code.update({country: ' '})
    # print(d_country_code) # Uncomment to check dictionary  

    # create a new column iso_alpha in the df
    # and fill it with appropriate iso 3 code
    for k, v in d_country_code.items():
    df1.loc[(df1.Country == k), 'iso_alpha'] = v    
    #print(df1.head)  # Uncomment to confirm that ISO codes added

## ---------- Step 3 ------------
    fig = px.choropleth(data_frame = df1,
                    locations= "iso_alpha",
                    color= "Confirmed",  # value in column 'Confirmed' determines color
                    hover_name= "Country",
                    color_continuous_scale= 'RdYlGn',  #  color scale red, yellow green
                    animation_frame= "Date")

     fig.show()
     
## Fork this repository

Fork this repository by clicking on the fork button on the top of this page. This will create a copy of this repository in your account.

## Clone the repository

Now clone the forked repository to your machine. Go to your GitHub account, open the forked repository, click on the clone button and then click the *copy to clipboard icon.*

Open a terminal and run the following git command:
'''
      git clone "url you just copied"
'''
where "url you just copied" (without the quotation marks) is the url to this repository (your fork of this project). See the previous steps to obtain the url.

For example:

     git clone https://github.com/Your_Username/Covid-19-Spread-Tracker.git

where Your_Username is your GitHub username. Here you're copying the contents of the Covid-19-Spread-Tracker repository on GitHub to your computer.





## *Created and Maintained with 💖, by NIDHI(https://twitter.com/Nidhish55851979)*

