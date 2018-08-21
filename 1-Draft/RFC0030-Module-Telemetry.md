--
RFC: RFC0030
Author: Michael Greene
Status: Draft
SupercededBy: 
Version: 0.1
Area: Modules
Comments Due: 9/30/2018
Plan to implement:
---

# Module Telemetry

The PowerShell Community regularly contributes new modules for public consumption.
Maintainers of these modules have no standardized method of gaining insight
in to how their work is being used.
They can make some inference based on download count,
but this does not help them to understand specific feature usage.

The purpose of this RFC is to solicit community feedback regarding a solution.

This Request for Comments includes all types of PowerShell modules
including those containing DSC resources.

## Motivation

    As a maintainer of a PowerShell module,
    I can understand how my work is used,
    so that I can better understand where to invest my time.

## Specification

It would be good if the solution follows at least the following guidelines:

 - Never collect personally identifiable information
 - Data should be publicly available for 30 days
 - On by default
 - Allow users to "opt out" on a per-module and/or per-machine basis
 - Provide a framework that can be easily cloned in to any project
 - Enable insight at the Function level of granularity

It is currently unknown:

 - How many module maintainers would like to enable telemetry in their work
 - How many consumers of PowerShell modules would "opt out"
 - What the timeline would be to prioritize such an effort if the community is interested

Brainstorming/References:

PowerShell Core has an existing
[telemetry solution](https://github.com/powershell/powershell#telemetry)
that could serve as a starting point.
This solution sends minimal data to
[Azure Application Insights](https://azure.microsoft.com/en-us/services/application-insights/)
that is presented via a 
[PowerBI dashboard](https://msit.powerbi.com/view?r=eyJrIjoiYTYyN2U3ODgtMjBlMi00MGM1LWI0ZjctMmQ3MzE2ZDNkMzIyIiwidCI6IjcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0NyIsImMiOjV9&pageName=ReportSection5).

It is unclear how a dashboard would be built to represent a view of any module.
One consideration could be attempting to integrate a reporting interface
in to the PowerShell Gallery.
This would enrich the search experience so someone looking for great modules
would have an opportunity to see how much Functions are used after they are downloaded.

If there are examples of how other languages integrate telemetry, feedback would be appreciated.

## Alternate Proposals and Considerations
