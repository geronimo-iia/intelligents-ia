Intelligents-ia
===============

What we can found in this project ?

A super pom for my maven projects which configure many many things like:

* Default compiler and resource: JDK6, UTF-8
* Maven jar add maven descriptor
* Source artifact will be generated on jar goal
* Checksum file will be deployed into repository with md5 and sha1 extension
* Release automatically assign submodules the parent version
* Configure maven-gpg-plugin to sign with gpg and automaticaly call it on release
* Configure maven-license-plugin to add license information
* Profile 'document-artifacts' -Ddocument=true generate source and javadoc artifact
* Configure distribution Management and repository

"Intelligents-ia":http://intelligents-ia.com is my personal blog for playing...

GNUPG
-----

In order to work with it, you should do:
* install "Gnupg":http://www.gnupg.org/
* generate de secret key "example":http://www.cyberciti.biz/tips/linux-how-to-create-our-own-gnupg-privatepublic-key.html "gpg --gen-key"
* configure your pom with this property

** gnupg.homedir: The directory from which gpg will load keyrings.
** gnupg.keyname: Your Key Name
** gnupg.passphrase: Your Passphrase
** gnupg.skip: set to false to use it


	<properties>
		<gnupg.homedir>${basedir}/src/gnupg</gnupg.homedir>
		<gnupg.keyname>Your Key Name</gnupg.keyname>
		<gnupg.passphrase>Your Passphrase</gnupg.passphrase>
		<gnupg.skip>false</gnupg.skip>
	</properties>



License
-------

In your project you should have on root:

* a LICENSE.txt with license content
* a NOTICE.txt
* header.txt the header content which will be set

In pom of your your sub module, set properties like this:


	<license.header.path>${basedir}/../header.txt</license.header.path>


License will be check on package phase.

To add header information your have to do


	mvn license:format

If you would NOT use this plugin, set property 'license.skip' to true


	mvn -Dlicense.skip=true

or


	<properties>
		<license.skip>true</license.skip>
	</properties>


Eclipse Formatter, code templates and clean up
----------------------------------------------

Under src/config you could find:
* "codetemplates.xml":https://github.com/geronimo-iia/intelligents-ia/tree/master/src/config/codetemplates.xml
* "eclipse-clean-up.xml":https://github.com/geronimo-iia/intelligents-ia/tree/master/src/config/eclipse-clean-up.xml
* "eclipse-formatter.xml":https://github.com/geronimo-iia/intelligents-ia/tree/master/src/config/eclipse-formatter.xml


Find which version, tags and commit, comment that running
----------------------------------------------------------

From "git-commit-id-plugin":https://github.com/ktoso/maven-git-commit-id-plugin

This generate some usefull information in:


	src/main/resources/git.properties

Add in your .gitignore


	# git.properties
	git.properties



GitHub maven plugin
-------------------

From "GitHub":https://github.com/github/maven-plugins, if you would upload artifact on GitHub download section, you have to:

1. activate profile 'downloads-github'

	mvn -Pdownloads-github


2. add a server section in your 'settings.xml' with id 'github'



This plugin will be activated by:

	mvn deploy -Pdownloads-github

or

	mvn ghDownloads:upload -Pdownloads-github



Configure your pom
------------------

1. add parent section
2. add initial repository

 
For example:


	<parent>
		<groupId>org.intelligents-ia</groupId>
		<artifactId>intelligents-ia</artifactId>
		<version>1.4.8</version>
	</parent>
	. . .
	<repositories>
		<repository>
			<id>intelligents-ia-releases</id>
			<name>Intelligents-ia releases repository</name>
			<url>http://mvn.intelligents-ia.com/releases</url>
			<releases>
				<enabled>true</enabled>
			</releases>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</repository>
	</repositories>



Release Notes
=============

1.4.8
-----

Change list:
* add jvm.specification.version property
* add enforcer plugin declaration (not activated by default)

1.4.7
-----

Change list:
* update plugin version (maven, jgitflow, ...)
* change distribution management (extract root url from pom and use variable 'intelligentsia.distribution.management')
* distribution supported now: ssh and ftp protocol
* add plugin keystone in plugins management section, use 'keystone-plugin.version' to manage version (3.1 by default)

1.4.4
-----

Change list:
* add id on all plugins execution


1.4.3
-----

Change list:
* add optimized compilation
* integrate download "github plugin":https://github.com/github/maven-plugins
* fix issue on maven-antrun-plugin version
* activate license plugin and add skip mechanism with property 'license.skip'
* create profile intelligents-ia, activated per default


1.4.1
-----

Change list:
* add older repository
* add license plugin configuration
* add gnupg plugin configuration
* add initial config for maven site plugin



