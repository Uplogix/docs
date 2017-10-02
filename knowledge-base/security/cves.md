<!-- 5.4 -->

About **Common Vulnerabilities and Exposures**, from [cve.mitre.org/about/](http://cve.mitre.org/about/)

> Common Vulnerabilities and Exposures (CVE®) is a list of common identifiers for publicly known cyber security vulnerabilities. Use of "CVE Identifiers (CVE IDs)," which are assigned by CVE Numbering Authorities (CNAs) from around the world, ensures confidence among parties when used to discuss or share information about a unique software vulnerability, provides a baseline for tool evaluation, and enables data exchange for cyber security automation.

Listed below are CVEs Uplogix has investigated and/or addressed.

**TIP: ** Use your browser's Find function to quickly jump to a CVE.

# CVE-2014-1491

It was found that NSS accepted weak Diffie-Hellman Key exchange (DHKE) parameters.

Fixed in LMS 5.4

# CVE-2015-8000 <i class='fa fa-fw fa-danger fa-warning'></i> 

A denial of service flaw was found in the way BIND processed certain records with malformed class attributes.

Fixed in LMS 5.4.

# CVE-2015-8704 <i class='fa fa-fw fa-danger fa-warning'></i>
 
A denial of service flaw was found in the way BIND processed certain malformed Address Prefix List (APL) records.

Fixed in LMS 5.4.

# CVE-2016-1285 <i class='fa fa-fw fa-danger fa-warning'></i> 

A denial of service flaw was found in the way BIND processed certain control channel input.

Fixed in LMS 5.4.

# CVE-2016-1286 <i class='fa fa-fw fa-danger fa-warning'></i>
 
A denial of service flaw was found in the way BIND parsed signature records for DNAME records.

Fixed in LMS 5.4.

# CVE-2016-1950 <i class='fa fa-fw fa-danger fa-warning'></i> 

NSS heap-based buffer overflow flaw in ASN.1 parsing of certificates.

Fixed in LMS 5.4.

# CVE-2016-2848 <i class='fa fa-fw fa-danger fa-warning'></i> 

A denial of service flaw was found in the way BIND handled packets with malformed options.

Fixed in LMS 5.4.

# CVE-2016-3081

Apache Struts 2.x before 2.3.20.2, 2.3.24.x before 2.3.24.2, and 2.3.28.x before 2.3.28.1, when Dynamic Method Invocation is enabled, allow remote attackers to execute arbitrary code via method: prefix, related to chained expressions.

Fixed in LMS 5.4.

# CVE-2016-5195 (AKA "Dirty Cow") <i class='fa fa-fw fa-danger fa-warning'></i>

The Local Manager is largely immune to this class of bugs as it neither allows users shell access or allows users to run untrusted code.

The Control Center contains a general purpose OS, so it is vulnerable. By default, only the *emsadmin* user is able to log into the UCC via SSH. If you change the default password, you largely reduce the threat of this class of bugs.

A patch addressing this CVE is available in LMS 5.4.

# CVE-2016-7429 <i class='fa fa-fw fa-danger fa-warning'></i>

A flaw was found in the way ntpd running on a host with multiple network interfaces handled certain server responses. A remote attacker could use this flaw that would cause ntpd to not synchronize with the source.

Fixed in LMS 5.4.1.

# CVE-2016-7433 <i class='fa fa-fw fa-danger fa-warning'></i>

A flaw was found in the way ntpd calculated the root delay. A remote attacker could send a specially-crafted spoofed packet to cause denial of service or in some special cases even crash.

Fixed in LMS 5.4.1.

# CVE-2016-8864 <i class='fa fa-fw fa-danger fa-warning'></i>
 
A denial of service flaw was found in the way BIND handled responses containing a DNAME answer.

Fixed in LMS 5.4.

# CVE-2016-8745 <i class='fa fa-fw fa-success fa-check'></i>

This issue affects the HTTP NIO connector, which is not

CVE-2016-9147: A denial of service flaw was found in the way BIND handled a query response containing inconsistent DNSSEC information. A remote hacker could use this flaw to make the named process exit unexpectedly with an assertion failure via a specially crafted DNS response.
 

# CVE-2017-5664 <i class='fa fa-fw text-success fa-check'></i>

Our products are not vulnerable to this issue, as we override the error page with a JSP, not with a static HTML page which uses the DefaultServlet.