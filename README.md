ecs-alfresco-content-store
===
Content Store implementation to store data in EMC Elastic Cloud Storage via S3. This produces an Alfresco Module Package (amp) file, configured to use ECS S3 for primary storage. You could also use S3 for other purposes, such as replication. In that case, you will need to change the configuration files appropriately and then rebuild the amp with that new configuration.

How to develop and build
---
This is basically a maven project to build an Alfresco Module Package (amp) file, with a simple gradle wrapper to create a distribution zip for that amp. The reason for not moving the basic amp build to gradle is that alfresco provides downloadable maven plugins but not gradle plugins. An amp file is basically a jarred set of jar libraries and configuration files, with the extension "amp".

To work with the code in a development environment, you should import it as a maven project, using the pom.xml file. The gradle file does not contain the dependencies, so you can't import it as a gradle project.

The easiest way to build is from the command line with gradlew. Here are the most useful commands, all of which should be run from the project root folder.
  - './gradlew clean' - cleans up all produced artifacts
  - './gradlew buildAmp' - builds just the amp file.
  - './gradlew distZip' (or simply './gradlew') - builds a complete distribution zip file.

How to install the amp
---
You MUST do this before you first run Alfresco, as changing the content storage mechanism once any data has been stored will break your Alfresco deployment. The simplest technique is to use the Module Management Tool, as described below.
  - http://docs.alfresco.com/5.1/tasks/amp-install.html

You must also add the following properties to your alfresco-global.properties file:

    #where to store the data
    ecss3.bucketName=
    #configuration parameters for the ecs client - legacy version
    #access id
    ecss3.access_key=
    #access key
    ecss3.secret_key=
    #endpoint or comma-separated lost of endpoints
    ecss3.endpoint=https://object.ecstestdrive.com:443
    #true/false
    ecss3.enable_vhost=
    #true/false for enabling client-side load balancing
    ecss3.smart_client=
    #configuration parameters for the ecs client - new version
    ecss3.config_uri=

