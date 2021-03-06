% Python R Visualisations

Mapping academic collaborations in Evolutionary Biology
=======================================================

_This post is a republication of a visualisation I did in 2011 for my (now defunct) datajujitsu.co.uk blog.  It was a naive first attempt at web-scraping from an academic publishers website.  It was done before I was aware of the problems surrounding access to, and text-mining of, online academic content hosted by publishers such as Wiley and Elsevier. Producing such a piece now (in 2013) would certainly be regarded as a political act. The text and visualisations are unchanged from the original_

Like many people, I was immensely impressed with Paul Butler's [global map of facebook friend connections](http://paulbutler.org/archives/visualizing-facebook-friends/), a spectacular way of visualising, and humanising, a large amount of raw data.
I was further impressed to find out that he did it solely using R. I recently found Flowingdata's [tutorial](http://flowingdata.com/2011/05/11/how-to-map-connections-with-great-circles/) on creating the same effect using flight information and got to thinking about what other datasets I could apply it to.
My original plan was to build a scraper to get all of the abstracts from a particular subject from [Pubmed](http://www.ncbi.nlm.nih.gov/pubmed/) and visualise the academic collaborations between institutions for all of these abstracts. Unfortunately though, Pubmed only stores the addresses of the institutions of the corresponding author, so I decided to stick with my own subject, evolutionary biology, and get all the abstacts from the journals [Evolution](http://onlinelibrary.wiley.com/journal/10.1111/(ISSN)1558-5646) and [Evolutionary Biology](http://onlinelibrary.wiley.com/journal/10.1111/(ISSN)1420-9101) since 2009. I could then extract these using a hacked together Python script which would then feed the addresses into the [Yahoo PlaceFinder](http://developer.yahoo.com/geo/placefinder/) api to get a data set of coordinates for each cross-institution collaboration in every paper published in the journals for the last two and a half years.
I then fed this data into R, generated great circles for each of the collaborations using the geosphere package and processed it a la FlowingData to get the following global map of academic collaboration in evolutionary biology since 2009:

![Evolution social network 2009-2011](/img/evolution_social_network.png)

You can clearly see the main hubs of collaboration in Europe and the East and West coasts of the USA, with smaller hubs in Japan and South-Eastern Australia. There are further actively collaborating institutions in South America and Africa, but almost all of their collaborations are with North american and European Universities. Looking into the data itself, the median longitude for JEB institutions is firmly in Europe, while the median longitude for Evolution in the USA (This makes sense since Evolution is based in the states while JEB is a European journal, though there is no geographic imperative to publish in either).
Technical info:
I scraped the data from the Wiley website for the two journals using Python and BeautifulSoup. For the R analysis I used the modules maps, geosphere, reshape and gdata.
