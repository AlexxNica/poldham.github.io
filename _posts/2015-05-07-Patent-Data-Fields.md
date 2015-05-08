---
title: "Understanding Patent Documents and Data Fields"
author: "Paul Oldham"
date: "23 March 2015"
layout: post
published: yes
---

This article provides a walkthrough of patent data fields for those who are completely new to patent analytics or want to understand the workings of patent data a little bit better. A video version of the walkthrough is available [here](https://youtu.be/RDPlIUB0_QE?list=PLsZOGmKUMi56dAuqSEHjVWkxEf3MbXlQG) and the slide deck is available for download in [.pdf](https://github.com/poldham/opensource-patent-analytics/raw/master/C_obtaining_patent_data/understanding_data_fields/patent_data_fields_OM.pdf), [powerpoint](https://github.com/poldham/opensource-patent-analytics/raw/master/C_obtaining_patent_data/understanding_data_fields/patent_data_fields_OM.pptx) and apple keynote(https://github.com/poldham/opensource-patent-analytics/raw/master/C_obtaining_patent_data/understanding_data_fields/patent_data_fields_OM.key) from [GitHub](https://github.com/poldham/opensource-patent-analytics/tree/master/C_obtaining_patent_data/understanding_data_fields.

###What is a Patent?

A patent can be described in two main ways:

1. As a particular form of intellectual property right.
2. As a type of document.

Understanding the structure of patent documents and data fields is the essential foundation of patent analytics. However, for those who are new to the patent system it is worth highlighting the key features of patents as a form of intellectual property right. 

###As a form of intellectual property right
1. A patent is a temporary grant of an exclusive right to a patentee to prevent others from making, using, offering for sale, or importing, a patented invention without their consent, in a country where a patent is in force.
2. Patent rights are territorial rights - they are only valid in the territory of the country where granted. 
3. Patents are typically granted for a period of 20 years from the filing data of an application but may be opposed or revoked.
5. To be eligible a claimed invention must:
    + Involve patentable subject matter
    + Be new or novel
    + Involve an inventive step
    + Be susceptible to industrial application or useful.

###Patents as a type of document
For patent analytics we need to concentrate on patents as a form of document and to understand:

1. The structure of patent documents and their data fields.
2. The strengths and limitations of different patent databases as a means for obtaining patent data. 

In this article we deal with the basics of patent documents and their data fields. 

###Basic Data Types

When performing patent analysis we are dealing with data of seven different types:

- **Dates** (priority, application and publication dates)
- **Numbers** (priority number, application number, publication number, family members, citations)
- **Names** (Applicants - also known as Assignees - and Inventors)
- **Classification codes** (e.g. International Patent Classification/Cooperative Patent Classification)
- **Text fields** (Title, Abstract, Description, Claims, Sequence data)
- **Images** (Diagrams)
- **Additional Information** (Legal Status, Public Registry etc)

We will walk through each of these fields using a patent application for synthetic genomes from the J. Craig Venter Institute as an example. 

###Synthetic Genomes: [Nature News](http://www.nature.com/nature/journal/v473/n7347/full/473403a.html)

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_nature_news.png)

###Synthetic Genomes: [Original Front Page](http://worldwide.espacenet.com/publicationDetails/originalDocument?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

original front page here

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_frontpage_WO.png)

###Database: [Front Page](http://worldwide.espacenet.com/publicationDetails/biblio?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

database front page here

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_WO.png)

###Synthetic Genomes: [Description](http://worldwide.espacenet.com/publicationDetails/description;jsessionid=2kCKJqOvMF0Te-kUiu5GaPA9.espacenet_levelx_prod_2?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

Description

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_description.png)

###Synthetic Genomes: [Claims](http://worldwide.espacenet.com/publicationDetails/claims?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

Claims
![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_claims.png)


###Synthetic Genomes: [Family Members](http://worldwide.espacenet.com/publicationDetails/inpadocPatentFamily?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

Family Members

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_WO_family.png)

###Synthetic Genomes: [Cited](http://worldwide.espacenet.com/publicationDetails/citedDocuments?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

Cited documents

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_WO_cited.png)

###Synthetic Genomes: [Citing](http://worldwide.espacenet.com/publicationDetails/citingDocuments?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_WO_citing.png)

Citing Documents

###Synthetic Genomes: [Legal Status](http://worldwide.espacenet.com/publicationDetails/inpadoc?CC=WO&NR=2008024129A2&KC=A2&FT=D&ND=5&date=20080228&DB=EPODOC&locale=en_EP)

Legal Status

![_config.yml]({{ site.baseurl }}/images/datafields/synthetic_genomes_WO_legalstatus.png)

###Round Up

In this article we have walked through some of the most important patent data fields. 

These fields are the building blocks for sophisticated patent analysis. In future sessions we will focus on:

- Retrieving data with these fields
- Cleaning up the data in these fields
- Mapping Trends
- Network Mapping
- Geographic Mapping

###Learn More

- Visit the [Github project page](http://poldham.github.io/opensource-patent-analytics/)
- Access materials in the repository directly and add your own [here](https://github.com/poldham/opensource-patent-analytics)