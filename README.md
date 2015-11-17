
# Rackspace Cloud DNS API Documentation

[![Build Status](https://travis-ci.org/rackerlabs/docs-cloud-dns.svg?branch=master)](https://travis-ci.org/rackerlabs/docs-cloud-dns)


## Resources

This github repository contains the source files for the following Rackspace Cloud DNS v1.0 API documentation:

* [Cloud DNS Getting Started Guide](http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/)
* [Cloud DNS Developer Guide](https://developer.rackspace.com/docs/cloud-dns/v1/developer-guide/)
* [Cloud DNS Release Notes](https://developer.rackspace.com/docs/cloud-dns/v1/developer-guide/#document-release-notes)

This github repository also contains the source files for the Rackspace Managed DNS v2.0 API documentation

## Contributing

Contributions are welcome! To suggest changes to the documentation, submit an [issue](https://github.com/rackerlabs/docs-cloud-dns/issues) or [pull request](https://github.com/rackerlabs/docs-cloud-dns/pulls).

To make changes to a project, create your own fork of the project and send a pull request to have your changes reviewed and merged into the master branch as appropriate.

### Building from Source

This repository uses Maven to generate the output documentation. Command line users can generate the complete output from this repository by using the following command:

mvn clean generate-sources

The output appears in PDF and HTML form in the following locations. The items in the **Name** column link to the location where the documentation is published, when available.

| Name | Build Location |
| --- | --- |
| [Getting Started Guide v1](http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/) | target/docbkx/webhelp/cdns-getting-started-external |
| [Developer Guide v1](http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/) | target/docbkx/webhelp/cdns-devguide-external |
| [Release Notes v1](http://docs.rackspace.com/cdns/api/v1.0/cdns-releasenotes/) | target/docbkx/webhelp/cdns-releasenotes-external |
| Developer Guide for Service Management v1 (Internal) | target/docbkx/webhelp/cdns-mgmt-devguide-internal |
| Release Notes v1 (Internal) | target/docbkx/webhelp/cdns-releasenotes-internal |
| [Getting Started Guide v2](http://docs-internal.rackspace.com/cdns/api/v2/cdns-getting-started-2/content/DNS_Overview.html) | target/docbkx/webhelp/cdns-getting-started-2-internal |
| [Developer Guide v2](http://docs-internal.rackspace.com/cdns/api/v2/cdns-devguide-2/content/overview.html) | target/docbkx/webhelp/cdns-devguide-2-internal |
| [Release Notes v2](http://docs-internal.rackspace.com/cdns/api/v2/cdns-releasenotes-2/content/doc_change_history.html) | target/docbkx/webhelp/cdns-releasenotes-2-internal |

#### Editors

You can use any text editor to work with these source files. If you want to use an IDE, consider [NetBeans](http://netbeans.org). This cross-platform IDE offers seamless support for Maven projects and does not require  additional configuration to open the **pom.xml** file as a project. You can configure the project so that the **Build** command, which appears when you right-click a project in the **Projects** pane, executes the `clean generate-sources` command. To do so, perform the following steps:

1. Right-click the project in the **Projects** window and select **Properties**.
2. Select the **Build** category in the left pane, and then select the **Build project** action in the right pane.
3. Change **Execute Goals** to `clean generate-sources`
4. *(Optional)* Repeat steps 2 and 3 for the **Clean and Build project** and **Build with Dependencies** actions.

### Quick Links

The files that are most likely to be of interest are:

Cloud DNS v1.0:

* [src/main/resources/cdns-getting-started.xml](src/main/resources/cdns-getting-started.xml)
* [src/main/resources/cdns-devguide.xml](src/main/resources/cdns-devguide.xml)
* [src/main/resources/wadl/dns.wadl](src/main/resources/wadl/dns.wadl)

Managed DNS v2.0

* [src/main/resources/cdns-getting-started-2.xml](src/main/resources/cdns-getting-started-2.xml)
* [src/main/resources/cdns-devguide-2.xml](src/main/resources/cdns-devguide-2.xml)
* [src/main/resources/wadl/dns_with_rax_roles-2.wadl](src/main/resources/wadl/dns_with_rax_roles-2.wadl)

If you want to make changes to the example files referenced in the v1 WADL file, you can find the example files at [src/main/resources/samples](src/main/resources/samples).

If you want to make changes to the example files referenced in the v2 WADL file, you can find the example files at [src/main/resources/samples](src/main/resources/samples-2).

The status codes referenced by the v1 WADL file are at [src/main/resources/wadl/common.ent](src/main/resources/wadl/common.ent).

The status codes referenced by the v2 WADL file are at [src/main/resources/wadl/common.ent](src/main/resources/wadl/common.ent).

