---
tags:
  - PenetrationTesting
  - Reporting
  - StandardInformation
---
## Common Vulnerabilities and Exposures (CVE)

[Common Vulnerabilities and Exposures (CVE)](https://cve.mitre.org/) is a publicly available catalog of security issues sponsored by the United States Department of Homeland Security (DHS). Each security issue has a unique CVE ID number assigned by the CVE Numbering Authority (CNA). The purpose of creating a unique CVE ID number is to create a standardization for a vulnerability or exposure as a researcher identifies it. A CVE consists of critical information regarding a vulnerability or exposure, including a description and references about the issue. The information in a CVE allows an organization's IT team to understand how detrimental a problem could be to their environment.

The following chart explains how a CVE ID may be assigned to a vulnerability. Any vulnerabilities assigned a CVE must be independently fixable, affect just one codebase, and be acknowledged and documented by the relevant vendor.

![qualifications](https://academy.hackthebox.com/storage/modules/108/cve/VulnerabilityAssessment_Diagram_01.png) _Adapted from the original graphic [here](https://www.balbix.com/app/uploads/what-is-a-CVE-1024x655.png)._

---

## Stages of Obtaining a CVE

#### Stage 1: Identify if CVE is Required and Relevant

Identify if the issue found is a vulnerability. According to the CVE Team, "A vulnerability in the context of the CVE Program is indicated by code that can be exploited, resulting in a negative impact to confidentiality, integrity, OR availability, and that requires a coding change, specification change, or specification deprecation to mitigate or address." Additionally, research should verify there is not a CVE ID already in the CVE database.

#### Stage 2: Reach Out to Affected Product Vendor

A researcher should ensure they have made a good faith effort to contact a vendor directly. Researchers can reference CVE's [Documents on Disclosure Practices](https://cve.mitre.org/cve/researcher_reservation_guidelines#appendix#a) for additional information.

#### Stage 3: Identify if Request Should Be For Vendor CNA or Third Party CNA

If a company is a part of participating CNA's, they can assign a CVE ID for one of their products. If the issue is for a participating CNA, researchers can contact the appropriate CNA organization [here](https://cve.mitre.org/cve/request_id.html). If the vendor is not a participating CNA, a researcher should attempt to reach out to the vendor's third-party coordinator.

#### Stage 4: Requesting CVE ID Through CVE Web Form

The CVE Team has a form that can be filled out online [here](https://cveform.mitre.org/) if the methods above do not work for CVE requests.

#### Stage 5: Confirmation of CVE Form

Upon submitting the CVE Web Form mentioned in Stage 4, an individual will receive a confirmation email. The CVE team will contact the requestor if any additional information is required.

#### Stage 6: Receival of CVE ID

Upon approval, the CVE Team will notify the requestor of a CVE ID if the affected product's vulnerability is confirmed. Please note that the CVE ID is not public yet at this stage.

#### Stage 7: Public Disclosure of CVE ID

CVE IDs can be announced to the public as soon as appropriate vendors and parties are aware of the issue to prevent duplication of CVE IDs. This stage ensures that all associated parties are aware of the problem before being publicly disclosed.

#### Stage 8: Announcing the CVE

The CVE Team asks researchers who are sharing multiple CVEs to ensure each CVE indicates the different vulnerabilities. Additional information can be found [here](https://cve.mitre.org/cve/researcher_reservation_guidelines).

#### Stage 9: Providing Information to The CVE Team

At this stage, the CVE Team asks that the researcher help provide additional information to be used in the official CVE listing on the website. The [U.S. National Vulnerability Database (NVD)](https://nvd.nist.gov/) maintains this information online in their database as well.