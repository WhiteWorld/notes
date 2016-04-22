# Hadoop Install

http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SingleCluster.html

### Required software

1. Java 版本
2. SSH

    $ ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
    $ cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
    
### Download a Hadoop distribution

To get a Hadoop distribution, download a recent stable release from one of the [Apache Download Mirrors](http://www.apache.org/dyn/closer.cgi/hadoop/common/)

### edit hadoop-env.sh

     # set to the root of your Java installation
     export JAVA_HOME=/usr/java/latest