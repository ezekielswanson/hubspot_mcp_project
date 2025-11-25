# Implementation Plan for HubSpot Object Contact Fields

1. **Identify all fields from the [System X] list in {field name file}.md** 

Create ALL fields list under the Field Label Names:

2. **Map [System X] data types to HubSpot types** according to these rules:

*** update rules based on field types from the system you are working with

   * Text/Formula (Text) → type: string, fieldType: text
   * Long Text Area/Text Area → type: string, fieldType: textarea
   * Rich Text Area → type: string, fieldType: textarea
   * Number → type: number, fieldType: number
   * Currency → type: number, fieldType: number
   * Formula (Number) → type: number, fieldType: number
   * Percent → type: number, fieldType: number
   * Date → type: date, fieldType: date
   * Date/Time → type: datetime, fieldType: datetime
   * Checkbox → type: bool, fieldType: booleancheckbox
   * Picklist → type: enumeration, fieldType: select (with placeholder option)
   * Multi-Select Picklist → type: enumeration, fieldType: checkbox (with placeholder option)
   * Lookup → type: string, fieldType: text
   * Email → type: string, fieldType: text
   * Phone → type: string, fieldType: text
   * URL → type: string, fieldType: text
   * Record Type → type: string, fieldType: text
   * Auto Number → type: string, fieldType: text
   * Time → type: datetime, fieldType: datetime
   * Address → type: string, fieldType: text
   * Geolocation → type: string, fieldType: text
   * Formula (Checkbox) → type: bool, fieldType: booleancheckbox

   ##Ignore the Controlling Field

   ##Please make field required if Required = true

3. **Execute the creation** using the hubspot-create-property tool, specifying:
   * objectType: "object"
   * name: [System X] internal field value converted to all lowercase (preserve exact format including underscores and "__c" suffix)
   * label: The exact human-readable field label from the Field Label Names section
   * type: The proper data type from our mapping
   * fieldType: The UI field type from our mapping
   * groupName: "test_group"
   * For picklists and multi-select picklists:
     * Include all values from the "Data Type Values" column as options
     * Each value should be included as a separate option in the options array
     * Format each option with a label and value matching the exact text from [System X]
   * For formula fields:
     * Use the calculationFormula parameter to specify the formula logic if available
   * For any field with predefined values in the "Data Type Values" column, ensure these values are properly transferred to the corresponding HubSpot property

## Examples:
* [System X] internal field: `of_Active_Users__c` → HubSpot name: `of_active_users__c`
* [System X] label: "# of Active Users" → HubSpot label: "# of Active Users"
* Picklist example for Fields with Picklist values field:
  ```
  options: [
    { 
      label: "Executive Leader (C-Suite)", 
      value: "Executive Leader (C-Suite)" 
    },
    { 
      label: "Owner", 
      value: "Owner" 
    },
    {
      label: "Office Manager / Administration",
      value: "Office Manager / Administration"
    },
    {
      label: "Marketing",
      value: "Marketing"
    },
    {
      label: "Accounts Payable",
      value: "Accounts Payable"
    },
    {
      label: "Insurance Billing",
      value: "Insurance Billing"
    },
    {
      label: "Technical / IT",
      value: "Technical / IT"
    },
    {
      label: "Operations",
      value: "Operations"
    },
    {
      label: "Lead Provider",
      value: "Lead Provider"
    },
    {
      label: "Provider (Doctor, Dentist, etc.)",
      value: "Provider (Doctor, Dentist, etc.)"
    }
  ]
  ```


##Requirements
Use the hubspot mcp tool for this.

ONLY create properites expliclity listed in the input or field name file I provided.

Always skip if the there's a field with an exact matching internal name value. List out the exiting matching internal value & list the field that couldn't be created 


Gather context, create a plan, clarify where needed. No dode yet please.


##mcp order steps
1. mcp_hubspot_hubspot-get-user-details - To check HubSpot account details
2. mcp_hubspot_hubspot-get-schemas - To verify the  object exists
3. mcp_hubspot_hubspot-list-properties - To see existing properties for th object
4. mcp_hubspot_hubspot-create-property




