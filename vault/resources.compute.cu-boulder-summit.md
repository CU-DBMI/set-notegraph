---
id: jfts4cigy6lsskwk1ps5at3
title: CU Boulder Summit
desc: ''
updated: 1656709205863
created: 1656707430074
---

## Summary

Research Computing (RC) through the University of Colorado Boulder (CU Boulder) provides a supercomputer resource called __Summit__. For more information see the following webpage: <https://colorado.edu/rc/resources/summit>.

## CU Anschutz Access

Those with University of Colorado Anschutz (CU Anschutz) may access the Summit supercomputing resource using an [XCEDE account](https://portal.xsede.org/) and configuration help from RC at UCB via the following email: [rc-help@colorado.edu](mailto:rc-help@colorado.edu).

Use the following guide for more information:
<https://curc.readthedocs.io/en/latest/access/rmacc.html>

Generally, the access sequence is as follows:

```mermaid
sequenceDiagram
    autonumber
    CU Anschutz Requester ->> XCEDE: Create account
    XCEDE-->>CU Anschutz Requester: Ask for Account Validation
    CU Anschutz Requester ->> XCEDE: Validate Account
    CU Anschutz Requester ->> XCEDE: Configure DUO MFA with XCEDE Acct.
    CU Anschutz Requester ->> rc-help@colorado.edu: Request RMACC Summit Authorization with XCEDE Username
    rc-help@colorado.edu -->> CU Anschutz Requester: Authorize RMACC Summit Access
    CU Anschutz Requester ->> Summit: Access Summit
```
