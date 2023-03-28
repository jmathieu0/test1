# D2S Security Operating Procedures (SYOPS) Addendum
```version 1.4```

## Contents

- [Introduction](#a-introduction)
- [Begin](#b-begin)
- [Onboarding](#c-onboarding)
- [Use/Manage](#d-usemanage)
- [Help/Support](#e-helpsupport)
- [Reconsider/Offboard](#f-reconsideroffboard)

# <a name="Introduction">A. Introduction</a>

1. This Addendum __SHALL__ be read in conjunction with the [Defence Digital Foundry SyOps](http://github.com/defencedigital/foundry-syops).

2. [Development Teams](#DevTeams), in addition to following the requirements of the [Defence Digital Foundry SyOps](http://github.com/defencedigital/foundry-syops) __SHALL__ additionally abide by the following:

	a. Each [Development Teams](#DevTeams) __SHALL__ have an application owner. This person __SHALL__ be a Crown servant with seniority not less than OF3/Senior Executive Officer. This person __SHALL__ be accountable to Defence Digital for ensuring the activities of the [Development Team](#DevTeams) overall adhere to the SyOps. Each user __SHALL__ know who their responsible official/officer is. 

	b. D2S' __OFFICIAL__ environments are intended for creating assets with a classification of __OFFICIAL__ (including all caveats) such as source code, comments, markdown files. [Development Teams](#DevTeams) are responsible for ensuring that assets they create or manage using the __OFFICIAL__ environments __SHALL NOT__ have a classification of __SECRET__ or above, based on the [Government Security Classifications](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/715778/May-2018_Government-Security-Classifications-2.pdf) policy. *Note: the classification of code will often be different than the classification of the information it is used to process.*

3. The D2S Service Owner ultimately holds the final decision as to the continued operation/hosting/deployment of any application – either planned or currently in service. In the event that these rules are not complied with, the D2S Service Owner is the ultimate arbitrator to actions required. 

4. All members of a [Development Team](#DevTeams) __SHALL__ be individually registered for access to D2S. Sharing of accounts __SHALL NOT__ be permitted.

# <a name="Begin">B. Begin</a>

1. Devices used to consume D2S __SHALL__ be controlled devices, following the controls specified in Section 2 of the [Defence Digital Foundry SyOps](http://github.com/defencedigital/foundry-syops). These devices __SHOULD__ follow the [Device Security Guidance](https://www.ncsc.gov.uk/collection/device-security-guidance) and use a suitably configured Mobile Device Management system. 

## Source Code Management

2. __Sharing__: [Development Teams](#DevTeams) are reminded of the [Civil Service Code](https://www.gov.uk/government/publications/civil-service-code/the-civil-service-code)’s obligation to “handle information as openly as possible within the legal framework” and that all MOD [Development Teams](#DevTeams) are expected to abide by the Code. In particular, [Development Teams](#DevTeams) are reminded that source code is a Crown asset. [Development Teams](#DevTeams) __SHALL NOT__ keep assets from other teams unless there is a specific and compelling reason to enforce a ‘need to know’ restriction. [Development Teams](#DevTeams) __SHOULD__ construct their assets in such a way as to maximise reuse opportunities, in particular by applying the [Security Considerations when Coding](https://www.gov.uk/government/publications/open-source-guidance/security-considerations-when-coding-in-the-open) in the open guidance and avoiding intellectual property barriers.

3. __Review__: When providing or receiving feedback on code, [Development Teams](#DevTeams) __SHOULD__ respect and value alternative viewpoints and seek, accept and offer honest criticisms of work as required by the Chartered Institute for IT’s [code of conduct](https://www.bcs.org/membership-and-registrations/become-a-member/bcs-code-of-conduct/). 

4. __GitHub__: The following GitHub standards __SHALL__ be followed by all [Development Teams](#DevTeams):

- All repositories are to be set as private or internal
- All commits to a release branch be signed
- Have main as the default branch
- Delete branch on merge
- Have non-empty description (shouldn't be null or "")
- Have issues enabled
- Have recent activity (pushedAt < ?)
- Checks for stored credentials is undertaken prior to commit
- Have branch protection on main, with:
	- Require a pull request before merging
	- Require approvals option and a nominated person to approve the pull request
	- Require review from Code Owners option (2 person check)
	- Include administrators option
	- Have Dependabot enabled 

## Import of [Container](#Containers) Images & Code

5. D2S provides curated [Container](#Containers) Images and access to trusted [Container](#Containers) Image repositories for those built on the platform. If other [Container](#Containers) Images are required, a Service Request __SHALL__ be raised for evaluation and import into the D2S.

## Continuous Integration

6. [Development Teams](#DevTeams), who want to move their workloads to [__D2S Production Environments__](#ProdEnv) using the D2S Security Assurance __SHALL__:

	- Integrate D2S provisioned [Static Application Security Testing (SAST)](#SAST) into their pipelines
	- Integrate D2S provisioned [Dynamic Application Security Testing (DAST)](#DAST) into their pipelines
	- Integrate D2S provisioned Image Scanning for vulnerabilities, configuration weaknesses, license violations and [Software Bill of Materials (SBOM)](#SBOM) generation
	- Ensure [secrets](#Secrets) are held in the D2S Vault

## Fair Usage & Licenses

7. [Development Teams](#DevTeams) are subject to a Fair Usage Policy. If resource usage is forecast to exceed the [Small T-Shirt](#TShirtSize) size model, [Development Teams](#DevTeams) __SHALL__ liaise with the D2S Service Owner in advance. 

8. [Development Teams](#DevTeams) __MAY__ bring onto D2S, third party tools/images as per specified in (Import of [Container](#Containers) Images & Code), and __SHALL__ ensure that any licensing requirements related to them are suitably fulfilled. 

## D2S Security Risk Appetite

D2S operates under Continuous Authority to Operate (CAtO), as such all applications form part of the risk case and are subject to the minimum security risk baseline and controls.

9. D2S has a recognised Security Risk Appetite Statement which is available to [Development Teams](#DevTeams), who __SHALL__ abide by the risk appetite.

# <a name="Onboarding">C. Onboarding</a>

1. [Development Teams](#DevTeams) __SHALL__ use the D2S Self Serve Portal for onboarding and for management of their teams. This can be accessed at: https://d2s.dev.service.mod.gov.uk/

# <a name="UseManage">D. Use/Manage</a>

## D2S Environments

D2S provides the following, supported tools for [Development Teams](#DevTeams) to consume in the [Development Environment](#DevEnv):

- [Kubernetes Platform](#k8s) compliant pipeline
- Vault for credential and [secrets](#Secrets) management
- Digital signing and attestation tooling, for moving [Containers](#Containers) to [D2S Production Environments](#ProdEnv)
- Static Application Security Testing [(SAST)](#SAST)
- Dynamic Application Security Testing [(DAST)](#DAST)
- Software Composition Analysis [(SCA)](#SCA)
- Image scanning including [SBOM](#SBOM) generation

1. D2S [Development Environments](#DevEnv) __SHALL ONLY__ be used for development and prototyping work. Development includes all D2S activities short of integration testing with services or systems in another environment or running production workloads. This __MAY__ include creating and carrying out unit testing, test automation, code creation, code compilation, [alpha prototypes] (https://www.gov.uk/service-manual/agile-delivery/how-the-alpha-phase-works) and performance benchmarking within the assigned namespace(s). For the avoidance of doubt, integration tests and production workloads __SHALL NOT__ be permitted in development environments.

2. Work in [Development Environments](#DevEnv) __SHALL__ use synthetic test data unless approval has been obtained from D2S to do otherwise. Synthetic test data means test records that do not reflect any genuine MOD activity or entities (only the schemata and data formats may be genuine). If the use of production data is required, [Development Teams](#DevTeams) __SHOULD__ generate anonymised data through a process to ensure it is irreversibly anonymised.

3. [Development Teams](#DevTeams) are responsible for the security of their application(s). Any deployed [Containers](#Containers) __MAY__ have internet-exposed end-points which __SHALL__ be secured as necessary. Additionally, [Development Teams](#DevTeams) __SHOULD__  consider the operational resilience of an application, including the backup and recovery of any data.

4. Any workload used to conduct or transact real MOD business or process genuine defence information __SHALL__ constitutes a production workload (regardless of the intended purpose of the environment in which the workload is running). Production workloads __SHALL ONLY__ be run in [D2S Production Environments](#ProdEnv).

5. Production workloads __SHALL__ be digitally signed by D2S and have valid attestations to ensure they have been suitably built and checked, before they can run in [D2S Production Environments](#ProdEnv).

## Security Assurance

6. [Development Teams](#DevTeams) who want to run workloads on D2S [Production Environments](#ProdEnv) using the D2S Security Assurance __SHALL__ complete the D2S Security Assurance questionnaire to begin assurance activity

7. [Development Teams](#DevTeams) __SHALL__ ensure the following before any workload is moved into D2S [Production Environments](#ProdEnv):

	a. They satisfy either the D2S Security Assurance or JSP604 Assurance process; where the JSP604 process has been used, they __SHALL__ provide proof of successful security assurance, including any caveats

	b. Integrate with [DDSOC](#DDSOC), by feeding logs through D2S, for security application monitoring
	
	c. They provide the following information to D2S for production readiness checking:

	- Details of their application, including identification, purpose, High Level Design (HLD), security classification, ownership details and scaling model
	- Application roadmap
	- Chosen & implemented security controls (including indication of inherited controls from D2S)
	- Penetration testing report, where applicable
	- Details of application security logging & monitoring
	- Details of application support & maintenance
	- Risk Assessment and Risk Treatment Plan

## Attestation

8. Before any workload is moved to a D2S [Production Environments](#ProdEnv), [Development Teams](#DevTeams) __SHALL__ ensure that it is digitally signed by D2S and pipeline attestations are captured in the [Container](#Containers) manifest.


# <a name="HelpSupport">E. Help/Support</a>

1. [Development Teams](#DevTeams) __SHALL__ have a documented Through Life Management Plan providing as a minimum:
	- Roles/responsibilities of a Live Support Team, providing technical and user support to application users
	- An Incident Response/Incident Management Plan
	- Performance monitoring and support
	- Processes for managing, responding to and remediating [MODCert](#MODCERT) alerts
	- Processes for managing, responding to and remediating alerts from [DDSOC](#DDSOC)
	- Processes for the through life management of CVEs, including remediation time frames
	- Processes for updating images

2. [Development Teams](#DevTeams) __SHALL__ ensure any security incidents associated with their workloads deployed within D2S, is communicated to the D2S security team as soon as practically possible.


# <a name="ReconsiderOffboard">F. Reconsider/Offboard</a>

1. Application owners __SHALL__ be responsible for ensuring individuals leaving their [Development Team](#DevTeams) have their access to D2S and associated services revoked in a timely manner.

2. [Development Teams](#DevTeams) __SHALL__ liaise with the D2S Team when the platform is no longer required, to avoid unnecessary costs and resource utilisation. 

3. Where a namespace has not been utilised for 30 days or more, the D2S Team will ask the [Development Team](#DevTeams) if the resource is still required. If no response is received, the D2S Team __SHALL__ delete the namespace after 60 days of continuous non-use.

# Requirements Language

The key words "Shall", "Shall Not", "Should", "Should Not" and "May" in this document are to be interpreted as follows:

- <a name="Shall"></a>__SHALL__: This word, means that the definition is an absolute requirement of the policy.
- <a name="Shall_NOT"></a>__SHALL NOT__: This phrase, means that the definition is an absolute prohibition of the policy.
- <a name="Should"></a>__SHOULD__: This word, or the adjective "Recommended", mean that there may exist valid reasons in particular circumstances to ignore a particular item, but the full implications must be understood and carefully weighed before choosing a different course.
- <a name="Should_NOT"></a>__SHOULD NOT__: This phrase, or the phrase "Not Recommended" mean that there may exist valid reasons in particular circumstances when the particular behaviour is acceptable or even useful, but the full implications Should be understood and the case carefully weighed before implementing any behaviour described with this label.
- <a name="May"></a>__MAY__: This word, or the adjective "OPTIONAL", mean that an item is truly optional.


# Definitions

- <a name="Containers">__Containers__</a>: A container in D2S is a package of files that constitutes an executable application that will be run in a target runtime environment. All application components are bundled into a single container for effective management and movement. D2S operates a containerised approach to maximise security and resilience, using a [Kubernetes Platform](#k8s).

- <a name="DAST">__DAST__</a>: Dynamic Application Security Testing. Analysis of an application using simulated attacks to identify security vulnerabilities.

- <a name="DDSOC">__DDSOC__</a>: Defence Digital Security Operations Centre. The department within MOD responsible for D2S monitoring.

- <a name="DevTeams">__Dev Teams__</a>: Any users of D2S who directly, or support in the activities of, application development and application production operations.

- <a name="DevEnv">__Development ('Dev') Environment__</a>: The environment in which all development and testing activities occur, and where tooling can be integrated.

- <a name="MODCERT">__MODCert__</a>: MOD Computer Emergency Response Team. Responsible for incident response and distribution of security notices.

- <a name="k8s">__Kubernetes Platform__</a>: This is an open-source [Container](#Containers) orchestration system for automating software deployment, scaling, and management. Originally designed by Google, the project is now maintained by the Cloud Native Computing Foundation, and is used in all D2S environments.

- <a name="ProdEnv">__Production ('Prod') Environment__</a>: The environment in which applications are deployed to for hosting/operations at either __OFFICIAL__ or __SECRET__ classification. Production is sometimes described with the term ‘live’. For the avoidance of confusion this is not the same as ‘live’ in the meaning of the [Government Service Manual](https://www.gov.uk/service-manual/agile-delivery/how-the-live-phase-works). Services in the [private beta, public beta or live service](https://www.gov.uk/service-manual/agile-delivery/how-the-beta-phase-works) phases as set out in the Manual are all considered to be ‘production’ services.

- <a name="SCA">__SCA__</a>: Software Composition Analysis. Full analysis of an application's supply chain for due diligence.

- <a name="SBOM">__SBOM__</a>: Software Bill of Materials. A full inventory of software components building up the [Container](#Containers).

- <a name="SAST">__SAST__</a>: Static Application Security Testing. Analysis of a [Container's](#Containers) code to identify security vulnerabilities.

- <a name="Secrets">__Secrets__</a>: Any application information that could compromise the security posture, e.g. API keys, credentials, certificates, etc.

- <a name="TShirtSize">__T-Shirt Size__</a>: D2S refers to 'T-Shirt Sizing' when estimating resources required for a [Development Team](#DevTeams). Details of available sizes are provided in the D2S Self Service portal.
				
