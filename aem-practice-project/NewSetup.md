# Project Information
1. To create AEM fres instance with no sample content, Open command prompt and go to the location where AEM Jar reside. Run the following command to create instance with no sample content:
   * java -server -XX:MaxPermSize=256m -Xmx1024M -jar cq-author.6.5-p4502.jar -r author,nosamplecontent
####NOTE
cq-author.6.5-p4502 is AEM jar name it may change according to the jar available in your system.
  
2. This project is based on Maven AEM Project Archetype 27.
3. Run the following command to build and deploy the entire project to AEM instance
   * mvn clean install -PautoInstallSinglePackage
4. The core module contains all the Java code associated with the project. To deploy only core module on AEM instance use below maven command under core location:
   * mvn clean install -PautoInstallBundle
5. The ui.apps maven module contains all of the rendering code needed for the site beneath /apps. This includes CSS/JS that will be stored in an AEM format called clientlibs. This also includes HTL scripts for rendering dynamic HTML. To build the just this module use below maven command under apps location:
   * mvn clean install -PautoInstallPackage
####NOTE
* For deploying apps package on publish instance (on default port 4503) use below maven command:
    * mvn -PautoInstallPackagePublish clean install
* For deploying apps package on publish instance with different port say 4504, use below maven command:
    * mvn -PautoInstallPackage clean install -Daem.port=4504

# Useful Information of setting a new project


# Useful Information of setting a new project

## Project Setup

### Prerequisites
* Ensure that you have a fresh instance of Adobe Experience Manager available locally and that no additional sample/demo packages have been installed (other than required Service Packs).
* Your AEM project contains all of the code, content, and configurations used for a Sites implementation.

### Create the project
* There are a couple options for creating a Maven Multi-module project for AEM. 
* This guide will leverage the Maven AEM Project Archetype 27.
* Cloud Manager also provides a UI wizard to initiate the creation of an AEM application project.

#### NOTE
*  It is always a best practice to use the latest version of the archetype to generate a new project.

### Steps
1. Open up a command line terminal. Verify that Maven is installed:
*  mvn --version

2. Verify that the adobe-public profile is active by running the following command:
*  mvn help:effective-settings

#### NOTE
* If you do not see the adobe-public it is an indication that the Adobe repo is not properly referenced in your ~/.m2/settings.xml file. Please install and configure Apache Maven in a local development environment.

3. Navigate to a directory in where we want to generate the AEM project. This directory in which we want to maintain our project’s source code.
*  Paste the following into the command line to generate the project in batch mode:
*  mvn -B archetype:generate \
-D archetypeGroupId=com.adobe.aem \
-D archetypeArtifactId=aem-project-archetype \
-D archetypeVersion=27 \
-D appTitle="My Practice Project" \
-D appId="practice-project" \
-D groupId="com.adobe.aem.practice.project" \
-D artifactId="aem-practice-project" \
-D version="0.0.1-SNAPSHOT" \
-D aemVersion="6.5.8"
   
#### NOTE
* If targeting AEM 6.5.8+ then aemVersion="6.5.8". If targeting cloud services then aemVersion="cloud".

4) Install service pack 6.5.8 (download it from https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)


# Troubleshoot

###Enabling CRXDE Lite in AEM

* When new AEM instance is created with nosample content then crx/de is disabled by default for security reasons.
* In order to ensure that AEM installations are as secure as possible, the security checklist recommends disabling WebDAV in production environments. However, CRXDE Lite depends on the org.apache.sling.jcr.davex bundle to function properly, so disabling WebDAV will effectively disable CRXDE Lite as well.
* If disabled, you can turn CRXDE Lite on by following the below procedure:
  * Go to the OSGi Components console at http://localhost:4502/system/console/components
  * Search for the following component:
    * org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
  * Click the wrench icon next to it in order to see its configuration options
  * Create the following configuration:
    * Root path: /crx/server
    * Tick the box under Use absolute URIs.
    

