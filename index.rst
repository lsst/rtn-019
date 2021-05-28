..
  Technote content.

:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. TODO: Delete the note below before merging new content to the master branch.

.. note::

   **This is a SQuaRE delivery note covering use of the Science Platform in Observatory Operations (not the Data Facilities).**

   A Delivery Note is being used to transition a service (or other codebase) from Rubin Construction to Operations in situations where the service is not covered by a requirements document, is not part of the observatory operational readiness milestone, or otherwise lacks a formal process of delivery.

   Its purpose is to document the transition so as to allow Ops-funded developers to continue to maintain and evolve the service, and to allow the service's deployment costs to be covered by Ops infrastructure or funding. It can also be used to describe responsibilities for the service when not a direct continuation of the model used in construction.

   The process is complete when the relevant AD(s) and/or Director reviews the note and the note is published (merged to master).

   **Engineering review:** Michael Reuter

   **Management review:** Wil O'Mullane, Chuck Claver and Bob Blum

.. Add content here.

Scope
=====

The scope of this Delivery Note is usage of the Rubin Science Platform (including) associated infrastructure for observatory operations, including (but not limited to) control of the observing queue, analysis and visualisation of incoming telescope data and analsysis of telemetry and other quantities stored in the Engineering Facilities Database.

The usage of the RSP in this way is "off-requirements".
The Construction project had a need for interim tooling at the summit pending delivery of other planned components, and so the RSP (in particularly the notebook service nublado) was opportunistically offered as a way to fill in that gap.
After more than a year of operating in this mode, it has become apparent that the summit RSP is here to stay as it provides both useful tools for the ad-hoc analysis of observatory data as well as deployment infrastructure that can be utilised by other observatory components.

Specifically, the scope is the operation and support of Science Platform clusters in what is informally referred to as the "telescope" (as opposed to "science") deployments:

* At the summit
* At the La Serena Base
* At the various engineering Teststands (currently at NCSA and Tucson)


Artifacts (code, docs, infrastructure) involved in this delivery
----------------------------------------------------------------

The usage of the RSP for the telescope deployments is largely "as-is" in terms of features and services.
No new requirements or usecases have been placed on the feature list as a result, although we have had to make some infrastructure changes to allow it to be effective in the summit/engineering environments.

None of the data publication services (API service) are in use at the telescope deployments.
The services exercised heavily are:

- The notebook aspect (https://github.com/lsst-sqre/nublado2)
- The portal aspect and the related Firefly JupyterLab plugin
- The umbrella app/landing page (https://github.com/lsst-sqre/charts/tree/master/charts/squareone)
- Infrastructure services underpinning the platform, such as (but not limited to):
    - deployment configuration (https://github.com/lsst-sqre/phalanx)
    - authentication and authorisation (https://github.com/lsst-sqre/gafaelfawr)
    - certificate management
    - ingres
    - deployment infrastructure

There are two significant differences between the "stock" Science Platform science deployments and the telescope deployments:

- The notebook service containers need to support multicast in order to integrate with the summit control network, as one of the usecases involves interfacing to CSCs from the notebook environment
- Unlike the science deployments, where we consume containers we build within our own subsystem, for the telescope deployments we consume containers built by Telescope & Site.


Site specific configurations for the telescope deployments of the science platform can be found here:

- https://github.com/lsst-sqre/phalanx/blob/master/science-platform/values-summit.yaml
- https://github.com/lsst-sqre/phalanx/blob/master/science-platform/values-base.yaml
- https://github.com/lsst-sqre/phalanx/blob/master/science-platform/values-nts.yaml
- https://github.com/lsst-sqre/phalanx/blob/master/science-platform/values-tucson-teststand.yaml

Deployment and configuration documentation is at https://phalanx.lsst.io

Potential costs
---------------

There are no direct costs associated with providing this service.
We utilise Github features that are free to us under our open source status.
The services are deployed on on-premises compute at Cerro Pachon, La Serena, NCSA, and Tucson.


Ongoing support
---------------

Support is offered to observatory staff on the #com-square Slack channel.

Work is co-ordinated through the appropriate meeting (currently the Comissioning Activities Project or CAP meeting) and carried out according the process outlined in https://sqr-056.lsst.io


Handover
========

Delivering team
----------------

SQuaRE, with contributions from the SUI/IPAC team.

Receiving Operations team
--------------------------

SQuaRE (as the SUI/IPAC effort is part of SQuaRE in the Ops WBS)

Authorization or asset transfer
-------------------------------

None required.

Known Issues
============

There are no current issues affecting service.

Additional Notes
================

Authentication
--------------

There are two currently implemented ways of authenticating (establishing user identity) to the Science Platform, as supported by the A&A service (gafaelfawr).

These are:
- CILogon, in this case tied to the NCSA identity LDAP
- Github tied to specific teams, in this case https://github.com/orgs/rubin-summit/teams/rsp-access among others.

Our summit IT team is planning on providing us with an OAuth2 service backed the FreeIPA identity service.
When this is available, work will be needed to interface to that service, which will allow us to operate the summit instance in the absence of external network.
This work can be better prioritised as part of Operations, since it is not part of Construction delivery.

Telescope & Site Build/Release
-------------------------------

This service consumes containers built by Telescope & Site (in Operations, Observatory Operations) and SQuaRE collaborates with the Telescope & Site release co-ordinator and scientist on adding the JupyterLab layer on top of those containers for the notebook service (nublado). We occasionally meet to resolve issues across (or about) our interface, eg https://confluence.lsstcorp.org/display/DM/2021-04-14+Build+Workshop

Visual Identity
---------------

The theming elements of Square One, the umbrella application for RSP users, contains visual identity elements.
Co-ordination is required with the Rubin visual identity team.



.. Do not include the document title (it's automatically added from metadata.yaml).



.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
