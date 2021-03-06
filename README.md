How to convert property files to GNU GetText files
==================================================

In order to use the Translation feature of Launchpad we need to have our
string resources in gettext format (.po and .pot files) rather than a
properties file (.properties). To convert between formats we need the
translate-toolkit.

Install and check the tools
---------------------------

Installation in Ubuntu:
	
	sudo apt-get install translate-toolkit

Installation in Windows:
	
	http://translate.sourceforge.net/wiki/

Make sure the installed version is at least v1.8.0. We use flex 
properties files encoded with UTF-8, and prior versions didn't let you
use that format. 
	
	prop2po --version

Convert from properties files to gettext files
----------------------------------------------

Use your English properties file(s) to create translation template(s):

	prop2po --personality=flex --encoding=utf-8 --duplicates=msgctxt \ 
        -P <REPO_ROOT>/flex/standalone/locale/en_US/myResources.properties \
        <REPO_ROOT>/flex/standalone/templates/myResources/myResources.pot

Use the properties file(s) in other languages to create translation file(s):

	prop2po --personality=flex --encoding=utf-8 --duplicates=msgctxt \ 
        -t <REPO_ROOT>/flex/standalone/locale/en_US/myResources.properties \ 
        <REPO_ROOT>/flex/standalone/locale/es_ES/myResources.properties \ 
        <REPO_ROOT>/flex/standalone/templates/myResources/es.po

Convert from gettext files to properties files
----------------------------------------------

	po2prop --personality=flex --encoding=utf-8 \
        -t <REPO_ROOT>/flex/standalone/locale/en_US/myResources.properties \
        <REPO_ROOT>/flex/standalone/templates/myResources/es.po \
        <REPO_ROOT>/flex/standalone/locale/es_ES/myResources.properties
  
Should UTF-8 encoding give you any problems (it is escaped by default as \u1E7D) use Mozilla's template
that displays those chars as real Unicode chars. 
        
    po2prop --personality=mozilla \
        -t <REPO_ROOT>/flex/standalone/locale/en_US/myResources.properties \
        <REPO_ROOT>/flex/standalone/templates/myResources/es.po \
        <REPO_ROOT>/flex/standalone/locale/es_ES/myResources.properties    

