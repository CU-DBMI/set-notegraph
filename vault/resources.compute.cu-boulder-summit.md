---
id: jfts4cigy6lsskwk1ps5at3
title: CU Boulder Summit
desc: ''
updated: 1659740151159
created: 1656707430074
---

## Summary

Research Computing (RC) through the University of Colorado Boulder (CU Boulder) provides a supercomputer resource called __Summit__. For more information see the following webpage: <https://colorado.edu/rc/resources/summit>.

## CU Anschutz Access

|__:warning: PLEASE NOTE__|
|:---------------------------|
| :exclamation: XSEDE SSO access will be discontinued as of 8/31/2022 ([see here](https://portal.xsede.org/web/advancetoaccess/-/important-information-for-access-resource-providers?redirect=https%3A%2F%2Fportal.xsede.org%2Fweb%2Fadvancetoaccess%2Fhome%3Fp_p_id%3D101_INSTANCE_GGZQtbM1Lixt%26p_p_lifecycle%3D0%26p_p_state%3Dnormal%26p_p_mode%3Dview%26p_p_col_id%3D_118_INSTANCE_PAjp68kDKWMl__column-1%26p_p_col_count%3D1)). Further details concerning accessing this resource are forthcoming from Research Computing. |

Those with University of Colorado Anschutz (CU Anschutz) may access the Summit supercomputing resource using an [XSEDE account](https://portal.xsede.org/) and configuration help from RC at UCB via the following email: [rc-help@colorado.edu](mailto:rc-help@colorado.edu).

Use the following guide for more information:
<https://curc.readthedocs.io/en/latest/access/rmacc.html>

Generally, the access sequence is as follows:

```mermaid
sequenceDiagram
    autonumber
    CU Anschutz Requester ->> portal.xsede.org: Create account
    portal.xsede.org-->>CU Anschutz Requester: Ask for Account Validation
    CU Anschutz Requester ->> portal.xsede.org: Validate Account
    CU Anschutz Requester ->> portal.xsede.org: Configure DUO MFA with XSEDE Acct.
    CU Anschutz Requester ->> rc-help@colorado.edu: Request RMACC Summit Authorization with XSEDE Username
    rc-help@colorado.edu -->> CU Anschutz Requester: Authorize RMACC Summit Access
    CU Anschutz Requester ->> login.xsede.org: local $ ssh -l <username> login.xsede.org
    CU Anschutz Requester ->> Summit: xsede $ gsissh rmacc-summit
```
