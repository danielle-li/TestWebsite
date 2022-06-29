# Sexist and sexualized language in rock climbing route names

This folder provides supporting data and code for an analysis of potentially offense climbing route names, available [here](https://danielle-li.github.io/climbing-routes/).  This analysis was done as part of a project for the [Lede Program in Data Journalism](https://ledeprogram.com/) at Columbia University.  

## Data Sources

The data come from [OpenBeta.io](https://openbeta.io/), specifically the dataset on all US climbing routes compiled by [Ryther Anderson](https://twitter.com/andersonryther) (thank you!).  

## Analysis

Analysis was done with Python and visualization was done with Datawrapper.  The dataset includes the text of climbing route names, along with information on their location, grade, and first ascent information.  

To identify a route as "potentially offensive" I searched the text of the route name for keywords related to sexual anatomy, as well as language related to gender, gender identity, sexual orientation, and racial and ethnic identity.  To benchmark the frequency of terms, I also searched the route names for common descriptors of climbing route features (e.g. "arete," "slab" etc.).  See code for the specific list of words.  I then extracted route locations and mapped them using Datawrapper.  The interactive map assumes that those listed as first ascending the route were those that also named the route.

## Want to improve the analysis?

Please do!  This was done as part of an introductory data journalism class so the analysis is rudimentary.  Here are a few things I or someone else should do better. I'm sure there are others too!

- **Improving text matching technique**.  The current matches a route if it contains the exact string in a list.  Under this approach, "Whoreizontal" would match to "whore" (good) but "ho" would also match to "show" (bad).  To avoid false positives, I included " ho " (with spaces) as a term to match, but not "ho" (no space).  This will lead to more false negatives, e.g. routes with names beginning or ending in "ho" will not match because they lack the space afterward.  Moving to exact word matches would reduce matches for portmanteaus such as "Frankenwhore."  Anyway, lots to be gained from even slightly better text matching.  

- **Improving offensive language dictionary**.  The current list of terms to match was derived in an ad hoc manner, basically a combination of words that naturally come to mind as well as words that came up when I actually looked through route names.  There were also a variety of editorial decisions regarding the inclusion of terms that are not offensive per se, e.g. the use of "dyke" by members of the LGBTQ community, but which often are in the context of climbing routes.  I ended up including "dyke" in the list of potentially offensive words to match but I did not include "lesbian."  There is probably a better (or at least less immediately subjective) dictionary out there.  

- **Improving context matching**.  The current list for the most part ignore routes that are offensive in context but which do not include words that are themselves individually offensive, e.g. "Slanty Eyes."  Potential offenders that are ignored include "hole", "plow" etc.  Ignoring context may also lead to false positives (sometimes a beaver is just a beaver).  

- **Potentially offensive language as it relates to race, ethnicity, sexual identity or orientation**.  The code includes some attempts to identify this, but I did not include the results in the main write up because there were too many instances of both false positives and false negatives.  There were relatively few instances of explicit racial slurs (e.g. the n-word).  Among other terms, I found it difficult to assess context and valence.  "Black," for instance, is one of the most common words that appears in climbing routes, but it can reference non-racial things (the color of a wall, black widow, etc), or it can reference racial identity in a non-derogatory way.  Similarly, words such as "gay" or "Asian" can have a variety of valances, so it was difficult to take a stand.  

## Repository contents

#### Code
- [OpenBeta.ipynb](./Code/OpenBeta.ipynb).  Located in the Code folder.  Takes the input datasets and spits out CSVs to input into Datawrapper.

#### Input Data
- [Curated_OpenBetaAug2020_RytherAnderson.pkl](./InputData/Curated_OpenBetaAug2020_RytherAnderson.pkl) from [Open Beta](https://github.com/OpenBeta/climbing-data/blob/main/curated_datasets/Curated_OpenBetaAug2020_RytherAnderson.pkl.zip).  This data includes technical climbing routes found in the Open Beta database as of August 2020.  For more details, see the documentation [here](https://github.com/OpenBeta/climbing-data/blob/main/curated_datasets/OpenBetaData_Curation.ipynb).

#### Final Data
- [df_chart_norating.csv](./FinalData/df_chart_norating.csv) and [df_chart_norating_clean.csv](./FinalData/df_chart_norating_clean.csv).  Data on word match frequencies. The `_clean` version simply renames columns for Datawrapper.  The figure in the write up uses these data.

- [df_chart_rating.csv](./FinalData/df_chart_rating.csv) and [df_chart_rating_clean.csv](./FinalData/df_chart_rating_clean.csv).  Data on word match frequencies. The _clean version simply renames columns for Datawrapper.  These data contain additional information on word matches by route difficulty.  Not used in the main write up.  

- [df_map.csv](./FinalData/df_map.csv).  A list of route names with terms matching a narrower list of offensive terms, as well as their longitude and latitude.  In the code this list is based on `has_fB==1`.  






