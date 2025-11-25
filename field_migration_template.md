# Universal System-to-System Field Migration Documentation Template

## Source System Fields

**Instructions:** Replace [SOURCE SYSTEM] with your source system name (e.g., Salesforce, Zoho, Custom System etc.)

| Field Label | Field Name | Data Type | Data Type Values |
|-------------|------------|-----------|------------------|  
| [Human-readable label] | [internal_field_name] | [Data type] | [Comma-separated values if applicable] |
| TEST_Lead Notes | Lead_Notes__c TEST | Long Text Area(10000) | |
| TEST_Lead Role | Lead_Role__c TEST | Picklist | Executive Leader (C-Suite), Owner, Office Manager / Administration, Marketing, Accounts Payable, Insurance Billing, Technical / IT, Operations, Lead Provider, Provider (Doctor, Dentist, etc.) |

---

## Implementation Plan for [TARGET SYSTEM] Object Fields

**Instructions:** Replace [TARGET SYSTEM] with your destination system name (e.g., HubSpot, Salesforce, Pipedrive, etc.)

### Step 1: Identify all fields from the [SOURCE SYSTEM] list

Create ALL fields list under the Field Label Names from your source system export.

### Step 2: Map [SOURCE SYSTEM] data types to [TARGET SYSTEM] types

**Instructions:** Customize this mapping table based on your specific source and target systems.

#### Example Mapping (Salesforce → HubSpot):

| Source System Data Type | Target System Type | Target System Field Type |
|-------------------------|-------------------|-------------------------|
| Text/Formula (Text) | string | text |
| Long Text Area/Text Area | string | textarea |
| Rich Text Area | string | textarea |
| Number | number | number |
| Currency | number | number |
| Formula (Number) | number | number |
| Percent | number | number |
| Date | date | date |
| Date/Time | datetime | datetime |
| Checkbox | bool | booleancheckbox |
| Picklist | enumeration | select |
| Multi-Select Picklist | enumeration | checkbox |
| Lookup | string | text |
| Email | string | text |
| Phone | string | text |
| URL | string | text |
| Record Type | string | text |
| Auto Number | string | text |
| Time | datetime | datetime |
| Address | string | text |
| Geolocation | string | text |
| Formula (Checkbox) | bool | booleancheckbox |

**Note:** 
- Ignore controlling fields or dependency fields that don't apply to the target system
- Make field required if Required = true in source system

### Step 3: Execute the creation using [TARGET SYSTEM API/TOOL]

**Instructions:** Replace the parameter names and values with those specific to your target system's API or tool.

#### Generic Parameters Template:

```
* objectType: "[target_object_type]"
* name: [source_internal_field_name converted to target system naming convention]
* label: [human-readable field label from source system]
* type: [mapped data type from Step 2]
* fieldType: [mapped UI field type from Step 2]
* groupName: "[optional_field_group_name]"
```

#### HubSpot-Specific Example:

```
* objectType: "contacts" (or "companies", "deals", "tickets", custom objects)
* name: Source internal field value converted to all lowercase (preserve exact format including underscores and "__c" suffix)
* label: The exact human-readable field label from the Field Label Names section
* type: The proper data type from our mapping
* fieldType: The UI field type from our mapping
* groupName: "test_group"
```

**For picklist/dropdown fields:**
- Include all values from the "Data Type Values" column as options
- Each value should be included as a separate option in the options array
- Format each option with a label and value matching the exact text from source system

**For formula/calculated fields:**
- Use the appropriate formula parameter to specify the calculation logic if available
- Note: Some systems may not support formula fields directly

**For any field with predefined values:**
- Ensure these values are properly transferred to the corresponding target system property

### Field Naming Convention Rules

**Instructions:** Define your naming convention rules based on source and target systems.

#### Example Rules (Salesforce → HubSpot):
* Source internal field: `of_Active_Users__c` → Target name: `of_active_users__c`
* Source label: "# of Active Users" → Target label: "# of Active Users"
* General rule: Convert to lowercase, preserve underscores and suffixes

#### Your Custom Rules:
* Source naming pattern: `[YOUR_PATTERN]` → Target naming pattern: `[YOUR_PATTERN]`
* Allowed characters: `[SPECIFY]`
* Maximum length: `[SPECIFY]`
* Special character handling: `[SPECIFY]`

---

## Data Migration Examples

### Example 1: Text Field

**Source System Field:**
```
Field Label: Customer Notes
Field Name: customer_notes__c
Data Type: Long Text Area(10000)
```

**Target System Property:**
```json
{
  "name": "customer_notes__c",
  "label": "Customer Notes",
  "type": "string",
  "fieldType": "textarea",
  "groupName": "custom_fields"
}
```

### Example 2: Picklist/Dropdown Field

**Source System Field:**
```
Field Label: Lead Role
Field Name: Lead_Role__c
Data Type: Picklist
Values: Executive Leader (C-Suite), Owner, Office Manager, Marketing, Operations
```

**Target System Property:**
```json
{
  "name": "lead_role__c",
  "label": "Lead Role",
  "type": "enumeration",
  "fieldType": "select",
  "groupName": "custom_fields",
  "options": [
    { 
      "label": "Executive Leader (C-Suite)", 
      "value": "Executive Leader (C-Suite)" 
    },
    { 
      "label": "Owner", 
      "value": "Owner" 
    },
    {
      "label": "Office Manager",
      "value": "Office Manager"
    },
    {
      "label": "Marketing",
      "value": "Marketing"
    },
    {
      "label": "Operations",
      "value": "Operations"
    }
  ]
}
```

### Example 3: Number/Currency Field

**Source System Field:**
```
Field Label: Annual Revenue
Field Name: annual_revenue__c
Data Type: Currency
```

**Target System Property:**
```json
{
  "name": "annual_revenue__c",
  "label": "Annual Revenue",
  "type": "number",
  "fieldType": "number",
  "groupName": "financial_data"
}
```

---



### mcp order steps
1. mcp_hubspot_hubspot-get-user-details - To check HubSpot account details
2. mcp_hubspot_hubspot-get-schemas - To verify the  object exists
3. mcp_hubspot_hubspot-list-properties - To see existing properties for th object
4. mcp_hubspot_hubspot-create-property



### Scenario 1: Salesforce → HubSpot
- Convert `__c` custom field suffix to lowercase
- Map Salesforce picklists to HubSpot select/radio fields
- Convert formula fields to calculated properties or plain fields

### Scenario 2: HubSpot → Salesforce
- Convert snake_case to PascalCase__c for custom fields
- Map HubSpot select fields to Salesforce picklists
- Consider Salesforce field length limits (255 chars for text fields)

### Scenario 3: Microsoft Dynamics → HubSpot
- Convert schema names (new_fieldname) to lowercase with underscores
- Map option sets to select/checkbox fields
- Handle lookup fields as text or associations

### Scenario 4: Zoho → Salesforce
- Map Zoho custom fields to Salesforce custom fields with `__c` suffix
- Convert multi-select picklists appropriately
- Consider API name length restrictions

### Scenario 5: Custom System → Any Platform
- Document current naming conventions
- Create comprehensive data type mapping table
- Plan for data transformation during migration

---

## Pre-Migration Checklist

- [ ] Export complete field list from source system
- [ ] Document all field dependencies and relationships
- [ ] Create data type mapping table
- [ ] Define naming convention rules
- [ ] Verify API access and permissions in target system
- [ ] Test field creation with sample fields
- [ ] Plan for data validation post-migration
- [ ] Document any fields that cannot be migrated
- [ ] Create rollback plan if needed
- [ ] Schedule migration during low-usage period

---

## Post-Migration Validation

1. **Field Count Verification**: Confirm all fields were created
2. **Data Type Validation**: Verify each field has correct data type
3. **Picklist Values Check**: Ensure all dropdown options migrated
4. **Required Fields**: Confirm required field settings
5. **Field Dependencies**: Test any conditional logic or dependencies
6. **Sample Data Test**: Migrate small data sample and verify
7. **User Access**: Confirm appropriate users can view/edit fields
8. **Documentation**: Update system documentation with new fields

---



## Customization Instructions

To adapt this template for your specific migration:

1. Replace all `[SOURCE SYSTEM]` placeholders with your source system name
2. Replace all `[TARGET SYSTEM]` placeholders with your destination system name
3. Update the data type mapping table in Step 2 with your specific mappings
4. Modify the field naming convention rules for your systems
5. Replace the API/tool implementation steps with your specific endpoints/commands
6. Add any system-specific considerations or limitations
7. Update examples with fields relevant to your migration project
8. Document any custom business logic or transformations needed
