# Halloween Webshop Database Design

Detta projekt innehåller designen av databasen för en Halloween-webshop som säljer kostymer, dekorationer och godis. 
Fokus ligger på att planera en normaliserad databasstruktur och visualisera den med ER-diagram.

---

## Syfte

- Hantera kunder och deras information
- Hantera leveransadresser
- Hantera produkter, varianter och lager
- Hantera kategorier och kopplingar mellan produkter och kategorier
- Hantera kundbeställningar och orderdetaljer
- Säkerställa att databasen är normaliserad och undviker dataduplicering

---

## Tabeller

### Customers
- Lagrar kundinformation för registrerade användare
- **Fält:** `id` (PK), `email` (unik), `password_hash`, `first_name`, `last_name`, `phone`, `created_at`
- En kund kan ha **flera adresser** och **flera beställningar** (N:N)

### Addresses
- Lagrar kunders leveransadresser
- **Fält:** `id` (PK), `customer_id` (FK), `street`, `city`, `postal_code`, `region`, `country`, `is_default`
- `is_default` markerar standardadress för kunden

### Products
- Lagrar huvudproduktinformation
- **Fält:** `id` (PK), `sku` (unik), `name`, `description`, `active`, `created_at`

### Product Variants
- Lagrar olika varianter av en produkt, t.ex. storlek och färg
- **Fält:** `id` (PK), `product_id` (FK), `sku`, `size`, `color`, `price`, `stock_quantity`, `allow_backorder`

### Categories
- Lagrar produktkategorier, t.ex. "Barn", "Kostymer"
- **Fält:** `id` (PK), `name`, `description`

### Product Categories
- Koppling mellan produkter och kategorier (N:M)
- **Fält:** `product_id` (PK, FK), `category_id` (PK, FK)

### Orders
- Lagrar kundbeställningar
- **Fält:** `id` (PK), `customer_id` (FK), `shipping_address_id` (FK), `status`, `order_date`, `delivery_date`, `total_amount`
- En kund kan ha **många beställningar** (1:N)

### Order Items
- Lagrar detaljer för produkter i varje beställning
- **Fält:** `id` (PK), `order_id` (FK), `product_variant_id` (FK), `product_name_snapshot`, `unit_price`, `quantity`, `subtotal`
- Snapshot av produktnamn och pris säkerställer korrekt historik även om produkten ändras eller tas bort

---

## Relationer och kardinalitet

- **Customers → Orders:** 1:N (en kund kan ha flera beställningar)  
- **Customers → Addresses:** 1:N (en kund kan ha flera adresser)  
- **Products → Product Variants:** 1:N  
- **Products → Categories:** N:M via `ProductCategories`  
- **Orders → Order Items:** 1:N  




