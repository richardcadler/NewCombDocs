# Introduction

## Overview

Combine is an application to facilitate the harvesting, transformation, analysis, and publishing of metadata records by Service Hubs for inclusion in the Digital Public Library of America (DPLA). Installing and maintaining Combine requires the skills of a web administrator, but users of Combine will not need a technical background to work with metadata. 

The name “Combine”, pronounced /kämˌbīn/ with a long i, is a nod to the combine harvester used in farming for, “combining three separate harvesting operations - reaping, threshing, and winnowing - into a single process.” Instead of grains, we have metadata records! These metadata records may come in a variety of metadata formats, various states of transformation, and may or may not be valid in the context of a particular data model. Like the combine equipment used for farming, this application is designed to provide a single point of interaction for multiple steps along the way of harvesting, transforming, and analyzing metadata in preparation for inclusion in the DPLA.

## Things You Need to Know Before Installing Combine

Combine is not a simple application. It requires a working knowledge of several server components, dependencies, and configurations that must be in place to work. 

It leverages Apache Spark, among other applications, for processing on the backend.

The current version of Combine, called combine-docker, has simplified the installation process by leveraging docker. This version is available in the MI-DPLA github directory: https://github.com/MI-DPLA/combine-docker. It is recommended to have a system administrator experienced with linux and web servers install Combine.

## Table of Contents

Part 1: Introduction (this page)
Part 2: Installation and Server Maintenance
Part 3: Command Line
Part 4: Background Tasks
Part 5: Date Model
Part 6: Configuration
Part 7: Running Jobs
Part 8: Harvesting Records
Part 9: Transforming Records
Part 10: Merging Records
Part 11: Validation
Part 12: Job Results and Record Details
Part 13: Publishing Records
Part 14: Exporting
Appendix: Deprecated Features

## The Current State of Combine

Recent development work on Combine has focused on its essential core functionality. As of March 2022, Combine is a reliable application for preparing and managing metadata for DPLA harvests. 

Some features of Combine have since become deprecated due to fixes, updates, and improvements in other areas. Documentation for these features was moved to an appendix during the 2022 revision. Combine’s functionality would be enhanced by bringing these features up to date, but they were not deemed essential to the core functionality of Combine during its recent development. We hope that future teams will revisit these deprecated features someday and make them part of Combine’s workflows..



