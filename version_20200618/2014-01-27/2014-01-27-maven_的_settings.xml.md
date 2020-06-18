#maven 的 settings.xml
###发表时间：2014-01-27
###分类：maven,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2009932" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2009932</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
--&gt;

&lt;!--
 | This is the configuration file for Maven. It can be specified at two levels:
 |
 |  1. User Level. This settings.xml file provides configuration for a single user, 
 |                 and is normally provided in ${user.home}/.m2/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -s /path/to/user/settings.xml
 |
 |  2. Global Level. This settings.xml file provides configuration for all Maven
 |                 users on a machine (assuming they're all using the same Maven
 |                 installation). It's normally provided in 
 |                 ${maven.home}/conf/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -gs /path/to/global/settings.xml
 |
 | The sections in this sample file are intended to give you a running start at
 | getting the most out of your Maven installation. Where appropriate, the default
 | values (values used when the setting is not specified) are provided.
 |
 |--&gt;
&lt;settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" 
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"&gt;
  &lt;!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ~/.m2/repository
  &lt;localRepository&gt;/path/to/local/repo&lt;/localRepository&gt;
  --&gt;

  &lt;!-- interactiveMode
   | This will determine whether maven prompts you when it needs input. If set to false,
   | maven will use a sensible default value, perhaps based on some other setting, for
   | the parameter in question.
   |
   | Default: true
  &lt;interactiveMode&gt;true&lt;/interactiveMode&gt;
  --&gt;

  &lt;!-- offline
   | Determines whether maven should attempt to connect to the network when executing a build.
   | This will have an effect on artifact downloads, artifact deployment, and others.
   |
   | Default: false
  &lt;offline&gt;false&lt;/offline&gt;
  --&gt;

  &lt;!-- pluginGroups
   | This is a list of additional group identifiers that will be searched when resolving plugins by their prefix, i.e.
   | when invoking a command line like "mvn prefix:goal". Maven will automatically add the group identifiers
   | "org.apache.maven.plugins" and "org.codehaus.mojo" if these are not already contained in the list.
   |--&gt;
  &lt;pluginGroups&gt;
    &lt;!-- pluginGroup
     | Specifies a further group identifier to use for plugin lookup.
    &lt;pluginGroup&gt;com.your.plugins&lt;/pluginGroup&gt;
    --&gt;
  &lt;/pluginGroups&gt;

  &lt;!-- proxies
   | This is a list of proxies which can be used on this machine to connect to the network.
   | Unless otherwise specified (by system property or command-line switch), the first proxy
   | specification in this list marked as active will be used.
   |--&gt;
  &lt;proxies&gt;
    &lt;!-- proxy
     | Specification for one proxy, to be used in connecting to the network.
     |
    &lt;proxy&gt;
      &lt;id&gt;optional&lt;/id&gt;
      &lt;active&gt;true&lt;/active&gt;
      &lt;protocol&gt;http&lt;/protocol&gt;
      &lt;username&gt;proxyuser&lt;/username&gt;
      &lt;password&gt;proxypass&lt;/password&gt;
      &lt;host&gt;proxy.host.net&lt;/host&gt;
      &lt;port&gt;80&lt;/port&gt;
      &lt;nonProxyHosts&gt;local.net|some.host.com&lt;/nonProxyHosts&gt;
    &lt;/proxy&gt;
    --&gt;
  &lt;/proxies&gt;

  &lt;!-- servers
   | This is a list of authentication profiles, keyed by the server-id used within the system.
   | Authentication profiles can be used whenever maven must make a connection to a remote server.
   |--&gt;
 &lt;!--  &lt;servers&gt; --&gt;
    &lt;!-- server
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     | 
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are 
     |       used together.
     |
    &lt;server&gt;
      &lt;id&gt;deploymentRepo&lt;/id&gt;
      &lt;username&gt;repouser&lt;/username&gt;
      &lt;password&gt;repopwd&lt;/password&gt;
    &lt;/server&gt;
    --&gt;
    
    &lt;!-- Another sample, using keys to authenticate.
    &lt;server&gt;
      &lt;id&gt;siteServer&lt;/id&gt;
      &lt;privateKey&gt;/path/to/private/key&lt;/privateKey&gt;
      &lt;passphrase&gt;optional; leave empty if not used.&lt;/passphrase&gt;
    &lt;/server&gt;
    --&gt;
  &lt;!-- &lt;/servers&gt; --&gt;
  

  &lt;!-- mirrors
   | This is a list of mirrors to be used in downloading artifacts from remote repositories.
   | 
   | It works like this: a POM may declare a repository to use in resolving certain artifacts.
   | However, this repository may have problems with heavy traffic at times, so people have mirrored
   | it to several places.
   |
   | That repository definition will have a unique id, so we can create a mirror reference for that
   | repository, to be used as an alternate download site. The mirror site will be the preferred 
   | server for that repository.
   |--&gt;
  &lt;!-- &lt;mirrors&gt; --&gt;
    &lt;!-- mirror
     | Specifies a repository mirror site to use instead of a given repository. The repository that
     | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
     | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
     |
    &lt;mirror&gt;
      &lt;id&gt;mirrorId&lt;/id&gt;
      &lt;mirrorOf&gt;repositoryId&lt;/mirrorOf&gt;
      &lt;name&gt;Human Readable Name for this Mirror.&lt;/name&gt;
      &lt;url&gt;http://my.repository.com/repo/path&lt;/url&gt;
    &lt;/mirror&gt;
     --&gt;
  &lt;!-- &lt;/mirrors&gt; --&gt;
  
  &lt;!-- profiles
   | This is a list of profiles which can be activated in a variety of ways, and which can modify
   | the build process. Profiles provided in the settings.xml are intended to provide local machine-
   | specific paths and repository locations which allow the build to work in the local environment.
   |
   | For example, if you have an integration testing plugin - like cactus - that needs to know where
   | your Tomcat instance is installed, you can provide a variable here such that the variable is 
   | dereferenced during the build process to configure the cactus plugin.
   |
   | As noted above, profiles can be activated in a variety of ways. One way - the activeProfiles
   | section of this document (settings.xml) - will be discussed later. Another way essentially
   | relies on the detection of a system property, either matching a particular value for the property,
   | or merely testing its existence. Profiles can also be activated by JDK version prefix, where a 
   | value of '1.4' might activate a profile when the build is executed on a JDK version of '1.4.2_07'.
   | Finally, the list of active profiles can be specified directly from the command line.
   |
   | NOTE: For profiles defined in the settings.xml, you are restricted to specifying only artifact
   |       repositories, plugin repositories, and free-form properties to be used as configuration
   |       variables for plugins in the POM.
   |
   |--&gt;
  &lt;!-- &lt;profiles&gt; --&gt;
    &lt;!-- profile
     | Specifies a set of introductions to the build process, to be activated using one or more of the
     | mechanisms described above. For inheritance purposes, and to activate profiles via &lt;activatedProfiles/&gt;
     | or the command line, profiles have to have an ID that is unique.
     |
     | An encouraged best practice for profile identification is to use a consistent naming convention
     | for profiles, such as 'env-dev', 'env-test', 'env-production', 'user-jdcasey', 'user-brett', etc.
     | This will make it more intuitive to understand what the set of introduced profiles is attempting
     | to accomplish, particularly when you only have a list of profile id's for debug.
     |
     | This profile example uses the JDK version to trigger activation, and provides a JDK-specific repo.
    &lt;profile&gt;
      &lt;id&gt;jdk-1.4&lt;/id&gt;

      &lt;activation&gt;
        &lt;jdk&gt;1.4&lt;/jdk&gt;
      &lt;/activation&gt;

      &lt;repositories&gt;
        &lt;repository&gt;
          &lt;id&gt;jdk14&lt;/id&gt;
          &lt;name&gt;Repository for JDK 1.4 builds&lt;/name&gt;
          &lt;url&gt;http://www.myhost.com/maven/jdk14&lt;/url&gt;
          &lt;layout&gt;default&lt;/layout&gt;
          &lt;snapshotPolicy&gt;always&lt;/snapshotPolicy&gt;
        &lt;/repository&gt;
      &lt;/repositories&gt;
    &lt;/profile&gt;
    --&gt;

    &lt;!--
     | Here is another profile, activated by the system property 'target-env' with a value of 'dev',
     | which provides a specific path to the Tomcat instance. To use this, your plugin configuration
     | might hypothetically look like:
     |
     | ...
     | &lt;plugin&gt;
     |   &lt;groupId&gt;org.myco.myplugins&lt;/groupId&gt;
     |   &lt;artifactId&gt;myplugin&lt;/artifactId&gt;
     |   
     |   &lt;configuration&gt;
     |     &lt;tomcatLocation&gt;${tomcatPath}&lt;/tomcatLocation&gt;
     |   &lt;/configuration&gt;
     | &lt;/plugin&gt;
     | ...
     |
     | NOTE: If you just wanted to inject this configuration whenever someone set 'target-env' to
     |       anything, you could just leave off the &lt;value/&gt; inside the activation-property.
     |
    &lt;profile&gt;
      &lt;id&gt;env-dev&lt;/id&gt;

      &lt;activation&gt;
        &lt;property&gt;
          &lt;name&gt;target-env&lt;/name&gt;
          &lt;value&gt;dev&lt;/value&gt;
        &lt;/property&gt;
      &lt;/activation&gt;

      &lt;properties&gt;
        &lt;tomcatPath&gt;/path/to/tomcat/instance&lt;/tomcatPath&gt;
      &lt;/properties&gt;
    &lt;/profile&gt;
    --&gt;
  &lt;!-- &lt;/profiles&gt; --&gt;

  &lt;!-- activeProfiles
   | List of profiles that are active for all builds.
   |
  &lt;activeProfiles&gt;
    &lt;activeProfile&gt;alwaysActiveProfile&lt;/activeProfile&gt;
    &lt;activeProfile&gt;anotherAlwaysActiveProfile&lt;/activeProfile&gt;
  &lt;/activeProfiles&gt;
  --&gt;
  


&lt;!-- 
&lt;mirrors&gt;
	&lt;mirror&gt;
	&lt;id&gt;local-nexus&lt;/id&gt;
	&lt;name&gt;My test repository&lt;/name&gt;
	&lt;url&gt;http://vm-server:8080/nexus/content/groups/local-nexus/&lt;/url&gt;
	&lt;mirrorOf&gt;*&lt;/mirrorOf&gt;
	&lt;/mirror&gt;
&lt;/mirrors&gt;
	  
	&lt;servers&gt;
	  &lt;server&gt;
	    &lt;id&gt;releases&lt;/id&gt;
	    &lt;username&gt;admin&lt;/username&gt;
	    &lt;password&gt;admin123&lt;/password&gt;
	  &lt;/server&gt;
	  &lt;server&gt;
	    &lt;id&gt;snapshots&lt;/id&gt;
	    &lt;username&gt;admin&lt;/username&gt;
	    &lt;password&gt;admin123&lt;/password&gt;
	  &lt;/server&gt;  
	&lt;/servers&gt;  
  
  
	&lt;profiles&gt;
	  &lt;profile&gt;
	    &lt;id&gt;nexus&lt;/id&gt;
	    &lt;repositories&gt;
	      &lt;repository&gt;
	        &lt;id&gt;local-nexus&lt;/id&gt;
	        &lt;url&gt;http://vm-server:8080/nexus/content/groups/local-nexus/&lt;/url&gt;
	        &lt;releases&gt;
	          &lt;enabled&gt;true&lt;/enabled&gt;
	        &lt;/releases&gt;
	        &lt;snapshots&gt;
	          &lt;enabled&gt;true&lt;/enabled&gt;
	        &lt;/snapshots&gt;
	      &lt;/repository&gt;
	    &lt;/repositories&gt;
	    
	    &lt;pluginRepositories&gt;
	    	&lt;pluginRepository&gt;
	    		&lt;id&gt;nexus&lt;/id&gt;
	    		&lt;url&gt;http://vm-server:8080/nexus/content/groups/local-nexus/&lt;/url&gt;
	    		&lt;releases&gt;
	          &lt;enabled&gt;true&lt;/enabled&gt;
	        &lt;/releases&gt;
	        &lt;snapshots&gt;
	          &lt;enabled&gt;true&lt;/enabled&gt;
	        &lt;/snapshots&gt;	        
	    	&lt;/pluginRepository&gt;
	    &lt;/pluginRepositories&gt;
	    	    
	  &lt;/profile&gt;
	&lt;/profiles&gt;
	&lt;activeProfiles&gt;
	  &lt;activeProfile&gt;nexus&lt;/activeProfile&gt;
	&lt;/activeProfiles&gt;

--&gt;

	&lt;localRepository&gt;D:\develop\maven-localRepository&lt;/localRepository&gt;
	
	&lt;mirrors&gt;
		&lt;mirror&gt;
		&lt;!--This sends everything else to /public --&gt;
		&lt;id&gt;nexus&lt;/id&gt;
		&lt;mirrorOf&gt;*&lt;/mirrorOf&gt;
		&lt;!-- &lt;url&gt;http://wm-nexus:8080/nexus/content/groups/public/&lt;/url&gt; --&gt;
		&lt;url&gt;http://localhost:8087/nexus/content/groups/public/&lt;/url&gt;
		&lt;/mirror&gt;
	&lt;/mirrors&gt;

	&lt;profiles&gt;
		&lt;profile&gt;
		&lt;id&gt;nexus&lt;/id&gt;
		&lt;!--Enable snapshots for the built in central repo to direct --&gt;
		&lt;!--all requests to nexus via the mirror --&gt;
		&lt;repositories&gt;
			&lt;repository&gt;
				&lt;id&gt;central&lt;/id&gt;
				&lt;url&gt;http://central&lt;/url&gt;
				&lt;releases&gt;&lt;enabled&gt;true&lt;/enabled&gt;&lt;/releases&gt;
				&lt;snapshots&gt;&lt;enabled&gt;true&lt;/enabled&gt;&lt;/snapshots&gt;
			&lt;/repository&gt;
		&lt;/repositories&gt;
		&lt;pluginRepositories&gt;
			&lt;pluginRepository&gt;
				&lt;id&gt;central&lt;/id&gt;
				&lt;url&gt;http://central&lt;/url&gt;
				&lt;releases&gt;&lt;enabled&gt;true&lt;/enabled&gt;&lt;/releases&gt;
				&lt;snapshots&gt;&lt;enabled&gt;true&lt;/enabled&gt;&lt;/snapshots&gt;
			&lt;/pluginRepository&gt;
		&lt;/pluginRepositories&gt;
		&lt;/profile&gt;
	&lt;/profiles&gt;
	&lt;activeProfiles&gt;
	&lt;!--make the profile active all the time --&gt;
	&lt;activeProfile&gt;nexus&lt;/activeProfile&gt;
	&lt;/activeProfiles&gt;
	  
&lt;/settings&gt;
</pre> 
 <p>&nbsp;</p> 
</div>