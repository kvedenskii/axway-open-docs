---
title: API Gateway and API Manager 7.7 <month> 2021 Release Notes
linkTitle: API Gateway and API Manager <month> 2021
draft: true
weight: 100
date: 2021-01-06
---

<!--

This is a template for API Gateway and API Manager 7.7

To use it, copy and paste this file, then rename the file
-->

## Summary

API Gateway is available as a software installation or a virtualized deployment in Docker containers. API Manager is a licensed product running on top of API Gateway, and has the same deployment options as API Gateway.

The software installation is available on Linux. For more details on supported platforms for software installation, see [System requirements](/docs/apim_installation/apigtw_install/system_requirements/).

Docker deployment is supported on Linux. For a summary of the system requirements for a Docker deployment, see [Set up Docker environment](/docs/apim_installation/apigw_containers/docker_scripts_prereqs/).

## New features and enhancements

The following new features and enhancements are available in this update.

### placeholder 1

placeholder text

For more information, see:

* [some reference 1](/docs/placeholder)
* [some reference 2](/docs/placeholder)

### placeholder 2

placeholder text

For more information, see:

* [some reference 1](/docs/placeholder)
* [some reference 2](/docs/placeholder)

## Important changes

<!-- It is important, especially when upgrading from an earlier version, to be aware of the following changes in the behavior or operation of the product in this update.. -->

There are no major changes in this update.

## Deprecated features

<!-- As part of our software development life cycle we constantly review our API Management offering. In this update, the following capabilities have been deprecated. -->

No features were deprecated in this release.

## Removed features

<!-- To stay current and align our offerings with customer demand and best practices, Axway might discontinue support for some capabilities. As part of this review, the following features have been removed: -->

No capabilities have been removed in this update.

## Fixed issues

This version of API Gateway and API Manager includes:

* Fixes from all 7.5.3, 7.6.2, and 7.7 service packs released prior to this version. For details of all the service pack fixes included, see the corresponding *SP Readme* attached to each service pack on [Axway Support](https://support.axway.com).
* Fixes from all 7.7 updates released prior to this version. For details of all the update fixes included, see the corresponding [Release note](/docs/apim_relnotes/) for each 7.7 update.

### Fixed security vulnerabilities

table of security issues

### Other fixed issues

table of other issues

## Known issues

The following are known issues for this update.

| Internal ID | Description   |
| ----------- |  |
| RDAPI-22573 | Service pack update fails with the following message when passphrases are in use: `"Problem connecting to store: Invalid passphrase for configuration"`.                                                                                                                                                                                    |
| RDAPI-16486 | Changes in the mapper always require a reload in the Execute Data Maps filter and once reloaded then providing values for the required parameters must be repeated                                                                                                                                                                          |
| RDAPI-17282 | Connector for Salesforce APIs in API Manager doesn't work or is impossible to configure                                                                                                                                                                                                                                                     |
| RDAPI-18332 | "Try-it" for API-Method is not working                                                                                                                                                                                                                                                                                                      |
| RDAPI-18523 | Inconsistent application search behavior relating to application sharing                                                                                                                                                                                                                                                                    |
| RDAPI-18601 | EMT environmentalization issue                                                                                                                                                                                                                                                                                                              |
| RDAPI-18986 | projpack is unable to merge projects after projupgrade; likely due to Default APIManager policies                                                                                                                                                                                                                                           |
| RDAPI-18990 | "Failed to delete undefined" window pops up unexpectedly when attempting to delete application                                                                                                                                                                                                                                              |
| RDAPI-19292 | When an APIM admin user's login name is changed, the user is directed to a blank page                                                                                                                                                                                                                                                       |
| RDAPI-19293 | API Catalog Try It shows only the first security device of a security profile                                                                                                                                                                                                                                                               |
| RDAPI-19442 | Saving Mode Stuck for the Application Creation in different session                                                                                                                                                                                                                                                                         |
| RDAPI-19601 | Sharing section of Application issue when Organization of application changed                                                                                                                                                                                                                                                               |
| RDAPI-20527 | xml2json filter, unable to use xml with valid namespace syntax                                                                                                                                                                                                                                                                              |
| RDAPI-20593 | Issue with Authentication profiles related to permethod override                                                                                                                                                                                                                                                                            |
| RDAPI-20726 | How to get attribute value for apimgmt.application.id                                                                                                                                                                                                                                                                                       |
| RDAPI-20742 | Inconsistent deletion of Environmentalized Settings                                                                                                                                                                                                                                                                                         |
| RDAPI-20952 | NullPointerException when opening a project with dependencies                                                                                                                                                                                                                                                                               |
| RDAPI-21009 | Issue after updating API Manager settings through rest api if lockUserAccount is missing                                                                                                                                                                                                                                                    |
| RDAPI-21061 | updated error message, OAS3 file import without servers section url                                                                                                                                                                                                                                                                         |
| RDAPI-21171 | Minor UI issue affecting pagination in API keys and Oauth client credentials                                                                                                                                                                                                                                                                |
| RDAPI-21275 | Application default quota in days produces "Cannot instantiate API constraint" error                                                                                                                                                                                                                                                        |
| RDAPI-21295 | XSD files are not downloaded when Use client registry is enabled                                                                                                                                                                                                                                                                            |
| RDAPI-21384 | Webservice (WSDL-based) responds with 500 instead of 405 when an invalid HTTP method is used                                                                                                                                                                                                                                                |
| RDAPI-21411 | Inconsistent treatment of multiple scopes in Oauth request                                                                                                                                                                                                                                                                                  |
| RDAPI-21423 | Quota values getting re-initialized just after clicking quota text box                                                                                                                                                                                                                                                                      |
| RDAPI-21434 | "Expect to Retrieve X rows" setting on database query filter                                                                                                                                                                                                                                                                                |
| RDAPI-21438 | Search box for Applications will not accept certain Unicode characters                                                                                                                                                                                                                                                                      |
| RDAPI-21456 | Application export doesn't include external credential                                                                                                                                                                                                                                                                                      |
| RDAPI-21653 | Custom Property Maximum Size                                                                                                                                                                                                                                                                                                                |
| RDAPI-21675 | API Gateway Manager > Messaging > {Queue}: display issue long name queue                                                                                                                                                                                                                                                                    |
| RDAPI-21680 | Method PATCH not visible api gateway - traffic monitor http filter                                                                                                                                                                                                                                                                          |
| RDAPI-21697 | problems with recent change to multipart form-data RDAPI-20461                                                                                                                                                                                                                                                                              |
| RDAPI-21770 | Incorrect semantics of negated match types like IS_NOT in Compare Attribute filter                                                                                                                                                                                                                                                          |
| RDAPI-21875 | User creation failing under small load                                                                                                                                                                                                                                                                                                      |
| RDAPI-22087 | API Manager - Duplicate header if header is overwritten in inbound security policy                                                                                                                                                                                                                                                          |
| RDAPI-22147 | API Manager GUI - API sorting issue                                                                                                                                                                                                                                                                                                         |
| RDAPI-22197 | Report display issue                                                                                                                                                                                                                                                                                                                        |
| RDAPI-22204 | Wrong documentation on API Manager Swagger/OAS for corsOrigins                                                                                                                                                                                                                                                                              |
| RDAPI-22221 | libxml Error while importing WSDL                                                                                                                                                                                                                                                                                                           |
| RDAPI-22247 | CWE-548 - Static Content Providers default to "Allow directory listings"                                                                                                                                                                                                                                                                    |
| RDAPI-22331 | automated submission form protection for forgottenpassword                                                                                                                                                                                                                                                                                  |
| RDAPI-22333 | OAS 3 import implicitly requires a "servers" object, which should not be mandatory                                                                                                                                                                                                                                                          |
| RDAPI-22430 | Issues removing custom policies from API Manager                                                                                                                                                                                                                                                                                            |
| RDAPI-22442 | Error when saving ENV file in Configuration Studio-Linux                                                                                                                                                                                                                                                                                    |
| RDAPI-22452 | On APIMgr monitoring, application id is displayed instead of application name                                                                                                                                                                                                                                                               |
| RDAPI-22455 | Self crosssite scripting vulnerability in API Manager                                                                                                                                                                                                                                                                                       |
| RDAPI-22459 | Accept header in per-method override is not replacing header                                                                                                                                                                                                                                                                                |
| RDAPI-22599 | APIM does accept colon (:) in query parameter name                                                                                                                                                                                                                                                                                          |
| RDAPI-22624 | API GW audit.log cannot handle UTF-8, unlike trace log.                                                                                                                                                                                                                                                                                     |
| RDAPI-22671 | XPath wizard - Unexpected behavior of 'Evaluate' button                                                                                                                                                                                                                                                                                     |
| RDAPI-22679 | KPS REST API - Stack trace disclosed in error message                                                                                                                                                                                                                                                                                       |
| RDAPI-22756 | No longer able to search applications by ID on API Manager 7.7                                                                                                                                                                                                                                                                              |
| RDAPI-22760 | setting for EMT offload of audit.log files                                                                                                                                                                                                                                                                                                  |
| RDAPI-22763 | Need Support for McAfee Scan Engine 6200                                                                                                                                                                                                                                                                                                    |
| RDAPI-22954 | swagger imports fine, but comes out with error from catalog 2.0 link                                                                                                                                                                                                                                                                        |
| RDAPI-22573 | Service pack update fails with the following message when passphrases are in use: `"Problem connecting to store: Invalid passphrase for configuration"`. As a workaround, you can wait for the purge task, which runs every 10 minutes on the NodeManager process, to remove old gateway configurations before starting the update process. |

### Scripting filter whiteboard attributes not preloaded for Jython scripts

The Scripting filter now uses a Jython 2.7 scripting environment (previously, Jython 2.5) to execute Jython scripts. As a result of this version change, the whiteboard attributes, such as `http.request.uri` and `http.request.verb`, are no longer preloaded for use by Jython scripts. However, you can run a Jython script to load these attributes before they are accessed as follows:

```
from com.vordel.trace import Trace

def invoke(msg):
    msg.forceGenerateAttributes()
    Trace.info("This trace statement was generated in script filter!  [" + str(msg.get("http.request.verb")) + "] [" + str(msg.get("http.request.uri")) + "]")
    return True
```

Related Issue: RDAPI-21363

### When an API Gateway instance is started, Xerces SAXParserImpl writes warnings to the error console

At API Gateway instance startup, the following warnings are logged to the error console, as opposed to the trace log:

```
Warning: org.apache.xerces.jaxp.SAXParserImpl$JAXPSAXParser: Property 'http://javax.xml.XMLConstants/property/accessExternalDTD' is not recognized.
Warning: org.apache.xerces.jaxp.SAXParserImpl$JAXPSAXParser: Property 'http://www.oracle.com/xml/jaxp/properties/entityExpansionLimit' is not recognized.
```

These new properties were added in JAXP 1.5 specification, which is supported by the embedded implementation in the JRE but not supported yet in Xerces-J Apache implementation. These are harmless warning messages, which are written to the error console instead of throwing an exception if a property is not supported by the Apache Xerces-J implementation.

Related Issue: RDAPI-22218

## Update a classic (non-container) deployment

To **update** your API Gateway, see [Update from API Gateway One Version](/docs/apim_installation/apigw_upgrade/upgrade_steps_oneversion/).

To **upgrade** from an older version, see [Upgrade from API Gateway 7.5.x or 7.6.x](/docs/apim_installation/apigw_upgrade/upgrade_steps_extcass/).

## Update a container deployment

Any custom `fed` files deployed to a container must be upgraded using [upgradeconfig](/docs/apim_installation/apigw_upgrade/upgrade_analytics#upgradeconfig-options) or [projupgrade](/docs/apim_reference/devopstools_ref#projupgrade-command-options). They must be upgraded the same way, regardless of whether they are API Manager enabled or not.

The `fed` now contains the updates for the API Manager configuration and can be used to build containers.

## Documentation

<!-- This section describes documentation enhancements and related documentation. -->

There are no major changes in this update.

### Related documentation

To find all available documentation for this product version:

1. Go to [Manuals on the Axway Documentation portal](https://docs.axway.com/bundle).
2. In the left pane Filters list, select your product or product version.

Customers with active support contracts need to log in to access restricted content.

The following reference documents are also available:

* [Supported Platforms](https://docs.axway.com/bundle/Axway_Products_SupportedPlatforms_allOS_en) - Lists the different operating systems, databases, browsers, and thick client platforms supported by each Axway product.
* [Interoperability Matrix](https://docs.axway.com/bundle/Axway_Products_InteroperabilityMatrix_allOS_en) - Provides product version and interoperability information for Axway products.

## Support services

The Axway Global Support team provides worldwide 24 x 7 support for customers with active support agreements.

Email [support@axway.com](mailto:support@axway.com) or visit [Axway Support](https://support.axway.com/).

See [Get help with API Gateway](/docs/apim_administration/apigtw_admin/trblshoot_get_help/) for the information that you should be prepared to provide when you contact Axway Support.