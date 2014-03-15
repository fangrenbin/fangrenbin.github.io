---
layout: post
title: "How to install jekins on your server"
description: ""
category: jenkins
tags: [jenkins]
---
{% include JB/setup %}

Enviroment: CentOS release 5.9 final

###install java enviroment###

1. #####Download jdk-6u30-linux-x64-rpm.bin#####
		$chmod +x jdk-6u30-linux-x64-rpm.bin
		$./jdk-6u30-linux-x64-rpm.bin
2. ####Install maven####
		$tar -zxvf apache-maven-3.0.4
		$sudo mkdir /opt/maven
		$sudo mv ~/software/apache-maven-3.0.4 /opt/maven
		$sudo vim /etc/profile

	Show maven version

		mvn -v
3. ####Install Jenkins####
		sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
		sudo rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
		sudo yum install jenkins
		#change own
		sudo chown -R admin /var/log/jenkins
		sudo chgrp -R admin /var/log/jenkins

		sudo chown -R admin /var/lib/jenkins
		sudo chgrp -R admin /var/lib/jenkins

		sudo chown -R admin /var/cache/jenkins
		sudo chgrp -R admin /var/cache/jenkins
	
	jenkins configraution files
	
		/etc/sysconfig/jenkins
	
	make it load up when system start up
	
		sudo chkconfig jenkins on