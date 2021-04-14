---
title: 1.1.1 Obit Formula
nav_order: 4
parent: The OBADA Standard 
---
## 1.1.1 Obit Formula

### Obit Formula

Identifying the physical asset.

### Current practice in asset disposition

There is no standard way for a processor of electronic devices to generate unique identifiers for their inventory. No standard identifiers for manufacturers or part-numbers/models are in use. Serial numbers are not unique across manufacturers, or even within manufacturers.

The minimum requirement for generating uniqueness across all electronics devices necessitates a combination of three fields: manufacturer, part(model), and serial number. Concatenating these three is the minimum viable method used by inventory systems in asset disposition today.

Obada applies a hashing algorithm to this concatenation to create a cryptographic identifier.

So any inventory system used in asset disposition can easily self-generate OBIT DIDs by running a little math on top of their existing system.

### Obit Version 1.0 Generation

The following instructions are for creating a general purpose OBIT DID for any category of product. For assets and asset classes that have pre-established immutable identifiers, see below.

appropriate identifiers already. pre-established identifiers To create an OBIT-DID:
1. serial_hash = sha256(serial_number) 2. obit = sha256(manufacturer + part_number + serial_hash)

    >OBIT asset hash = SHA-256(mp(SHA-256(sn))

1. Prepend 4 character “Obit Formula Version”
  1. See version list.
  2. If no version identifier, assume default (version 1)
2. Append 4 character checksum
  1. 4 digit checksum.  
  2. checksum method needs to be defined

The final OBIT-DID, with versioning and a checksum.

>OBIT-DID=version-assetHash-checksum

Examples:
+ MPSN hash: ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785
+ Formula version:  0000 
+ Checksum: 1234
+ OBIT DID =  0000ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee481234

### OBIT DID Elaborations
+ hyphens
  + Use of hyphens to separate version and checksum is optional. 
  + Services that parse the OBIT-DID should provide support for both hyphenated and non-hyphenated versions.
+ DID type identification
  + Appending the DID type (i.e. “OBIT-abcde12345” vs “abcde12345” is also optional.
+ DID elaborations can be added to assist with readability, primarily for development purposes and ongoing debugging.   Elaborations are recommended even in production, unless maximum obfuscation is an absolute necessity.  (see “1.? Elaborations)
+ Examples with Elaborations:
  + 0000-ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48-1234
  + OBIT-0000-ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48-1234

### Asset Categories with pre-established unique identifiers.

Some types of devices already have a unique ID, that is not considered the serial number. Only one asset class has been approved to date.

1. Automobiles
  - Automobiles have a VIN.   The VIN is already unique.  
  - In the case of automobiles, the “asset hash” is just the VIN.  No hashing is necessary.
  - So the OBIT DID for an auto is version-VIN-checksum

Other asset classes have been discussed but none have been approved.
+ Mobile Devices
  - The suggestion has been to  use IMEI as the UID.  However, dual-sim and virtual-sim phones create problem with this approach.
+ Networking Devices
  - The suggestion has been made to use the Mac Address as UID, and to concatenate and hash all Mac addresses if there are  multiple.   Needs ratification
+ Telecom 
  - Use CLEI codes (14 digit unique codes).  Needs ratification

### Obit Formula Versions
  >(insert version list and text from versions slide)

### Manufacturer Identifier

The mpsn formula specifies to concatenate the manufacturer name, but there are no common standards used for identifying a manufacturer. The industry shares csv files of inventory lists using names like “Dell, Dell Computer, Dell Inc” interchangeably, requiring complicated data cleansing mechanism inside of industry systems to identify them.

Because these systems are often based around ecommerce, the manufacturer names given often align with Google’s structured data requirements, for SEO, as specified in Schema.org.

### Manufacturer Name Format

+ The manufacturer name  should adhere to Schema.org / good relations,  as specified on the authoritative wikipedia URL page.

### Wikipedia slugs are the manufacturer identifier

+ https://www.wikipedia.org/wiki/**dell**​
+ https://www.wikipedia.org/wiki/**apple**​
+ https://www.wikipedia.org/wiki/**intel**​
  + This is perhaps the most decentralized solution possible, and a method which data cleansing systems can automatically check.

### Wikipedia Slug not found
+ If the manufacturer cannot be found via schema.org, use the manufacturer domain name, without the TLD.
  + i.e.  Dell because www.DELL.com

### Manufacturer Data Format
+ Manufacturer names (wikipedia slug name) should be lower cased prior to hashing.

### Part Number / Model
Obada defines “part number” as the lowest-level of device type identification available. System “models” are often further classified by part numbers to specific their configuration options. But some manufacturers do not distinguish between part and model. If only model is available, use that, otherwise use the more exact of the two. (e.g. use the one you’d need to order the exact same device again)

### Part Number Format
+ For “part number”: use the most exact identifier available

### Data Cleansing & Case Sensitivity
Part numbers often come with many variations such as 01-abcde, 01/abcde, or 01abcde.
  + The part number field should be trimmed, and all punctuation should be stripped, prior to hashing.

All characters should be UPPER cased. check… lower?

<code>insert list of characters to exclude</code>

### Serial Number
Serial number must be entered exactly as provided by the manufacturer. Do not alter or change the format in any way.

### .obada-standard/2-content-archive/1-information-architecture/1-obits/obit-formula


## | [Previous: Table of Contents](tableofcontents) |         | [Next: Participants](Participants) |
