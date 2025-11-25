# HubSpot Custom Properties Implementation

## Overview
This repository contains templates and guides for migrating custom fields from external CRM systems into HubSpot custom properties.

## Files

### `custom_properties_hubspot_implementation_template.md`
A generalized template for implementing custom properties in HubSpot from any source system (referred to as "[System X]"). This template provides:
- Field mapping guidelines from source system data types to HubSpot types
- Step-by-step execution instructions using HubSpot MCP tools
- Examples for handling picklists, formulas, and various field types
- MCP tool execution order

### `implementation.md`
Salesforce-specific implementation guide with the same structure as the template, tailored for Salesforce-to-HubSpot migrations.

### `leads.md`
Sample source system field definitions showing the structure needed for migration (Field Label, Field Name, Data Type, and Data Type Values).

## Quick Start

1. **Prepare your source data** - Create a field list following the format in `leads.md`
2. **Review the template** - Use `custom_properties_hubspot_implementation_template.md` as your guide
3. **Execute MCP steps** in order:
   - Verify HubSpot account access
   - Confirm target object schema
   - Review existing properties
   - Create new properties

## Key Principles

- Field names convert to lowercase while preserving underscores and suffixes
- Picklist values transfer with matching labels and values
- Each field type maps to specific HubSpot type/fieldType combinations
- All fields created in "test_group" for organization

## Requirements

- HubSpot portal access with custom schema read/write permissions
- HubSpot MCP integration tools configured
