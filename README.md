# ApacheNutch-ApacheSolr-Configuration

# Overview

Search Engines are one of the most useful feature an application can offer to it's user. Search
Engines have all the information particularly about the subject that you are trying to search for.
Some famous Search Engines are Google, Bing, Yahoo and there may be many many more in the
present and in the future. However, the easy it looks to search something useful from a Search
Engine provided by any application. The tricky and I would say not really easy it is to develop one.
In this document we will talk about How we developed a Search Engine particularly aiming to the
medical site for our application, Moreover, this document will also explain about the technologies
we use, How we gather configure and install different technologies, and what are the steps we use
to successfully communicate the data from one place to another.
Following is the brief description of technologies that we used for Search Engine.
* Apache Nutch: Apache Nutch is said to be one of the powerful and highly extensible and
scalable open source web crawler software project, coded in JAVA. It is originated with Doug
Cutting, creator of both Lucene and Hadoop. It has highly modular architecture, which
allows developers to create plug-ins and crawl the data from different websites they want to.
APache Nutch got famous in June 2003, after a successfull 100 million page demonstration
system was developer.
* Apache Solr: Solr is an open-source enterprise-search platform, written in Java, from the
Apache Lucene project. Its major features include full-text search, hit highlighting, faceted
search, real-time indexing, dynamic clustering, database integration, NoSQL features and
rich document handling.
* Azure Cloud Services: The Azure Cloud services are use to deploy Apache Solr on a VM
to communicate with the application live.
* .NetCore: .NetCore language is used for the communication and the development of the
middleware as well as api response fetching.


# Prerequisites
As of the usage of different technologies for different kinds of solutions. Apache Nutch has some
prerequisites to be worked easily and successfully. These are as follows.
* Unix environment, or Windows-Cygwin environment.
* Java Runtime/Development Environment (JDK 1.8 / Java 8)
* (Source build only) Apache Ant: https://ant.apache.org/
As discussed above, Apache Solr was used on Azure VM provided by bitnami. The link to the
particular Azure VM is given below.
* https://bitnami.com/stack/solr/cloud/azure
Or you can just create your own from your Azure Portal.
* Go to "Create Resource"
* Search For "Apache Solr Certified by Bitnami"
* Install
