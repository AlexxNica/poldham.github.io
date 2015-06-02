---
title: "Cleaning Patent Data with Open Refine"
author: "Paul Oldham"
date: "1 June 2015"
layout: post
published: true
---

Cleaning patent data is one of the most challenging and time consuming tasks involved in patent analysis. In this article we will cover. 

1. Basic data cleaning using Open Refine
2. Separating a patent dataset on applicant names and cleaning the names.
3. Exporting a dataset from Open Refine at different stages in the cleaning process.

[Open Refine](http://openrefine.org) is an open source tool for working with all types of messy data. It started life as Google Refine but has since migrated to Open Refine. It is a programme that runs in a browser on your computer but does not require an internet connection. It is a key tool in the open source patent analysis toolkit and is very sophisticated including extensions and the use of custom code for particular custom tasks. In this article we will cover some of the basics that are most relevant to patent analysis and then move on to more detailed work to clean patent applicant names. 

The reason that patent analysts should use Open Refine is that it is the easiest to use and most efficient free tool for cleaning and reshaping or wrangling patent data. It is far superior to attempting the same cleaning tasks in Excel or Open Office. The terminology that is used can take some getting used to, but it is possible to develop efficient workflows for cleaning and reshaping data using Open Refine and to create and reuse custom codes needed for specific tasks. 

In this article we use Open Refine to clean up a raw dataset from WIPO Patentscope containing nearly 10,000 raw records that make some kind of reference to the word `pizza` in the whole text. To follow this article using one of our training sets, download it from [here](https://github.com/poldham/opensource-patent-analytics/blob/master/2_datasets/pizza_medium/pizza_medium.csv?raw=true) or use your own dataset. 

##Install Open Refine

To install Open Refine visit the Open Refine [website](http://openrefine.org) and [download](http://openrefine.org/download.html) the software for your operating system:

![_config.yml]({{ site.baseurl }} /images/openrefine/OpenRefine-2015-06-01\ 12-18-34.png)

From the download page select your operating system. Note the extensions towards the bottom of the page for future reference. 

![_config.yml]({{ site.baseurl }} /images/openrefine/OpenRefine-download.png)

When you download Open Refine at the time of writing it actually downloads and installs as Google Refine (reflecting its history) and so that is the application you will need to look for and open. 

##Create a Project

We will use the Patentscope Pizza Medium file that can be downloaded from the repository [here](https://github.com/poldham/opensource-patent-analytics/blob/master/2_datasets/pizza_medium/pizza_medium.csv?raw=true).

![_config.yml]({{ site.baseurl }} /images/openrefine/create_project.png)

The file will load and then attempt to guess the column separator. Choose `.csv.` Note that a wide range of files can be imported and that there are additional options such as storing blank cells as nulls that are selected by default. 

![_config.yml]({{ site.baseurl }} /images/openrefine/create_project2.png)

Click `create project` in the top right of the bar as the next step.

##Open Refine Basics

A few basic features of Open Refine will soon have you working smoothly. Here is a quick tour. 

###1. Open Refine runs in a broswer but lives on your computer

Open Refine is a computer application that lives on your computer but runs in a browser. It does not require an internet connection and it does not lose your work if you close the browser. 

###2. Open Refine works on columns. 

At the top of each column is a pull down menu. Be ready to use these menus quite a lot. In particular, you will often use the `Edit cells > Common tranforms` as shown below for functions such as trimming whitespace.

![_config.yml]({{ site.baseurl }} /images/openrefine/menu_basics.png)

Other important menus are `Edit column` for splitting columns into new columns. 

###3. Open Refine works with Facets. 

This terminology may initially be confusing but basically calls up a window that arranges the items in a column for inspection, sorting, and editing as we can see below. This is important because it becomes possible to identify problems and address them. It also becomes possible to apply a variety of clustering algorithms to clean up the data.

![_config.yml]({{ site.baseurl }} /images/openrefine/facet_menu.png)

Hovering over an item allows it to be edited, such as removing <i> and </i> from the title.

###4. Custom Facets

The Facet menu below brings up a custom menu that allows for the use of code in [Open Refine Expression Language (GREL)](https://github.com/OpenRefine/OpenRefine/wiki/GREL-Functions) to perform tasks not covered by the main menu items. This language is quite simple and can range from short snippets for finding and replacing text to more complex functions that can be reused in future.  

![_config.yml]({{ site.baseurl }} /images/openrefine/facet_menu.png)

###5. Reordering Columns

Where we have a large number of columns we may want to change the order to bring a working column to the front of the set. To do that select the `All` drop down menu in the first column and then `Edit columns > Re-order/remove columns`. In the pop up menu of fields drag the desired field to the top of the list. In this case we have dragged the priority_date column to the top of the list. It will now appear as the first data column. 

![_config.yml]({{ site.baseurl }} /images/openrefine/reorder_columns.png)

###6. Undo and Redo

Open Refine keeps track of each action and allows you to go back several steps or to the beginning. This is particularly helpful when testing whether a particular approach to cleaning (e.g. splitting columns or using a snippet of code) will meet your needs. In particular it means you can explore and test approaches while not worrying about losing your previous work. 

![_config.yml]({{ site.baseurl }} /images/openrefine/undo_redo.png)

###7. Exporting 

When a clean up exercise is completed a file can be exported in a variety for formats. When working with patent data expect to create more than one file (e.g. core, applicants, inventors, IPC) to allow for analysis of aspects of the data in other tools. In this article we will create two files. 

1. A cleaned version of the original data
2. An applicants file that separates the data by each applicant. 

##Basic Data Cleaning in Open Refine

This is the first step in working with a dataset and it will make sense to perform some basic cleaning tasks before going any further. The Pizza Medium dataset that we are working with in this article is raw in the sense that the only cleaning so far has been to remove the two empty rows at the head of the data table and to fill blank cells with NA values. The reason that it makes sense to do some basic cleaning before working with applicant, inventor or IPC data is that new datasets will be generated by this process. 

Bear in mind that Open Refine is not the fastest programme and make sure that you allocate sufficient time for the clean up tasks and are prepared to be patient while the programme runs algorithms to process the data. Note that Open Refine will save your work and you can return to it later. 

When working with Open Refine we will typically be working on one column at a time. However, the key `checklist` for cleaning steps is: 

1. Make sure you have a back up of the original file. Creating a `.zip` file and marking it with the name `raw` can help to preserve the original. 
2. Open and save a text file as a `code book` to write down the steps taken in cleaning the data (e.g. pizza_codebook.txt). 
3. Regularise characters (e.g. title, lowercase, uppercase).
4. Remove leading and trailing whitespace.
5. Address encoding problems.

Additional actions:

6. Transform dates
7. Access additional information and create new columns and/or rows.

We will generally approach these tasks in each column and steps 6 and 7 will not always apply. The creation of a codebook will allow you to keep a note of all the steps taken to clean up a dataset. The codebook should be saved with the cleaned dataset (e.g. in the same folder) as a reference point if you need to do further work or if colleagues want to understand the transformation steps.

###1. Changing case

The first column in our dataset is the publication number. To inspect what is happening and needs to be cleaned in this column we will first select the column menu and choose `text facet` from the dropdown. This will generate the side menu panel that we can see below containing the data. We can then inspect the column for problems. 

![_config.yml]({{ site.baseurl }} /images/openrefine/cleaning_pubno_createfacet.png)

When we scroll down the side panel we can see that some publication numbers have a lowercase country code (in this case `ea` rather than `EA` for Eurasian Patent Organization using the [WIPO country codes](http://www.wipo.int/pct/guide/en/gdvol1/annexes/annexk/ax_k.pdf)). To address this we select the column menu `Edit cells > Common transforms > to Uppercase`.

![_config.yml]({{ site.baseurl }} /images/openrefine/cleaning_pubno_totitlecase.png)

If we scroll down all the publication numbers will have been converted to upper case. This will make it easier to extract the publication country codes at a later stage. 

###2. Regularise case

For the other text columns it is sensible to repeat the common transformations step and select `to titlecase`. Note that this will generally work well for the title field but may not always work as well on concatenated fields such as applicants and inventor names. Repeat this step following the separation of these concatenated fields (see below on applicants). If the abstract or claims were present we would not regularise those text fields. 

###3. Remove leading and trailing whitespace

To remove leading and trailing white space in a column we select `Edit cells > Common transforms > Trim` leading and trailing whitespace across the columns. 

![_config.yml]({{ site.baseurl }} /images/openrefine/title_trailingwhitespace.png)

Note that following the splitting of concatenated cells with multiple entries such as the applicants and the inventors fields it is generally a good idea to repeat the trim exercise when the process is complete to avoid potential leading white space at the start of the new name entries. 

###4. Add Columns

We can also add columns by selecting the column menu and  `Edit Column > Add column based on this column`. In this case we have added a column called publication_year. 

![_config.yml]({{ site.baseurl }} /images/openrefine/add_column_publicationyear.png)

We have a number of options with respect to dates (see below). In this case we want to separate out the date information into separate columns. To do that we can use `Edit column > Split into several columns`. We can also choose the separator for the split, in this case `.` and whether to keep or delete the source column. In this case we selected to retain the original column and created three new date related columns. We could as necessary then delete the date and month column if we only needed the year field. 

![_config.yml]({{ site.baseurl }} /images/openrefine/split_date.png)

We can then rename these columns using the edit `Edit Column > Rename this column`. Note that in this case the use of lowercase and underscores marks out columns we are creating or editing as a flag for internal use informing us that this is not original. 

![_config.yml]({{ site.baseurl }} /images/openrefine/rename_column.png)

###5. Reformatting dates

One problem we may encounter is that the standard date definition on patent documents (e.g. 21.08.2009) is not recognised as a date field in our analysis software because. We might anticipate this and transform the data into another form such as 21/08/2009. A very simple way to do this is by using a replace function. In this case we select the menu for the publication_date field and then `Edit cells > Transform`. 

![_config.yml]({{ site.baseurl }} /images/openrefine/transform.png)

This produces a menu where we enter a simple GREL replace code. 

![_config.yml]({{ site.baseurl }} /images/openrefine/transform_replace_date.png)


{% highlight r %}
replace(value, '.', '/')
{% endhighlight %}

This simple replace code is basically the same as find and replace in Excel or Open Office. In addition, we can see the consequences of the choice in the panel before we run the command. This is extremely useful for spotting problems. For example, if attempting to split a field on a comma we may discover that there are multiple commas in a cell. By testing the code in the panel we could then work to find a solution or edit the offending texts in the main facet panel. 

To find other simple codes visit the [Open Refine Recipes page](https://github.com/OpenRefine/OpenRefine/wiki/Recipes).

We will now focus on extracting information from some of the columns before saving the dataset and moving on. 

##Extracting the Publication Country

The Patentscope data does not contain a publication country field. Note here that Patentscope merges all publications for an application record into one dossier accessible through the Documents section on the website. However, we could access this information from the front of the publication number
in the Patentscope records using a very simple code and create a new column (as above) based on the values returned as below.

![_config.yml]({{ site.baseurl }} /images/openrefine/publication_country.png)


{% highlight r %}
substring(value, 0, 2)
{% endhighlight %}

Note here that the code begins counting from 0 (e.g. 0, 1 = U, 2 = S). The first part of the code looks in the value field. 0 tells the code to begin counting from 0 and the 2 tells it to read the two characters from 0. We could change these values, e.g to 1 and 4 to capture only the chunk of a number. 

##Fill blank cells

Filling blank cells with a value (NA for Not Available) to prevent calculation problems with analysis tools later can be performed by selecting each column, creating a text facet and choosing blank and then entering NA for the value. 

![_config.yml]({{ site.baseurl }} /images/openrefine/blank_na_facets.png)

Note that this is somewhat time consuming (until a more rapid method is found) but has the benefit of being accurate. It may prove faster to open the resulting data file in Excel (or Open Office) and using find and replace with the find box left blank and NA in the replace field across the data table.  

##Rename the columns

At this stage we have a set of columns that are mixed between the original sentence case and the additions in lower case with no spaces such as `publication_number`. This is a matter of person preference but it is generally a good idea to regularise the case of all columns to make them easy to remember. In this case we will also add the word `original` to the columns to distinguish between those created by cleaning the data and those we have created.  

##Exporting the Data

When we are happy that we have worked through the core cleaning steps and filled blank cells with NA values we are in a position to export the dataset. It is important to do this before the steps described below because it preserves a copy of the core dataset that can be used for separation (or splitting activities) on applicants, inventors, IPC etc. during the next steps. It is important that this `clean` dataset is as clean as is reasonably possible before moving on. The reason for this is that ***any noise or problems will multiply*** when we move on to the next steps. This may require a restart of the cleaning steps on later files for applicants or inventors. Therefore make sure that you are happy that the data is as clean as is reasonably possible at this stage. Then choose export from the menu and the desired format (preferably `.csv` or `.tab` if using analytics tools later). 

![_config.yml]({{ site.baseurl }} /images/openrefine/export_core.png)

##Splitting Applicants

This article was inspired by a [very useful tutorial](http://www.patinformatics.com/blog/patent-assignee-cleanup-using-google-refine-open-refine-text-facets-and-clustering/) on cleaning assignee names with Google Refine by Anthony Trippe. Anthony is also the author of the forthcoming WIPO Guidelines on Patent Landscapes and the [Patentinformatics LLC](http://www.patinformatics.com) website has played a pioneering role in promoting patent analytics. We will take example forward using the pizza dataset of nearly 10,000 to create a file that can be used to visualise applicants using the term `pizza` in a range of tools such as Tableau Public. If you have not done so already, you can download that dataset [here](https://github.com/poldham/opensource-patent-analytics/blob/master/2_datasets/pizza_medium/pizza_medium.csv?raw=true).  

We actually have two options here and we will go through them so that you can work out your needs in a particular situation. Note that you can use Undo in Google Refine to go back to the point before testing these approaches. However, if you have followed the data cleaning steps above, make sure that you have also saved a copy of your dataset. 

###Situation 1 - First Applicants

As discussed by Anthony Tripp we could split the applicant column into separate columns by choosing, `Applicants > Edit column > Split into several columns`. 

![_config.yml]({{ site.baseurl }} /images/openrefine/split_applicants_columns.png)

We then need to select the separator. In this case (and normally with patent data), it is `;`. 

![_config.yml]({{ site.baseurl }} /images/openrefine/split_selectseparator.png)

This will produce a set of 18 columns.

![_config.yml]({{ site.baseurl }} /images/openrefine/split_columns.png)

At this point, we could begin the clustering process to start cleaning the names that is discussed in situation 2. However, the disadvantage with this is that with this size of dataset we would need to do this 18 times in the absence of an easy way of combining the columns into a single column (applicants) with a name on each row. We might want to use this approach in circumstances where we were not focusing on the applicants and were happy to accept the first name in the list as the first applicant. In that case we would simply be reducing the applicant field to one applicant. Bear in mind that the first applicant listed in the series of names may not always be the first applicant as listed on an application and may not be an organisation name. Bearing these caveats in mind, we might also use this approach to reduce the concatenated inventors field to one inventor. For general purposes that would be much cleaner. 

However, if we wanted to perform detailed applicant analysis for an area of technology, we would need to adopt a different approach. 

###Situation 2 - All Applicants

One of the real strengths of Open Refine is that it is very very easy to separate applicant and inventor names into individual rows. Instead of choosing Edit column we now choose `Edit cells` and then `split multi-valued cells`. 

![_config.yml]({{ site.baseurl }} /images/openrefine/split_multivaluedcells.png)

In the pop up menu choose `;` as the separator rather than the default comma. 

We now have a dataset with 15,884 rows as we can see below. 

![_config.yml]({{ site.baseurl }} /images/openrefine/split_multivaluedcells2.png)

The advantage of this is that all our individual applicant names are now in a single column. However, note that the rest of the data has not been copied to the new rows. We will come back to this but as a precaution it is sensible to fill down on the publication number column as the key that links the individual applicants to the record. So let's do that for peace of mind by selecting `publication number > edit cells > fill down`. 

![_config.yml]({{ site.baseurl }} /images/openrefine/split_filldown.png)

We should now have a column filled with the publication number values for each applicant as our key. 

If you have not already done so above to assist the clean up process, and as general good practice, transform the mixed case in the applicants field to a single case type. To do that select `Applicants > Edit Cells > Common Transformations > To titlecase`.

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_titlecase.png)

We now move back to the applicants and select `Facet > Text Facet`.

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_textfacet.png)

What we will see (with Applicants moved to the first column by selecting `Applicants > Edit Column > Move column to beginning`) is a new side window with 9,368 choices. 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants1.png)

The cluster button will trigger a set of six clean up algorithms with user choices along the way. It is well worth reading the [documentation](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth) on these steps to decide what will best fit your needs in future. These cleaning steps proceed from the strict to the lax in terms of matching criteria. The following is a brief summary of the details provided in the documentation page:

1. Fingerprinting. This method is the least likely in the set to produce false positives (and that is particularly important for East Asian names in patent data). It involves a series of steps including removing trailing whitespace, using all lowercase, removing punctuation and control characters, splitting into tokens on white space, splitting and joining and normalising to ASCII. 
2. N-Gram Fingerprint. This is similar but uses n-grams (a sequence of characters or multiple sequences of characters) that are chunked, sorted and rejoined and normalised to ASCII text. The documentation highlights that this can produce more false positives but is food for finding clusters missed by fingerprinting. 
3. Phonetic Fingerprint. This transforms tokens into the way they are pronounced and produces different fingerprints to methods 2 & 3. 
4. Nearest Neighbour Methods. This is a distance method but can be very very slow. 
5. Levenshtein Distance. This famous algorithm measures the minimal number of edits that are required to change one string into another (and for this reason is widely known as edit distance). Typically, this will spot typological and spelling errors not spotted by the earlier approaches. 
6. PPM a particular use of Kolmogorov complexity as described in this [article](http://arxiv.org/abs/cs/0111054) that is implemented in Open Refine as `Prediction by Partial Matching`. 

It is important to gain an insight into these methods because they may affect the results you receive. In particular, caution is required on East Asian names where cultural traditions produce lots false positive matches on the same name for persons who are actually distinct (synonyms or "lumping" in the literature) that can have dramatic impacts on the results of patent analysis for inventor names. 

We will now walk through each algorithm to view the results. 

![_config.yml]({{ site.baseurl }} /images/openrefine/cluster_step1.png)

This identifies 1187 clusters dominated by hidden characters in the applicants field (typically appearing after the name). At this stage we need to make some decisions about whether or not to accept or reject the proposed merger by checking the `Merge?` boxes. 

This step was particularly good at producing a match on variant names and name reversals as we can see here. 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants2.png)

It pays to manually inspect the data before accepting it. One important option here is to use the slider on `Choices in Cluster` to move the range up or down and then make a decision about the appropriate cut off point. Then use select all in the bottom left for results you are happy with followed by `Merge Selected & Re-Cluster`. In the next step we can change the keying function dropdown to Ngram-fingerprint. 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants-ngramfingerprint2.png)

This produces 98 clusters which inspection suggests are very accurate. The issues to watch out for here (and throughout) are very similar names that may not be the same company (such as Ltd. and Inc.) or distinct divisions of the same company. It is also important, when working with inventor names, not to assume that the same name is the same inventor in the absence of other match criteria, or that apparently minor variations in initials (e.g. Smith, John A and Smith, John B) are the same person because they may not be. 

To see these potential problems in action try reducing the N-gram size to 1. At this point we see the following. 

![_config.yml]({{ site.baseurl }} /images/openrefine/ngram1_problems.png)

This measure is too lax and is grouping together companies that should not be grouped. In contrast increasing the N-gram value to 3 or 4 will tighten the cluster. We will select all on N-gram 2 and proceed to the next step. 

At this point it is worth noting that the original 9,368 clusters have been reduced to 7,875 and if we sort on the count in the main window then Google is starting to emerge as the top applicant. 

###Phonetic Fingerprint (Metaphone 3) clustering 

As we can see below, Metaphone 3 clustering produces 413 looser clusters with false positive matches in International Business Machines but positive matches on Cooperative Verkoop. 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_metaphone3.png)

At this point we could either manually review the 413 clusters and select as appropriate or change the settings to reduce the number of clusters using the `Choices in Clusters` until we see something manageable for manual review. At this stage we might also want to use the `browse` cluster function that appears on hovering over a particular selection, to review the data.

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_browsecluster.png)

In this case we are attempting to ascertain whether the Korea Institute of Oriental Medicine should be grouped with the Korea Institute of Science and Technology (which appears unlikely). If we open the browser function we can review the entries for shared characteristics as possible match criteria. 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_browsecluster1.png)

For example, if the applicants shared inventors and/or the same title we may want to record this record in the larger grouping (remembering that we have preserved the original data). Or, as is more likely, we might want to capture most members of the group and remove the Korea Institute of Oriental Medicine. However, how to do this is not at all obvious. 

In practice, selection of items at this stage feeds into the next stage of cleaning using the Cologne-phonetic algorithm. As we can see below, this algorithm identified 271 clusters that were almost entirely clustered on the names of individuals with a limited number of accurate hits. 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_cologne.png)

###Levenshtein Edit Distance

The final steps in the process focus on Nearest Neighbour matches for our reduced number of clusters. Note that this may take some time to run (e.g. 10-15 minutes for the +7,000 clusters in this case). The results are displayed below 

![_config.yml]({{ site.baseurl }} /images/openrefine/applicants_levenshtein.png)

In some cases the default settings matched individual names on different initials, but in the majority of cases the clusters appeared valid and were accepted. In this case particular caution is required on the names of individuals and browsing the results to check the accuracy of matches. 

###PPM

The PPM step is the final logarithm but took so long that we decided to abandon it relative to the likely gains. 

###Preparing data for export

In practice, the cleaning process will generate a new data table for export that focuses on the characteristics of applicants. To prepare for export with the cleaned group of applicant names there will be a choice on whether to retain the publication number as the single key, or, whether to use the fill down process illustrated above across the columns of the dataset. It is important to note that caution is required in the blanket use of fill down. 

It is also important to bear in mind that the dataset that has been created contains many more rows than the original version. Prior to exporting we would therefore suggest two steps:

1. Rerun Common transforms > to title case, to regularise any names that may have been omitted in the first round. 
2. Rerun facets on each column, select blank at the end of the facet panel and fill with NA. Alternatively, do this immediately following export. 

##Round Up

In this article we have covered the main features of basic data cleaning using Open Refine. As should now be clear, while it requires an investment in familiarisation it is a powerful tool for cleaning up small to medium sized patent datasets such as our 10,000 pizza patent records. However, a degree of patience, caution and forward planning is required to create an effective workflow using this tool. It is likely that further investments of time (such as the use of regular expressions in GREL) would improve cleaning tasks prior to analysis. 

Open Refine is also probably the easiest to use free tool for separating and cleaning applicant and inventor names without programming knowledge. For that reason alone, while noting the caveats highlighted above, Open Refine is a very valuable tool in the open source patent analytics toolbox. 

## Useful Resources

The [Open Refine website](http://openrefine.org) has links to lots of useful resources including video walkthroughs

[Open Refine Wiki Recipes](https://github.com/OpenRefine/OpenRefine/wiki/Recipes)

[Open Refine Tips and Tricks](http://googlerefine.blogspot.co.uk)


