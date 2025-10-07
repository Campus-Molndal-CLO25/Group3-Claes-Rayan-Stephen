### 1 -> N  one-to-many  
Customer has multiple addresses
Customers can have multiple orders.
Product has multiple variants  
Order has multiple order lines
### N <-> M many-to-many  
A Product can belong to multiple categories and a category can contain multiple products (solved via ProductCategories)
### 1 -> 1 one-to-one  
A product variant has exactly one inventory record (Inventory)

## Main parts   
Customers → Orders → Order items → Products.
### First:   
started with the main part — 
A customer places an Order with multiple Products.
### Second:  
The extension — Categories, Variants, Inventory, Addresses.
### Finally:  
Then normalized the data by moving variants and addresses to their own tables to avoid duplication.
