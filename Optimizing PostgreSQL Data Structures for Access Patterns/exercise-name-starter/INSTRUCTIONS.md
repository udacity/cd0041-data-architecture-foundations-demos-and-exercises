# Optimizing PostgreSQL Data Structures for Access Patterns

## Instructions

Using the data contract found below and the three CSV files provided: (vendor, software, contract_info)

Create base tables based on Data Contract

Populate the tables with CSV data

### Indexing

Choose a column that would benefit from indexing

Run an "Explain Analyze" query on the the table holding that column

Create index

Re-run the "Explain Analyze"

### OLAP

Create an OLAP view for annual contract spend and run a query on the view to ensure it works

### Data Contract

  "contract_name": "Software Vendor Support Contract Data Contract",
  "version": "1.0",
  "description": "Data contract defining vendors, software products, and support contract information for enterprise software management.",
  "tables": [
    {
      "table_name": "Vendor",
      "description": "Organizations that provide software products and support services.",
      "columns": [
        {
          "name": "vendor_id",
          "data_type": "string",
          "required": true,
          "pattern": "^VEN[0-9]{4}$"
        },
        {
          "name": "vendor_name",
          "data_type": "string",
          "required": true,
          "min_length": 2,
          "max_length": 100
        },
        {
          "name": "vendor_type",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "Software Publisher",
            "Cloud Provider",
            "Managed Service Provider",
            "Security Vendor",
            "Consulting Partner"
          ]
        },
        {
          "name": "primary_contact",
          "data_type": "string",
          "required": true,
          "max_length": 100
        },
        {
          "name": "contact_email",
          "data_type": "string",
          "required": true,
          "format": "email"
        },
        {
          "name": "support_phone",
          "data_type": "string",
          "required": false
        }
      ]
    },
    {
      "table_name": "Software",
      "description": "Software applications supported under vendor contracts.",
      "columns": [
        {
          "name": "software_id",
          "data_type": "string",
          "required": true,
          "pattern": "^SW[0-9]{5}$"
        },
        {
          "name": "software_name",
          "data_type": "string",
          "required": true,
          "max_length": 100
        },
        {
          "name": "software_category",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "ERP",
            "CRM",
            "Cybersecurity",
            "Database",
            "Analytics",
            "Cloud Platform",
            "Collaboration",
            "IT Operations"
          ]
        },
        {
          "name": "version",
          "data_type": "string",
          "required": true,
          "max_length": 50
        },
        {
          "name": "vendor_id",
          "data_type": "string",
          "required": true,
          "foreign_key": {
            "table": "Vendor",
            "column": "vendor_id"
          }
        }
      ]
    },
    {
      "table_name": "Contract_Info",
      "description": "Support contract information for software products.",
      "columns": [
        {
          "name": "contract_id",
          "data_type": "string",
          "required": true,
          "pattern": "^CON[0-9]{6}$"
        },
        {
          "name": "software_id",
          "data_type": "string",
          "required": true,
          "foreign_key": {
            "table": "Software",
            "column": "software_id"
          }
        },
        {
          "name": "contract_start_date",
          "data_type": "date",
          "required": true
        },
        {
          "name": "contract_end_date",
          "data_type": "date",
          "required": true
        },
        {
          "name": "annual_cost",
          "data_type": "decimal",
          "required": true,
          "minimum": 0.01
        },
        {
          "name": "support_level",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "Standard",
            "Premium",
            "Enterprise",
            "24x7"
          ]
        },
        {
          "name": "sla_response_hours",
          "data_type": "integer",
          "required": true,
          "minimum": 1
        },
        {
          "name": "contract_status",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "Active",
            "Expired",
            "Pending Renewal",
            "Terminated"
          ]
        }
      ]
    }
  ],
  "business_rules": [
    "Every software product must be associated with a valid vendor.",
    "Every contract must reference a valid software product.",
    "Contract end date must be later than contract start date.",
    "Annual contract cost must be greater than zero.",
    "Support level must be one of the approved support tiers.",
    "Vendor email addresses must be unique.",
    "Only one active contract may exist for a software product at a given time.",
    "Contracts with an end date in the past should have a status of Expired or Terminated."
  ]
}