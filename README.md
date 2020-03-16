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


# Problem Statement
The Problem Statement is explained below with the each step.
Below are some key steps of the problem statement:
* Crawl 1000's of pages from the internet.
* Save the crawled data in a database.
* Index the crawled data for usage with application.
* Develop a middleware to communicate between .netcore application and crawled data.
* Fetch the data and show the response.



# Installing and Configuring Apache Nutch
listings Apache Nutch Installation and configuration In this section, the key steps of Apache
Nutch up and running are explained. How to successfully run Apache Nutch and crawled the data
from the sites mentioned by the developer is also explained.
Some of the dependencies are as follows.
* Apache Nutch 2.2.3
* HBase 0.94.0
* Ant
* JDK 8
The key steps are as follows.
* Install Apache Nutch 2.2.3 from http://nutch.apache.org/downloads.html.
* Extract Apache Nutch in the folder of your choice forexample (Nutch/apachenutch2.2.3).
* Install and extract HBase from http://archive.apache.org/dist/hbase/hbase-0.90.4/.
* Now in Nutch Folder we have HBase0.94 and apachenutch2.2.3.
* Go to HBase0.94/conf folder and open hbase-site.xml file.
* Copy and paste the following code in hbase-site.xml

```
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
<property>
<name>hbase.rootdir</name>
<value><Your path></value>
<! You need to create one directory and assign a path up to that directory. That directory will be <property>
<name>hbase.zookeeper.property.dataDir</name>
<value><Your path></value>
<! You need to create one directory and assign a path up to that directory. That directory will be </property>
</configuration>
```

* Specify Gora Properties. Go to apachenutch2.2.3/conf Folder and open nutch-site.xml.

* Copy and paster the following piece of code in nutch-site.xml file.
```
<property>
<name>storage.data.store.class</name>
<value>org.apache.gora.hbase.store.HBaseStore</value>
<description>Default class for storing data</description>
</property>
```
* Make sure HBasegora properties are also available in ivy.xml file. Located in apachenutch2.2.3/ivy/ivy.xml file.
```
<!-- Uncomment this to use HBase as Gora backend. -->
<dependency org="org.apache.gora" name="gora-hbase" rev="0.2" conf="*-
>default" />
```
* Go to apachenutch2.2.3/conf and open the file gora.properties.
* Copy and paste the following line of code in it.
gora.datastore.default=org.apache.gora.hbase.store.HBaseStore
* Now go to apachenutch2.2.3 Folder and open your terminal in the particular directory. Run
Command "ant runtime".
* Runing the above command with create the respective directory named as "runtime" in the
apachenutch2.2.3 Folder. The structure of apachenutch2.2.3 will look like the following image
below.


- Apache-nutch-2.2.3
  -  build
  -  conf
  -  docs
  -  ivy
  -  lib
  -  runtime
  -  src


Lets Go to HBase directory and check HBase is working fine.
* Go to Hbase0.94 directory and run the following command.
```./bin/hbase shell```
* If everything goes well. You may see the following output.
```HBase Shell; enter 'help<RETURN>' for list of supported commands. Type "exit<RETURN>" ```
```to leave the HBase Shell Version: 0.90.4, r1001068, Fri Sep 24 13:55:42 PDT 2010```

* This Completes your installation of Apache Nutch and integrating HBase. For more details
about all the logs please refer to apachenutch2.2.3/runtime/local/logs/hadoop.log.



# Verifying Your Apache Nutch Installation
* Go to apachenutch2.2.3/runtime/local folder and run the following command. bin/nutch
* If everything is successful, you shall see the following output.
```
Usage: nutch COMMAND
..
..
..

Most commands will print help when invoked w/o parameters.
```
* If the permission is denied run the following command chmod +x bin/nutch
* You may also see an error that can occur at any step stating that "JAVA Home is
not set".
* Set JAVA HOME with the following commands.
```sudo nano /.bashrc.```
* In the file put the following piece of line.
  ```export JAVA HOME=Your Java path```
  
 
 # Crawling Your First Website/ No. Of Websites
* Go to apachenutch2.2.3/runtime/local/conf Folder and open the file nutch-site.xml.
* Copy the following piece of code in it.
```
<configuration>
<property>
<name>http.agent.name</name>
<value>My Nutch Spider</value>
</property>
</configuration>
```
* Now go to apachenutch2.2.3/runtime/local Folder and make another Folder. Name the Folder as "urls".
* In Folder urls make a file and named it as "seed.txt".
* In seed.txt file provide the urls that you want to crawl. Forexample https://www.apple.com/. Save
the file and close it.
* Now go back to Folder apachenutch2.2.3/runtime/local and run the following commands.
* ``` bin/nutch inject urls```
* ```bin/nutch generate -topN 100.``` 
# (Note: You can mention your own number while generating to tell the apache nutch that How many linked urls should it generate from the given sites.)
* ```bin/nutch fetch -all.```
* ```bin/nutch parse -all```
* ```bin/nutch updatedb -all```
* ```bin/nutch solrindex http://azureipaddress:8983/solr/nutch -all``` 
# Note: Run this command after deployment of Apache Solr.

After every step you will see the successfull output. Otherwise check hadoop.log file mentioned above.
