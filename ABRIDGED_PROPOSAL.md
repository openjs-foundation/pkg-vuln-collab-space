# Package Vulnerability Management & Reporting

### Champion(s) & Participants

* Darcy Clarke (@darcyclarke)
  * Engineering Manager for the npm CLI & Node.js Collaborator (Package Maintenance & Tooling WGs)
* Wesley Todd (@wesleytodd)
  * Node.js Contributor (Package Maintenance & Web Frameworks WGs)

### Initial Participants

* Darcy Clarke (@darcyclarke)
  * Engineering Manager for the npm CLI & Node.js Collaborator (Package Maintenance & Tooling WGs)
* Wesley Todd (@wesleytodd)
  * Node.js Collaborator (Package Maintenance & Web Frameworks WGs)
* Zbyszek Tenerowicz (@naugtur)
  * Creator of npm-audit-resolver
  * Node.js Contributor (Diagnostics WG)
* Christopher Hiller (@boneskull))
  * Node.js Collaborator & Mocha Maintainer
* Michael Dawson (@mhdawson)
  * OpenJS CPC Member, Node.js Collaborator & TSC Chair
* Dominykas Blyžė (@dominykas)
  * Node.js Contributor (Package Maintenance WG)

> Note: We also plan to reach out to Snyk, HackerOne & GitHub (specifically, the DSP - Data & Security Products - Team) to encourage their participation
Description

Today maintainers deal with a significant influx of issues, PRs (re. updating dependencies) & broader comms when a new CVE is reported on a popular library in our ecosystem. Many of these are being considered "false positives" from an impact/vulnerability perspective. This level of noise creates distrust in the relationships between security companies/researchers, maintainers, & the collective end-users/consumers.

There are numerous examples of this problem & the corresponding frustration it creates in the community; Including but not limited to:

> --- REDACTED ---

By creating a neutral forum to discuss & ideate across this ecosystem's stakeholders, we hope to improve CVE reporting & resolution workflows; Minimizing burden on maintainers & noise for consumers.

Examples of desired or successful outcomes from this discourse/space:

* Improved delineation of domains & controls
* Improved communication between maintainers & security researchers/organizations
* Improved tooling for package auditing, resolution & management as a whole
  * ex. package maintainers have a mechanism to flag/counterclaim vulnerability reports of dependencies that do not affect their own usage/workflows
  * ex. end-users have a mechanism to more granularly control the visibility of the vulnerability reports of their dependencies (including filtering on flags/counterclaims)

### Impact & users of the project

This is a cross-functional effort that we believe impacts the following groups:

* Security Researches/Organizations
* Package Maintainers
* End-users/Consumers

Furthermore, the JavaScript ecosystem, as a whole, will be made better through improvements to this problem space; This is of particular importance to our community due to the deeply interconnected relationships we've created with package dependency trees.

It is worth noting that this work can, & does, extend beyond the scope of the JavaScript ecosystem itself. A key aspect for consideration may be how improvements made here can impact other languages & communities; With that in mind, the applicability/use of what this collaboration space ideates on, as it pertains to - or is relevant to - those other languages & communities, should be considered in the scope of this forum.
Resources

* Creation of a dedicated repository within the openjs-foundation GitHub Organization
* Creation of a channel within the Foundation's Slack Organization
* Use of meeting generation tools to align with existing Foundation best practices
* Use of the Foundation's Zoom & YouTube accounts for streaming
* Marketing support (ex. monthly allotment of re-tweets by the Foundation's Twitter account & support in conducting surveys on this group's behalf)
* Invitation to participate (through email or other comm) sent to Member organizations

### Existing assets

* There is an existing JSON schema created for an `audit-resolve` format which can be considered/utilized as "prior art" in this space (ref. https://github.com/naugtur/audit-resolve-core/blob/master/auditFile/versions/v1.js)
   * This tool is licensed under Apache 2.0

### Proposal Checklist

* [x] Members/space leaders agree to manage the space under open governance
* [x] Work will happen under the OpenJS Foundation IP Policy & use the Apache 2.0 license
* [x] The Collaboration Space will work under the OpenJS CoC
