# Building Domain ERDs in Mermaid

## Background

Below you will find a data contract for a 4 table database that tracks B2B (Business to Business) sales of kitchen equipment for the fictional company ABC Kitchen Corp. 

The tables are: Inventory, Salesperson, Customer, Purchases. All information, including column names, data types, and key relationships are covered in the contract.

{
  "contract_name": "B2B Kitchen Equipment Sales Data Contract",
  "version": "1.0",
  "description": "Data contract defining schema and validation rules for kitchen equipment inventory, sales representatives, customers, and purchase transactions.",
  "tables": [
    {
      "table_name": "Inventory",
      "description": "Kitchen equipment available for sale.",
      "columns": [
        {
          "name": "inventory_id",
          "data_type": "string",
          "required": true,
          "pattern": "^INV[0-9]{5}$"
        },
        {
          "name": "product_name",
          "data_type": "string",
          "required": true,
          "min_length": 3,
          "max_length": 100
        },
        {
          "name": "category",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "Refrigeration",
            "Cooking Equipment",
            "Dishwashing",
            "Food Preparation",
            "Ventilation",
            "Storage"
          ]
        },
        {
          "name": "unit_price",
          "data_type": "decimal",
          "required": true,
          "minimum": 0.01
        },
        {
          "name": "quantity_on_hand",
          "data_type": "integer",
          "required": true,
          "minimum": 0
        }
      ]
    },
    {
      "table_name": "Salesperson",
      "description": "Sales representatives responsible for customer accounts.",
      "columns": [
        {
          "name": "salesperson_id",
          "data_type": "string",
          "required": true,
          "pattern": "^SP[0-9]{4}$"
        },
        {
          "name": "first_name",
          "data_type": "string",
          "required": true,
          "min_length": 2,
          "max_length": 50
        },
        {
          "name": "last_name",
          "data_type": "string",
          "required": true,
          "min_length": 2,
          "max_length": 50
        },
        {
          "name": "email",
          "data_type": "string",
          "required": true,
          "format": "email"
        },
        {
          "name": "territory",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "Northeast",
            "Southeast",
            "Midwest",
            "Southwest",
            "West"
          ]
        }
      ]
    },
    {
      "table_name": "Customer",
      "description": "Business customers purchasing kitchen equipment.",
      "columns": [
        {
          "name": "customer_id",
          "data_type": "string",
          "required": true,
          "pattern": "^CUS[0-9]{5}$"
        },
        {
          "name": "company_name",
          "data_type": "string",
          "required": true,
          "min_length": 2,
          "max_length": 150
        },
        {
          "name": "industry",
          "data_type": "string",
          "required": true,
          "allowed_values": [
            "Restaurant",
            "Hotel",
            "Hospital",
            "School",
            "Corporate Cafeteria",
            "Food Service Distributor"
          ]
        },
        {
          "name": "state",
          "data_type": "string",
          "required": true,
          "pattern": "^[A-Z]{2}$"
        },
        {
          "name": "salesperson_id",
          "data_type": "string",
          "required": true,
          "foreign_key": {
            "table": "Salesperson",
            "column": "salesperson_id"
          }
        }
      ]
    },
    {
      "table_name": "Purchases",
      "description": "Purchase transactions made by customers.",
      "columns": [
        {
          "name": "purchase_id",
          "data_type": "string",
          "required": true,
          "pattern": "^PUR[0-9]{6}$"
        },
        {
          "name": "purchase_date",
          "data_type": "date",
          "required": true
        },
        {
          "name": "customer_id",
          "data_type": "string",
          "required": true,
          "foreign_key": {
            "table": "Customer",
            "column": "customer_id"
          }
        },
        {
          "name": "inventory_id",
          "data_type": "string",
          "required": true,
          "foreign_key": {
            "table": "Inventory",
            "column": "inventory_id"
          }
        },
        {
          "name": "quantity_purchased",
          "data_type": "integer",
          "required": true,
          "minimum": 1
        },
        {
          "name": "total_amount",
          "data_type": "decimal",
          "required": true,
          "minimum": 0.01
        }
      ]
    }
  ],
  "business_rules": [
    "Every customer must be assigned to a valid salesperson.",
    "Every purchase must reference a valid customer and inventory item.",
    "Quantity purchased must be greater than zero.",
    "Unit price and total amount must be positive values.",
    "Inventory quantity on hand cannot be negative.",
    "Salesperson email addresses must be unique."
  ]
}

## Assignment

Using the information found in the above data contract, create 3 ERDs using Mermaid

### Conceptual

The Conceptual ERD should only include Entity names and show relationship lines.

### Logical

The Logical Model includes Entities and Attributes but uses non-technical terminology. Column names can be more verbose and data types can be can use generic terminology such as Text or String instead of Varchar(x).

### Physical

The Physical Model should be built with a PostgreSQL implementation in mind. Entity and Column names should be computer friendly (No spaces, abbreviations can be used) and data types need to conform to data types found in PostgreSQL. 

## Submission

Your Mermaid code should be placed in the Markdown cells below. Ensure the Mermaid images render correctly.