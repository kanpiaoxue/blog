#Curator的pom.xml(可做Maven的pom.xml的范例)
###发表时间：2014-08-06
###分类：maven,curator,zookeeper
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2101081" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2101081</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;&lt;!--
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

&lt;project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;

    &lt;parent&gt;
        &lt;groupId&gt;org.apache&lt;/groupId&gt;
        &lt;artifactId&gt;apache&lt;/artifactId&gt;
        &lt;version&gt;14&lt;/version&gt;
    &lt;/parent&gt;

    &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
    &lt;artifactId&gt;apache-curator&lt;/artifactId&gt;
    &lt;version&gt;2.6.1-SNAPSHOT&lt;/version&gt;
    &lt;packaging&gt;pom&lt;/packaging&gt;

    &lt;name&gt;Apache Curator&lt;/name&gt;
    &lt;description&gt;
        Curator is a set of Java libraries that make using Apache ZooKeeper much easier.
    &lt;/description&gt;
    &lt;url&gt;http://curator.apache.org&lt;/url&gt;
    &lt;inceptionYear&gt;2011&lt;/inceptionYear&gt;

    &lt;licenses&gt;
        &lt;license&gt;
            &lt;name&gt;The Apache Software License, Version 2.0&lt;/name&gt;
            &lt;url&gt;file://${basedir}/LICENSE&lt;/url&gt;
            &lt;distribution&gt;repo&lt;/distribution&gt;
        &lt;/license&gt;
    &lt;/licenses&gt;

    &lt;organization&gt;
        &lt;name&gt;The Apache Software Foundation&lt;/name&gt;
        &lt;url&gt;http://www.apache.org/&lt;/url&gt;
    &lt;/organization&gt;

    &lt;properties&gt;
        &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
        &lt;project.build.resourceEncoding&gt;UTF-8&lt;/project.build.resourceEncoding&gt;
        &lt;project.reporting.outputEncoding&gt;UTF-8&lt;/project.reporting.outputEncoding&gt;

        &lt;jdk-version&gt;1.6&lt;/jdk-version&gt;

        &lt;!-- versions --&gt;
        &lt;maven-project-info-reports-plugin-version&gt;2.7&lt;/maven-project-info-reports-plugin-version&gt;
        &lt;maven-javadoc-plugin-version&gt;2.9.1&lt;/maven-javadoc-plugin-version&gt;
        &lt;maven-dependency-plugin-version&gt;2.8&lt;/maven-dependency-plugin-version&gt;
        &lt;maven-install-plugin-version&gt;2.5.1&lt;/maven-install-plugin-version&gt;
        &lt;maven-compiler-plugin-version&gt;3.1&lt;/maven-compiler-plugin-version&gt;
        &lt;maven-bundle-plugin-version&gt;2.3.7&lt;/maven-bundle-plugin-version&gt;
        &lt;maven-surefire-plugin-version&gt;2.17&lt;/maven-surefire-plugin-version&gt;
        &lt;maven-site-plugin-version&gt;3.3&lt;/maven-site-plugin-version&gt;
        &lt;doxia-module-confluence-version&gt;1.5&lt;/doxia-module-confluence-version&gt;
        &lt;maven-scm-publish-plugin-version&gt;1.0&lt;/maven-scm-publish-plugin-version&gt;
        &lt;maven-license-plugin-version&gt;1.9.0&lt;/maven-license-plugin-version&gt;
        &lt;maven-release-plugin-version&gt;2.5&lt;/maven-release-plugin-version&gt;
        &lt;apache-rat-plugin-version&gt;0.10&lt;/apache-rat-plugin-version&gt;
        &lt;javassist-version&gt;3.18.1-GA&lt;/javassist-version&gt;
        &lt;commons-math-version&gt;2.2&lt;/commons-math-version&gt;
        &lt;jackson-mapper-asl-version&gt;1.9.13&lt;/jackson-mapper-asl-version&gt;
        &lt;jersey-version&gt;1.18.1&lt;/jersey-version&gt;
        &lt;jsr311-api-version&gt;1.1.1&lt;/jsr311-api-version&gt;
        &lt;jetty-version&gt;6.1.26&lt;/jetty-version&gt;
        &lt;scannotation-version&gt;1.0.2&lt;/scannotation-version&gt;
        &lt;resteasy-jaxrs-version&gt;2.3.0.GA&lt;/resteasy-jaxrs-version&gt;
        &lt;zookeeper-version&gt;3.4.6&lt;/zookeeper-version&gt;
        &lt;guava-version&gt;16.0.1&lt;/guava-version&gt;
        &lt;testng-version&gt;6.8.8&lt;/testng-version&gt;
        &lt;swift-version&gt;0.12.0&lt;/swift-version&gt;
        &lt;dropwizard-version&gt;0.7.0&lt;/dropwizard-version&gt;
        &lt;maven-shade-plugin-version&gt;2.3&lt;/maven-shade-plugin-version&gt;

        &lt;!-- OSGi Properties --&gt;
        &lt;osgi.export.package /&gt;
        &lt;osgi.import.package /&gt;
        &lt;osgi.private.package /&gt;
        &lt;osgi.dynamic.import /&gt;
        &lt;osgi.require.bundle /&gt;
        &lt;osgi.export.service /&gt;
        &lt;osgi.activator /&gt;
    &lt;/properties&gt;

    &lt;scm&gt;
        &lt;url&gt;https://github.com/apache/curator.git&lt;/url&gt;
        &lt;connection&gt;scm:git:https://git-wip-us.apache.org/repos/asf/curator.git&lt;/connection&gt;
        &lt;developerConnection&gt;scm:git:https://git-wip-us.apache.org/repos/asf/curator.git
        &lt;/developerConnection&gt;
        &lt;tag&gt;HEAD&lt;/tag&gt;
    &lt;/scm&gt;

    &lt;issueManagement&gt;
        &lt;system&gt;JIRA&lt;/system&gt;
        &lt;url&gt;http://issues.apache.org/jira/browse/CURATOR&lt;/url&gt;
    &lt;/issueManagement&gt;

    &lt;ciManagement&gt;
        &lt;system&gt;Jenkins&lt;/system&gt;
        &lt;url&gt;https://builds.apache.org/job/Curator/&lt;/url&gt;
        &lt;notifiers&gt;
            &lt;notifier&gt;
                &lt;type&gt;mail&lt;/type&gt;
                &lt;sendOnError&gt;true&lt;/sendOnError&gt;
                &lt;sendOnFailure&gt;true&lt;/sendOnFailure&gt;
                &lt;sendOnSuccess&gt;false&lt;/sendOnSuccess&gt;
                &lt;sendOnWarning&gt;false&lt;/sendOnWarning&gt;
                &lt;configuration&gt;
                    &lt;address&gt;dev@curator.apache.org&lt;/address&gt;
                &lt;/configuration&gt;
            &lt;/notifier&gt;
        &lt;/notifiers&gt;
    &lt;/ciManagement&gt;

    &lt;distributionManagement&gt;
        &lt;site&gt;
            &lt;id&gt;apache.website.svnpub&lt;/id&gt;
            &lt;url&gt;scm:svn:https://svn.apache.org/repos/asf/curator/site/trunk&lt;/url&gt;
        &lt;/site&gt;
    &lt;/distributionManagement&gt;

    &lt;mailingLists&gt;
        &lt;mailingList&gt;
            &lt;name&gt;Users&lt;/name&gt;
            &lt;post&gt;user@curator.apache.org&lt;/post&gt;
            &lt;subscribe&gt;user-subscribe@curator.apache.org&lt;/subscribe&gt;
            &lt;unsubscribe&gt;user-unsubscribe@curator.apache.org&lt;/unsubscribe&gt;
            &lt;archive&gt;http://mail-archives.apache.org/mod_mbox/curator-user/&lt;/archive&gt;
        &lt;/mailingList&gt;
        &lt;mailingList&gt;
            &lt;name&gt;Development&lt;/name&gt;
            &lt;post&gt;dev@curator.apache.org&lt;/post&gt;
            &lt;subscribe&gt;dev-subscribe@curator.apache.org&lt;/subscribe&gt;
            &lt;unsubscribe&gt;dev-unsubscribe@curator.apache.org&lt;/unsubscribe&gt;
            &lt;archive&gt;http://mail-archives.apache.org/mod_mbox/curator-dev/&lt;/archive&gt;
        &lt;/mailingList&gt;
        &lt;mailingList&gt;
            &lt;name&gt;Commits&lt;/name&gt;
            &lt;post&gt;commits@curator.apache.org&lt;/post&gt;
            &lt;subscribe&gt;commits-subscribe@curator.apache.org&lt;/subscribe&gt;
            &lt;unsubscribe&gt;commits-unsubscribe@curator.apache.org&lt;/unsubscribe&gt;
            &lt;archive&gt;http://mail-archives.apache.org/mod_mbox/curator-commits/&lt;/archive&gt;
        &lt;/mailingList&gt;
    &lt;/mailingLists&gt;

    &lt;developers&gt;
        &lt;developer&gt;
            &lt;id&gt;randgalt&lt;/id&gt;
            &lt;name&gt;Jordan Zimmerman&lt;/name&gt;
            &lt;email&gt;randgalt@apache.org&lt;/email&gt;
            &lt;timezone&gt;-5&lt;/timezone&gt;
            &lt;roles&gt;
                &lt;role&gt;Committer&lt;/role&gt;
                &lt;role&gt;PMC Chair&lt;/role&gt;
            &lt;/roles&gt;
            &lt;url&gt;https://people.apache.org/~randgalt&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;id&gt;zarfide&lt;/id&gt;
            &lt;name&gt;Jay Zarfoss&lt;/name&gt;
            &lt;email&gt;zarfide@apache.org&lt;/email&gt;
            &lt;timezone&gt;-8&lt;/timezone&gt;
            &lt;roles&gt;
                &lt;role&gt;Committer&lt;/role&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;url&gt;http://www.linkedin.com/pub/jay-zarfoss/34/56/a19&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;id&gt;cheddar&lt;/id&gt;
            &lt;name&gt;Eric Tschetter&lt;/name&gt;
            &lt;email&gt;cheddar@apache.org&lt;/email&gt;
            &lt;timezone&gt;-6&lt;/timezone&gt;
            &lt;roles&gt;
                &lt;role&gt;Committer&lt;/role&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
                &lt;role&gt;ChedHeader&lt;/role&gt;
            &lt;/roles&gt;
        &lt;/developer&gt;
        &lt;developer&gt;
            &lt;id&gt;iocanel&lt;/id&gt;
            &lt;name&gt;Ioannis Canellos&lt;/name&gt;
            &lt;email&gt;iocanel@apache.org&lt;/email&gt;
            &lt;timezone&gt;+2&lt;/timezone&gt;
            &lt;roles&gt;
                &lt;role&gt;Committer&lt;/role&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;url&gt;http://iocanel.blogspot.com&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;id&gt;cammckenzie&lt;/id&gt;
            &lt;name&gt;Cameron McKenzie&lt;/name&gt;
            &lt;email&gt;cammckenzie@apache.org&lt;/email&gt;
            &lt;timezone&gt;+10&lt;/timezone&gt;
            &lt;roles&gt;
                &lt;role&gt;Committer&lt;/role&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;url&gt;https://people.apache.org/~cammckenzie&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;name&gt;Patrick Hunt&lt;/name&gt;
            &lt;email&gt;phunt1@gmail.com&lt;/email&gt;
            &lt;roles&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;timezone&gt;-8&lt;/timezone&gt;
            &lt;url&gt;http://www.linkedin.com/pub/patrick-hunt/2/5b2/24a&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;name&gt;Mahadev Konar&lt;/name&gt;
            &lt;email&gt;mahadev@apache.org&lt;/email&gt;
            &lt;roles&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;timezone&gt;-8&lt;/timezone&gt;
            &lt;url&gt;http://www.linkedin.com/in/mahadevkonar&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;name&gt;Luciano Resende&lt;/name&gt;
            &lt;email&gt;lresende@apache.org&lt;/email&gt;
            &lt;roles&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;timezone&gt;-8&lt;/timezone&gt;
            &lt;url&gt;https://people.apache.org/~lresende&lt;/url&gt;
        &lt;/developer&gt;

        &lt;developer&gt;
            &lt;name&gt;Enis Söztutar&lt;/name&gt;
            &lt;email&gt;enis@apache.org&lt;/email&gt;
            &lt;roles&gt;
                &lt;role&gt;PMC Member&lt;/role&gt;
            &lt;/roles&gt;
            &lt;timezone&gt;-8&lt;/timezone&gt;
            &lt;url&gt;https://people.apache.org/~enis&lt;/url&gt;
        &lt;/developer&gt;
    &lt;/developers&gt;

    &lt;modules&gt;
        &lt;module&gt;curator-client&lt;/module&gt;
        &lt;module&gt;curator-test&lt;/module&gt;
        &lt;module&gt;curator-framework&lt;/module&gt;
        &lt;module&gt;curator-recipes&lt;/module&gt;
        &lt;module&gt;curator-examples&lt;/module&gt;
        &lt;module&gt;curator-x-discovery&lt;/module&gt;
        &lt;module&gt;curator-x-discovery-server&lt;/module&gt;
        &lt;module&gt;curator-x-rpc&lt;/module&gt;
    &lt;/modules&gt;

    &lt;dependencyManagement&gt;
        &lt;dependencies&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
                &lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;
                &lt;version&gt;1.7.6&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.mockito&lt;/groupId&gt;
                &lt;artifactId&gt;mockito-core&lt;/artifactId&gt;
                &lt;version&gt;1.9.5&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
                &lt;artifactId&gt;curator-client&lt;/artifactId&gt;
                &lt;version&gt;${project.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
                &lt;artifactId&gt;curator-framework&lt;/artifactId&gt;
                &lt;version&gt;${project.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
                &lt;artifactId&gt;curator-recipes&lt;/artifactId&gt;
                &lt;version&gt;${project.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
                &lt;artifactId&gt;curator-test&lt;/artifactId&gt;
                &lt;version&gt;${project.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
                &lt;artifactId&gt;curator-x-discovery&lt;/artifactId&gt;
                &lt;version&gt;${project.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
                &lt;artifactId&gt;curator-x-discovery-server&lt;/artifactId&gt;
                &lt;version&gt;${project.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.javassist&lt;/groupId&gt;
                &lt;artifactId&gt;javassist&lt;/artifactId&gt;
                &lt;version&gt;${javassist-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
                &lt;artifactId&gt;commons-math&lt;/artifactId&gt;
                &lt;version&gt;${commons-math-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.codehaus.jackson&lt;/groupId&gt;
                &lt;artifactId&gt;jackson-mapper-asl&lt;/artifactId&gt;
                &lt;version&gt;${jackson-mapper-asl-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;
                &lt;artifactId&gt;jersey-server&lt;/artifactId&gt;
                &lt;version&gt;${jersey-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;
                &lt;artifactId&gt;jersey-servlet&lt;/artifactId&gt;
                &lt;version&gt;${jersey-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;
                &lt;artifactId&gt;jersey-client&lt;/artifactId&gt;
                &lt;version&gt;${jersey-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;
                &lt;artifactId&gt;jersey-core&lt;/artifactId&gt;
                &lt;version&gt;${jersey-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;javax.ws.rs&lt;/groupId&gt;
                &lt;artifactId&gt;jsr311-api&lt;/artifactId&gt;
                &lt;version&gt;${jsr311-api-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.mortbay.jetty&lt;/groupId&gt;
                &lt;artifactId&gt;jetty&lt;/artifactId&gt;
                &lt;version&gt;${jetty-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;net.sf.scannotation&lt;/groupId&gt;
                &lt;artifactId&gt;scannotation&lt;/artifactId&gt;
                &lt;version&gt;${scannotation-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.jboss.resteasy&lt;/groupId&gt;
                &lt;artifactId&gt;resteasy-jaxrs&lt;/artifactId&gt;
                &lt;version&gt;${resteasy-jaxrs-version}&lt;/version&gt;
                &lt;exclusions&gt;
                    &lt;exclusion&gt;
                        &lt;groupId&gt;org.scannotation&lt;/groupId&gt;
                        &lt;artifactId&gt;scannotation&lt;/artifactId&gt;
                    &lt;/exclusion&gt;
                &lt;/exclusions&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.zookeeper&lt;/groupId&gt;
                &lt;artifactId&gt;zookeeper&lt;/artifactId&gt;
                &lt;version&gt;${zookeeper-version}&lt;/version&gt;
                &lt;exclusions&gt;
                    &lt;exclusion&gt;
                        &lt;groupId&gt;com.sun.jmx&lt;/groupId&gt;
                        &lt;artifactId&gt;jmxri&lt;/artifactId&gt;
                    &lt;/exclusion&gt;
                    &lt;exclusion&gt;
                        &lt;groupId&gt;com.sun.jdmk&lt;/groupId&gt;
                        &lt;artifactId&gt;jmxtools&lt;/artifactId&gt;
                    &lt;/exclusion&gt;
                    &lt;exclusion&gt;
                        &lt;groupId&gt;javax.jms&lt;/groupId&gt;
                        &lt;artifactId&gt;jms&lt;/artifactId&gt;
                    &lt;/exclusion&gt;
                    &lt;exclusion&gt;
                        &lt;groupId&gt;junit&lt;/groupId&gt;
                        &lt;artifactId&gt;junit&lt;/artifactId&gt;
                    &lt;/exclusion&gt;
                    &lt;exclusion&gt;
                        &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
                        &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
                    &lt;/exclusion&gt;
                &lt;/exclusions&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
                &lt;artifactId&gt;guava&lt;/artifactId&gt;
                &lt;version&gt;${guava-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.testng&lt;/groupId&gt;
                &lt;artifactId&gt;testng&lt;/artifactId&gt;
                &lt;version&gt;${testng-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.facebook.swift&lt;/groupId&gt;
                &lt;artifactId&gt;swift-codec&lt;/artifactId&gt;
                &lt;version&gt;${swift-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.facebook.swift&lt;/groupId&gt;
                &lt;artifactId&gt;swift-service&lt;/artifactId&gt;
                &lt;version&gt;${swift-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;io.dropwizard&lt;/groupId&gt;
                &lt;artifactId&gt;dropwizard-configuration&lt;/artifactId&gt;
                &lt;version&gt;${dropwizard-version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;io.dropwizard&lt;/groupId&gt;
                &lt;artifactId&gt;dropwizard-logging&lt;/artifactId&gt;
                &lt;version&gt;${dropwizard-version}&lt;/version&gt;
            &lt;/dependency&gt;
        &lt;/dependencies&gt;
    &lt;/dependencyManagement&gt;

    &lt;dependencies&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.apache.zookeeper&lt;/groupId&gt;
            &lt;artifactId&gt;zookeeper&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
            &lt;artifactId&gt;guava&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;org.testng&lt;/groupId&gt;
            &lt;artifactId&gt;testng&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
    &lt;/dependencies&gt;

    &lt;reporting&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-project-info-reports-plugin&lt;/artifactId&gt;
                &lt;version&gt;${maven-project-info-reports-plugin-version}&lt;/version&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-javadoc-plugin&lt;/artifactId&gt;
                &lt;version&gt;${maven-javadoc-plugin-version}&lt;/version&gt;
                &lt;configuration&gt;
                    &lt;aggregate&gt;true&lt;/aggregate&gt;
                    &lt;additionalJOptions&gt;
                        &lt;additionalJOption&gt;-J-Xmx1g&lt;/additionalJOption&gt;
                    &lt;/additionalJOptions&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
    &lt;/reporting&gt;

    &lt;build&gt;
        &lt;pluginManagement&gt;
            &lt;plugins&gt;
                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-dependency-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-dependency-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-install-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-install-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-compiler-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.felix&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-bundle-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-bundle-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-surefire-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-surefire-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-javadoc-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-javadoc-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-site-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-site-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-scm-publish-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-scm-publish-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;com.mycila.maven-license-plugin&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-license-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-license-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-release-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-release-plugin-version}&lt;/version&gt;
                    &lt;configuration&gt;
                        &lt;autoVersionSubmodules&gt;true&lt;/autoVersionSubmodules&gt;
                        &lt;tagNameFormat&gt;${project.artifactId}-${project.version}&lt;/tagNameFormat&gt;
                        &lt;pushChanges&gt;false&lt;/pushChanges&gt;
                        &lt;localCheckout&gt;true&lt;/localCheckout&gt;
                    &lt;/configuration&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.rat&lt;/groupId&gt;
                    &lt;artifactId&gt;apache-rat-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${apache-rat-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;

                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-shade-plugin&lt;/artifactId&gt;
                    &lt;version&gt;${maven-shade-plugin-version}&lt;/version&gt;
                &lt;/plugin&gt;
            &lt;/plugins&gt;
        &lt;/pluginManagement&gt;

        &lt;resources&gt;
            &lt;resource&gt;
                &lt;directory&gt;${basedir}&lt;/directory&gt;
                &lt;targetPath&gt;META-INF&lt;/targetPath&gt;
                &lt;includes&gt;
                    &lt;include&gt;DISCLAIMER&lt;/include&gt;
                    &lt;include&gt;LICENSE&lt;/include&gt;
                    &lt;include&gt;NOTICE&lt;/include&gt;
                &lt;/includes&gt;
            &lt;/resource&gt;
        &lt;/resources&gt;

        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-dependency-plugin&lt;/artifactId&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-install-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;createChecksum&gt;true&lt;/createChecksum&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;source&gt;${jdk-version}&lt;/source&gt;
                    &lt;target&gt;${jdk-version}&lt;/target&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.felix&lt;/groupId&gt;
                &lt;artifactId&gt;maven-bundle-plugin&lt;/artifactId&gt;
                &lt;extensions&gt;true&lt;/extensions&gt;
                &lt;inherited&gt;true&lt;/inherited&gt;
                &lt;configuration&gt;
                    &lt;instructions&gt;
                        &lt;Bundle-Name&gt;${project.name}&lt;/Bundle-Name&gt;
                        &lt;Bundle-SymbolicName&gt;${project.artifactId}&lt;/Bundle-SymbolicName&gt;
                        &lt;Export-Package&gt;${osgi.export.package}&lt;/Export-Package&gt;
                        &lt;Import-Package&gt;${osgi.import.package}&lt;/Import-Package&gt;
                        &lt;DynamicImport-Package&gt;${osgi.dynamic.import}&lt;/DynamicImport-Package&gt;
                        &lt;Private-Package&gt;${osgi.private.package}&lt;/Private-Package&gt;
                        &lt;Require-Bundle&gt;${osgi.require.bundle}&lt;/Require-Bundle&gt;
                        &lt;Bundle-Activator&gt;${osgi.activator}&lt;/Bundle-Activator&gt;
                        &lt;Export-Service&gt;${osgi.export.service}&lt;/Export-Service&gt;
                    &lt;/instructions&gt;
                    &lt;supportedProjectTypes&gt;
                        &lt;supportedProjectType&gt;jar&lt;/supportedProjectType&gt;
                        &lt;supportedProjectType&gt;war&lt;/supportedProjectType&gt;
                        &lt;supportedProjectType&gt;bundle&lt;/supportedProjectType&gt;
                    &lt;/supportedProjectTypes&gt;
                    &lt;unpackBundle&gt;true&lt;/unpackBundle&gt;
                &lt;/configuration&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;id&gt;bundle-manifest&lt;/id&gt;
                        &lt;phase&gt;process-classes&lt;/phase&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;manifest&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-surefire-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;forkCount&gt;1&lt;/forkCount&gt;
                    &lt;reuseForks&gt;false&lt;/reuseForks&gt;
                    &lt;redirectTestOutputToFile&gt;true&lt;/redirectTestOutputToFile&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-javadoc-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;aggregate&gt;true&lt;/aggregate&gt;
                    &lt;additionalJOptions&gt;
                        &lt;additionalJOption&gt;-J-Xmx1g&lt;/additionalJOption&gt;
                    &lt;/additionalJOptions&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-site-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;locales&gt;en&lt;/locales&gt;
                    &lt;skipDeploy&gt;true&lt;/skipDeploy&gt;
                &lt;/configuration&gt;
                &lt;dependencies&gt;
                    &lt;dependency&gt;
                        &lt;groupId&gt;org.apache.maven.doxia&lt;/groupId&gt;
                        &lt;artifactId&gt;doxia-module-confluence&lt;/artifactId&gt;
                        &lt;version&gt;${doxia-module-confluence-version}&lt;/version&gt;
                    &lt;/dependency&gt;
                &lt;/dependencies&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;phase&gt;site&lt;/phase&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;site&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-scm-publish-plugin&lt;/artifactId&gt;
                &lt;inherited&gt;false&lt;/inherited&gt;
                &lt;configuration&gt;
                    &lt;checkinComment&gt;Curator website deployment&lt;/checkinComment&gt;
                    &lt;!-- define curator-website-checkout-path in settings.xml --&gt;
                    &lt;checkoutDirectory&gt;${curator-website-checkout-path}&lt;/checkoutDirectory&gt;
                &lt;/configuration&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;id&gt;scm-publish&lt;/id&gt;
                        &lt;phase&gt;site-deploy&lt;/phase&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;publish-scm&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;com.mycila.maven-license-plugin&lt;/groupId&gt;
                &lt;artifactId&gt;maven-license-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;header&gt;src/etc/header.txt&lt;/header&gt;
                    &lt;excludes&gt;
                        &lt;exclude&gt;**/*.confluence&lt;/exclude&gt;
                        &lt;exclude&gt;**/help.txt&lt;/exclude&gt;
                        &lt;exclude&gt;**/*.rdf&lt;/exclude&gt;
                        &lt;exclude&gt;**/.gitignore&lt;/exclude&gt;
                        &lt;exclude&gt;**/*.thrift&lt;/exclude&gt;
                        &lt;exclude&gt;**/*.json&lt;/exclude&gt;
                        &lt;exclude&gt;**/.idea/**&lt;/exclude&gt;
                        &lt;exclude&gt;**/DISCLAIMER&lt;/exclude&gt;
                        &lt;exclude&gt;**/DEPENDENCIES&lt;/exclude&gt;
                        &lt;exclude&gt;**/KEYS&lt;/exclude&gt;
                        &lt;exclude&gt;**/LICENSE&lt;/exclude&gt;
                        &lt;exclude&gt;**/NOTICE&lt;/exclude&gt;
                        &lt;exclude&gt;**/README&lt;/exclude&gt;
                        &lt;exclude&gt;**/CHANGES&lt;/exclude&gt;
                        &lt;exclude&gt;**/RELEASE-NOTES&lt;/exclude&gt;
                        &lt;exclude&gt;**/generated/**&lt;/exclude&gt;
                    &lt;/excludes&gt;
                    &lt;strictCheck&gt;true&lt;/strictCheck&gt;
                &lt;/configuration&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;id&gt;license&lt;/id&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;check&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-release-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;arguments&gt;-Dmaven.test.skip=true&lt;/arguments&gt;
                    &lt;mavenExecutorId&gt;forked-path&lt;/mavenExecutorId&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;

            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.rat&lt;/groupId&gt;
                &lt;artifactId&gt;apache-rat-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;numUnapprovedLicenses&gt;0&lt;/numUnapprovedLicenses&gt;
                    &lt;excludeSubProjects&gt;false&lt;/excludeSubProjects&gt;
                    &lt;excludes&gt;
                        &lt;exclude&gt;**/*.confluence&lt;/exclude&gt;
                        &lt;exclude&gt;**/*.rdf&lt;/exclude&gt;
                        &lt;exclude&gt;**/help.txt&lt;/exclude&gt;
                        &lt;exclude&gt;**/.gitignore&lt;/exclude&gt;
                        &lt;exclude&gt;**/*.thrift&lt;/exclude&gt;
                        &lt;exclude&gt;**/*.json&lt;/exclude&gt;
                        &lt;exclude&gt;**/.idea/**&lt;/exclude&gt;
                        &lt;exclude&gt;**/DISCLAIMER&lt;/exclude&gt;
                        &lt;exclude&gt;**/DEPENDENCIES&lt;/exclude&gt;
                        &lt;exclude&gt;**/KEYS&lt;/exclude&gt;
                        &lt;exclude&gt;**/LICENSE&lt;/exclude&gt;
                        &lt;exclude&gt;**/NOTICE&lt;/exclude&gt;
                        &lt;exclude&gt;**/README&lt;/exclude&gt;
                        &lt;exclude&gt;**/CHANGES&lt;/exclude&gt;
                        &lt;exclude&gt;**/RELEASE-NOTES&lt;/exclude&gt;
                        &lt;exclude&gt;**/generated/**&lt;/exclude&gt;
                    &lt;/excludes&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
    &lt;/build&gt;
&lt;/project&gt;
</pre> 
 <p>&nbsp;</p> 
</div>