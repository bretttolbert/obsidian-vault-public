# java

## See also
- [gradle](./gradle.md)

###### How to see JRE location and which are being loaded?
```bash
java -verbose
```

### Install Java JDK
```bash
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

### List available Java JREs
```bash
update-java-alternatives -l
```

### Pick desired Java JRE
```bash
sudo update-alternatives --config java
```

### Install java:
```bash
sudo apt-get install default-jre icedtea-plugin
```

### Install oracle-java8 on Ubuntu 14.04

[Install oracle-java8 on Ubuntu 14.04 via ppa](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html)

