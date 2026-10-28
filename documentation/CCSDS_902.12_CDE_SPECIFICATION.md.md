# CCSDS 902.12-M-1 & CSS-SM Common Data Entities (CDE) Specification

## Executive Summary

This document provides the technical specification and architecture for **CDEForge Pro**, an industrial aerospace workstation implementing the **Consultative Committee for Space Data Systems (CCSDS) 902.12-M-1** Recommended Practice (*Cross Support Service Management—Common Data Entities*, Magenta Book, Issue 1, February 2021\) and **ISO Cross Support Service Management (CSS-SM)**.

In space communications cross-support, multi-agency exchanges (NASA, ESA, JAXA, ISRO, MBRSC, commercial networks) require consistent, unambiguous definitions for foundational data types. The **Common Data Entities (CDE)** standard specifies the normative schemas for Information Entity Headers, space link resources, RF carrier frequencies and power envelopes, temporal intervals, antenna polarizations, modulations, and disposition diagnostics utilized throughout CSS-SM specifications.

---

## 1\. CSS-SM Foundational Architecture

\+-------------------------------------------------------------------------+

\|                  CCSDS CSS-SM SERVICE LIFECYCLE                         \|

\+-------------------------------------------------------------------------+

\|  Service Catalog (SECA)            \|  CCSDS 902.7-M-1 \[\#488\]            \|

\|  Service Agreement & Profiles      \|  CCSDS 902.5-B-1 (SACP) \[\#486\]     \|

\|  Communications Planning           \|  CCSDS 902.2-B-1 (CPIF) \[\#482\]     \|

\|  Service Utilization Request       \|  CCSDS 902.9-B-1 (SMURF) \[\#485\]    \|

\|  Simple Schedule Agreement         \|  CCSDS 902.1-B-1 (SSF)  \[\#481\]     \|

\|  Service Package Provisioning      \|  CCSDS 902.4-B-1 (SPDF) \[\#483\]     \|

\|  Event Sequence Execution          \|  CCSDS 902.6-B-1 (EVSQ) \[\#484\]     \|

\|  Service Accounting                \|  CCSDS 902.8-B-1 (SMAC) \[\#487\]     \|

\+-------------------------------------------------------------------------+

\|  FOUNDATIONAL DATA MODELS:                                              \|

\|   • Abstract Event Definition (AED)\|  CCSDS 902.13-M-1 \[\#489\]           \|

\|   • Common Data Entities (CDE)     \|  CCSDS 902.12-M-1 \[\#490\] \<---------\|

\+-------------------------------------------------------------------------+

---

## 2\. Common Data Entities Data Model

A Common Data Entity structure defines:

1. **Service Management Information Entity Header**:  
   - `entityIdentifier`: Globally unique XML ID string (`CDE-DOC-YYYY-Wxx-xxx`).  
   - `originatorId`: Sending mission or ground station entity (`LUNAR_GATEWAY_MOC`).  
   - `recipientId`: Target ground tracking network entity (`NASA_DSN_OPERATIONS`).  
   - `generationTime`: Strict ISO 8601 UTC timestamp (`YYYY-MM-DDTHH:MM:SS.sssZ`).  
   - `standardVersion`: Version descriptor (`1.0`).  
2. **Resource Descriptors**:  
   - `SpacecraftIdentifier`: SANA Spacecraft ID / SCID.  
   - `GroundStationIdentifier`: SANA ground network aperture (`NASA_DSN_DSS24`, `ESA_ESTRACK_NNO1`).  
   - `AntennaIdentifier`: Dish name and physical diameter (\$\\ge 34.0\$ meters).  
3. **RF Descriptors**:  
   - `CarrierFrequency`: Carrier frequency represented in Hertz (\$10^6\$ to \$10^{11}\$ Hz).  
   - `Power`: Transmitter RF power in Watts and kW (\$\\le 100\$ kW).  
   - `EIRP`: Effective Isotropic Radiated Power in dBW.  
   - `Polarization`: Normative modes (`RHCP`, `LHCP`, `DUAL_CIRCULAR`, `LINEAR_H`, `LINEAR_V`).  
   - `Modulation`: Standard deep-space schemes (`PCM/PSK/PM`, `BPSK`, `QPSK`, `OQPSK`).  
4. **Temporal Interval Descriptors**:  
   - `startTime` and `stopTime`: Absolute UTC interval boundaries.  
   - `durationSeconds`: Non-negative duration interval (\$\\ge 0.0\$ seconds).  
5. **Disposition & Diagnostic Entities**:  
   - `DispositionState`: `ACCEPTED`, `REJECTED`, `FEASIBLE`, `SCHEDULED`, `CANCELLED`.  
   - `DiagnosticCode`: Alphanumeric diagnostic category.  
   - `DiagnosticMessage`: Human-readable explanation.

---

## 3\. Bilateral Serialization Formats (§5)

- **SANA XML Schema**: Conforms to official SANA CSS-SM schema `902x12m1-SmCmnEnt.xsd` (`urn:ccsds:schema:csssm:cde`).  
- **Key-Value Notation (KVN)**: Structured ASCII key-value mapping for automated tracking network ingestion.