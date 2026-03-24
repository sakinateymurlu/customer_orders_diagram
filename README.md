# Customer Orders Sample Schema

## Schema Description

Customer Orders (`CO`) is a sample schema resembling a generic customer orders management schema. The Customer Orders (`CO`) schema records the details of transactions made by a retail application.

The `CO` schema highlights features such as JSON support.

The company sells a variety of products, which are maintained in the `products` table. Each product has a unique identification number, name, price, details stored in a JSON object and product image details.

The orders placed by the customer are tracked in the `orders` table using the order identification number, date and time when the order was placed, customer details, order status and the store information.

The details of the products in a particular order are also tracked in the `order_items` table using the order identification number. Details of the products, price at the time of purchase, quantity and shipment are recorded.

The information of a customer placing an order is tracked in the `customers` table. Each customer has an identification number, name, and email address that is used for communication of the orders.

The customers can purchase the products in stores or online through the company's website. The information for all of the stores and their corresponding physical and virtual addresses is tracked in the `stores` table. The store information is also recorded in the order details.

The shipment details of the orders placed such as the delivery address, customer details, store information and the shipment status are stored in the `shipments` table.

An `inventory` table stores the details of each product such as the quantity available at each store.

---

## Install Instructions

1. Connect as privileged user with rights to create another user (`SYSTEM`, `ADMIN`, etc.)
2. Run the `co_install.sql` script to create the `CO` (Customer Orders) schema
3. You are prompted for:
   - `password` — enter an Oracle Database compliant password
   - `tablespace` — if you do not enter a tablespace, the default database tablespace is used

**Note:** If the CO schema already exists, it is removed/dropped and a fresh CO schema is installed.

### Dependencies and Requirements

- Oracle Database 19c and higher  
- Access to `co_install.sql`, `co_create.sql`, `co_populate.sql`  
- Scripts need to be run as a privileged user with rights to create and drop another user (`SYSTEM`, `ADMIN`, etc.)

---

## Uninstall Instructions

1. Connect as privileged user with rights to drop another user (`SYSTEM`, `ADMIN`, etc.)  
2. Run the `co_uninstall.sql` script to remove the `CO` (Customer Orders) schema  

---

## Schema Details

### Schema Objects

| Object Type | Objects |
|-------------|---------|
| Index       | `customers_name_i`, `orders_customer_id_i`, `orders_store_id_i`, `products_pk`, `stores_pk`, `store_name_u`, `customers_pk`, `customers_email_u`, `orders_pk`, `order_items_pk`, `order_items_product_u`, `inventory_product_id_i`, `inventory_pk`, `inventory_store_product_u`, `shipments_store_id_i`, `shipments_customer_id_i` |

### Table Descriptions

#### CUSTOMERS
- `customer_id` PK
- `name`
- `email`
- `phone`
- `address`

#### STORES
- `store_id` PK
- `store_name`
- `location`

#### PRODUCTS
- `product_id` PK
- `product_name`
- `category`
- `price`
- `stock_quantity`

#### ORDERS
- `order_id` PK
- `customer_id` FK
- `store_id` FK
- `order_date`
- `status`

#### ORDER_ITEMS
- `order_item_id` PK
- `order_id` FK
- `product_id` FK
- `quantity`
- `unit_price`

#### SHIPMENTS
- `shipment_id` PK
- `order_id` FK
- `shipped_date`
- `carrier`
- `tracking_number`

#### INVENTORY
- `store_id` FK
- `product_id` FK
- `quantity`

---

## ER Diagram

```mermaid
erDiagram
    CUSTOMERS ||--o{ ORDERS : "places"
    STORES ||--o{ ORDERS : "fulfills"
    ORDERS ||--|{ ORDER_ITEMS : "contains"
    PRODUCTS ||--o{ ORDER_ITEMS : "included in"
    ORDERS ||--o{ SHIPMENTS : "shipped via"
    STORES ||--o{ INVENTORY : "holds"
    PRODUCTS ||--o{ INVENTORY : "stored in"
