---
layout : post
title : Building Camunda Platform from source code on Windows
date : 2015-09-04 19:10
---
**Camunda** is an open source platform for workflow and business process automation. Camunda is lightweight,embeddable,supports many different application servers with well defined API. Since its 
quite popular we decided to explore features offered by this product. The best way to explore an open source product would be to build the binaries from its source code.

####Camunda Source Code 

Camunda source code is hosted on github and located at

{% highlight ruby %}
https://github.com/camunda/camunda-bpm-platform.git
{% endhighlight %}

In order to build the source one must first clone the repository on your local machine. Use the following command to clone the camunda platform repository

**Note:** You must have git  installed on your machine



{% highlight ruby %}
git clone https://github.com/camunda/camunda-bpm-platform.git
{% endhighlight %}

#### Prerequiste for building
> - JDK 6 or 7
> - Apache Maven 3


####Installing JDK
Install JDK before you install maven. You can use either use Oracle JDK or Open JDK version 6 or 7. However OpenJDK is only available for Linux platforms
{% highlight ruby %}
Oracle JDK Download link
http://www.oracle.com/technetwork/java/javase/archive-139210.html
{% endhighlight %}


####Installing Maven
We used maven 3.3.3 which requires JDK 1.7. You can download the latest maven binaries from 
{% highlight ruby %}
https://maven.apache.org/download.cgi
{% endhighlight %}

Choose the archive which is most appropriate for your platform. For windows, its best to choose the zip binaries. The installation instructions for maven can be found at

{% highlight ruby%}
https://maven.apache.org/install.html
{% endhighlight%}

Verify the maven installation using

{% highlight ruby%}
mvn -v
{% endhighlight%}

The output should look something similar

{% highlight ruby%}
Apache Maven 3.3.3 (7994120775791599e205a5524ec3e0dfe41d4a06; 2015-04-22T21:57:3
7+10:00)
Maven home: E:\Program Files\Apache Software Foundation\maven\apache-maven-3.3.3
\bin\..
Java version: 1.7.0_45, vendor: Oracle Corporation
Java home: E:\Program Files\Java\jdk1.7.0_45\jre
Default locale: en_IN, platform encoding: Cp1252
OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"
{% endhighlight%}

####Configure Maven

We need to add camunda public nexus repository to your maven `settings.xml`. The `settings.xml` can be found inside the `MAVEN_INSTALL_DIR/conf`. Add the following lines to it

{% highlight ruby%}
<profiles>
  <profile>
    <id>camunda-bpm</id>
    <repositories>
      <repository>
        <id>camunda-bpm-nexus</id>
        <name>camunda-bpm-nexus</name>
        <releases>
          <enabled>true</enabled>
        </releases>
        <snapshots>
          <enabled>true</enabled>
        </snapshots>
        <url>https://app.camunda.com/nexus/content/groups/public</url>
      </repository>
    </repositories>
  </profile>
</profiles>
<activeProfiles>
  <activeProfile>camunda-bpm</activeProfile>
</activeProfiles>
{% endhighlight%}

####Building Source Code

Now we are ready to build the camunda platform code. Open the command prompt and navigate to the directory where the camunda platform code is checkedout. Build the source code using
{% highlight ruby%}
mvn clean install
{% endhighlight%}

This will compile the platform source code,run the unit as well as the integration test cases. It will also build distribution for each application server. After the build is complete, the distribution can be found under

{% highlight ruby%}
distro/tomcat/distro/target     (Apache Tomcat 7 Distribution)
distro/gf31/distro/target       (Glassfish 3 Distribution)
distro/jbossas7/distro/target   (JBoss AS 7 Distribution)
{% endhighlight%}

**Note:** The build will take some time to complete and it took around 2 hours on my machine.


####Next Steps
In the next blog, we are going to see how to start the camunda server using one of the distributions built from the source and then how to develop a sample application using camunda.



