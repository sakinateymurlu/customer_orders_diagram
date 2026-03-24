# customer_orders_diagram
sample_schemas
```mermaid
erDiagram
    CUSTOMERS {
        INT customer_id PK
        VARCHAR name
        VARCHAR email
        VARCHAR phone
        VARCHAR address
    }
    STORES {
        INT store_id PK
        VARCHAR store_name
        VARCHAR location
    }
    PRODUCTS {
        INT product_id PK
        VARCHAR product_name
        VARCHAR category
        NUMBER price
        NUMBER stock_quantity
    }
    ORDERS {
        INT order_id PK
        INT customer_id FK
        INT store_id FK
        DATE order_date
        VARCHAR status
    }
    ORDER_ITEMS {
        INT order_item_id PK
        INT order_id FK
        INT product_id FK
        NUMBER quantity
        NUMBER unit_price
    }
    SHIPMENTS {
        INT shipment_id PK
        INT order_id FK
        DATE shipped_date
        VARCHAR carrier
        VARCHAR tracking_number
    }
    INVENTORY {
        INT store_id FK
        INT product_id FK
        NUMBER quantity
    }

    CUSTOMERS ||--o{ ORDERS : "places"
    STORES ||--o{ ORDERS : "fulfills"
    ORDERS ||--|{ ORDER_ITEMS : "contains"
    PRODUCTS ||--o{ ORDER_ITEMS : "included in"
    ORDERS ||--o{ SHIPMENTS : "shipped via"
    STORES ||--o{ INVENTORY : "holds"
    PRODUCTS ||--o{ INVENTORY : "stored in"
