============
Introduction
============

Overview
--------

- This guide will walk you through the entire workshop in easy steps.
- There are three modules as part of this workshop.

Important Note on the Translation process
-----------------------------------------

- This translation is only meant for ACI (Application Centric Infrastructure).
- This is not a static translation.
- The process does not directly convert Ansible playbook written in YAML (YAML ain't markup language) to a Terraform configuration file which is written in HCL (Hashicorp Configuration Language).
- The selected playbook will be run by Ansible and interact with the provided APIC (Application Policy Infrastructure Controller) for the translation to complete.
- At a minimum, you need an APIC simulator.


Module1: Translate **my_ACI_playbook.yml** using the Translator application 
-----------------------------------------------------------------------
This module will familiarize you with the translator application.

Module2: Manually translate **my_ACI_playbook.yml**
-----------------------------------------------
This module replicates Module1, but you will perform the steps manually. This allows you to understand what the application does in the backend.

Module3: Translate **my_ACI_role** using the Translator application 
---------------------------------------------------------------
This module shows you how to translate an entire Ansible ACI role using the translator application.
