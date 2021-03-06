=====================
childcaremap/NYCdaycare
=====================
Project to map licensed day care centers for children 0-5 years in New York City.

Data from Bureau of Child Care at https://a816-healthpsi.nyc.gov/ChildCare/ChildCareList.do

Plan is to map the daycare centers, provide basic information (phone number, capacity, age range, etc) and summarize health inspection results.

Possible approaches to get data:

1. scrape data off website, quick and dirty. might not be sustainable
2. push the release of the data on the NYC Open Data site by bumping a request placed a year ago here: https://nycopendata.socrata.com/nominate/2570
3. contact the Department of Health and Mental Hygiene and ask for the data to be released via NYC Open Data: waiting for reply from Commissioner Mary Travis Bassett, M.D., MPH

Approaches for Scraping:

1. php based scrape script in "scraper" folder working for first layer data + some info from second layer (Service Name	Address	Zip Code	Phone	Permit Status, Borough, Permit No.) Note: do NOT run script without consulting with omnisite or schmiani! Data retrieved on March 30 2014 is saved on github as an mysql dump.
2. python scrapy, problems with form requests
3. ruby based script with mechanize is working, possibility to expand this code and/or translate it to python with mechanize

Combining permits:

Licenses are issued for 0-2 years or 2-5 years, therefore many child care centers are listed twice (or more times, if they have different types of premits, such as private and corporate etc.). Also, sometimes more than one daycare center are located at the same address. Because they have the same geolocation, only one of the entries will be visible in a map (unless artificial jitter is introduced, an approach not taken here). Python scripts in python_combine_and_geocode folder combines any permit at the same location into one entry, but preserves the different entries with slashes. This is done just for mapping, the original file is kept separately. Workflow is to combine permits for the exact same address, then geocode using pygeocoder (Google Geocoding API V3 without key, if several locations are returned, script chooses the first one in the list), then combine permits for the exact same geolocation (sometimes addresse is written differently for different permits, but the geolocation returned by Google is the same).

Mapping:

Right now, cartoDB is used for the mapping. It's difficult to update the information, but using their API could possibly make it easier. Looking into filter settings.

To view map http://childcaremap.github.io/NYCdaycare/

GitHub page is maintained in seperate gh-pages branch which gets updated with master but not vice-versa.
Jekyll with a modified single page responsive theme Solo. Docs are here https://github.com/chibicode/solo. Thanks to Shu Uesugi (<a href="http://twitter.com/chibicode">Twitter</a>/<a href="http://github.com/chibicode">GitHub</a>/<a href="https://plus.google.com/110325199858284431541?rel=author">G+</a>).

=====================
License:

This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/ or send a letter to Creative Commons, 444 Castro Street, Suite 900, Mountain View, California, 94041, USA.
