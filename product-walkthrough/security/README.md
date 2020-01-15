---
description: Defining how Reblaze processes your traffic
---

# Security

This section defines the parameters with which Reblaze scrubs traffic. 

The user interface is divided into five sections:

1. [Static Rules](static-rules.md): Security settings that apply to your entire planet. 
2. [Dynamic Rules](dynamic-rules.md):  Thresholds for banning sources of hostile traffic.
3. [Quarantined](quarantined.md): The "warehouse" of traffic sources that are currently banned. This contains blacklists and whitelists, allowing you to manually control quarantines when necessary. 
4. [Profiles](profiles/): Creation of security rule sets for assignment to specific resources, locations, and applications. 
5. [Args Analysis](args-analysis.md): Settings for allowing requests based on their arguments, in a procedure that occurs before normal WAF inspection and filtering.

The Security section is where you define the "under the hood" settings for Reblaze. When defining or editing the information in this section, careful consideration is necessary. 

Before investigating each section of the interface, it's recommended to read the "[Security Concepts](concepts.md)" discussion on the next page of this Manual.

