---
layout: default
title: Data Model
---
# The Combine Data Model


## Overview

Combine’s Data Model can be broken down into the following hierarchy:

Home → Organizations --> RecordGroups --> Jobs --> Records

## Organizations

“Organizations” is the highest layer in the data hierarchy of Combine (equivalent to a ‘Data Provider’ in REPOX). For the typical service hub, an ‘organization’ will correspond to a cultural institution. Combine was designed to be flexible within  a complicated ecosystem of metadata providers and harvesters. 

A single instance of Combine might have two Organizations:

* Foo University
* Bar Historical Society

Organizations contain Record Groups. The Organization “Foo University” would contain all Record Groups shared by Foo University; for example, a Fedora repository, an Omeka instance, and an aggregation of records hosted on behalf of a local historical society.  Regardless of origin, if the Record Groups are all shared by a single institution, they can be logically grouped under the same Organization.

## Record Groups

“Record Groups" are similar to “Data Sets” in REPOX. 

A Record Group is a set of records grouped intellectually. Usually this means they are part of the same collection, but they could also be a set of records from different collections that are grouped together in order to share the same transformation or other process. 

Taking our Foo University example above it would be reasonable to make the Fedora Repository, the Omeka exhibits, and the historical society records each a separate and distinct Record Group, three in all.

Record Groups contain Jobs.

## Jobs

Jobs will be new for anyone accustomed to REPOX.  A Record Group can, and usually does, contain several Jobs. A Job is an action taken on a Record Group and the results of that action. A Job can also be thought of as one step in a series of actions. 

In a typical Record Group, you may see one Job that represents a harvest of records, another for a transformation of those records, and another for a different transformation. One of these jobs will probably be “Published” (meaning, added to Combine’s OAI feed; see “Part 13: Publishing Records” for more). 

To give an example, let’s return to the Record Groups from Foo University and say that their Fedora repository includes a collection of photographs under the name “County Fair.” 

* A harvest of the “County Fair” collection metadata from the Fedora repository’s OAI feed into Combine creates “Job1”
* Transforming Job1 with an XSLT from Combine’s library creates “Job2.”
* Transforming Job1--or Job2--with a different XSLT from Combine’s library creates “Job3”
* “Publishing” Job3 adds it to Combine’s OAI feed so it can be harvested by the DPLA.
* 
Note how an early Job can become an input for later Jobs. 

All the metadata for the “County Fair” collection can be found in each Job, but each set is at a different stage: harvest, transformation, and alternative transformation. Each Job is additive and does not delete or replace the data from an earlier Job unless the user takes special steps to do that. Combine errs on the side of duplicating data in order to preserve a record of provenance or lineage, and to maintain a standard of transparency regarding how and why a Record “downstream” looks the way it does. 

Creating new Jobs while retaining older Jobs gives Combine’s Record Groups a kind of version control. Jobs from earlier harvests can be retained in order to preserve a history of that Record Group. If a problem emerges with a harvest, having older Jobs still available makes it possible to step back to an earlier version of that Record Group until the problem is identified and fixed.

The history of a Record Group might eventually look like this: 

Harvest on  1/1/2020 (Job01) --> Transformation to Service Hub Profile (Job02)
Harvest on  4/1/2020 (Job03) --> Transformation to Service Hub Profile (Job04) 
Harvest on  7/1/2021 (Job05) --> Transformation to Service Hub Profile (Job06)
Harvest on 10/1/2022 (Job07) --> Transform to Service Hub Profile (Job08) (Published)

In this scenario, the Record Group has eight Jobs, but only Job08, the fourth “transformation” Job appears in Combine’s OAI feed.  

There are three types of Jobs: Harvest, Transformation, and Merge/Duplicate.

* Harvest Jobs ingest records from a contributing institution into Combine. A Harvest will typically be the oldest Job in a Record Group because other types of Jobs will use it as input. Harvest Jobs can ingest Records from an OAI feed or a MODS xml file. Harvest Jobs create records in Combine, so they do not have input Jobs.
* Transformation Jobs, unsurprisingly, transform the Records in some way. Currently, Combine supports transformations by XSLT. A Transformation Job can have a single input Job (usually a Harvest), and that input Job must be within the same Record Group. 
* Merge Jobs can merge Records across multiple Jobs. Duplicate Jobs are a variant type that can take all of the Records from a single Job and create a new single Job.

Regardless of type, all Jobs contain Records.

## Record

The most granular level of hierarchy in Combine is a single Record. Records are contained within Jobs.

Each Record’s XML content, and its other attributes, are recorded in MongoDB, while its indexed fields are stored in ElasticSearch.

### Identifiers

A Record has three important identifiers:

* Database ID
** id (integer)
** This is the ObjectID in MongoDB, unique for all Records
* Combine ID
** combine_id (string)
** This is randomly generated for a Record on creation, and is assigned to all other versions of that Record in Combine. It allows the same Record to be linked across Jobs, but is otherwise unique for all Records
* Record ID
** record_id (string)
** Not necessarily unique for all Records, this identifier is used for publishing
** When harvesting from an OAI-PMH feed, this is usually populated from the OAI identifier that came with the Record

























