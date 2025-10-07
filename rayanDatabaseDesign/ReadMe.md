# 🎃 Halloween Webshop – Databasdesign

Detta projekt är en planering av en databas för en Halloween-webshop som säljer kostymer, dekorationer och godis.  
Syftet är att skapa en normaliserad och tydlig databasstruktur som hanterar kunder, produkter, beställningar och kategorier.

---

## 🧩 Databasöversikt

Databasen är uppdelad i flera tabeller med tydliga ansvarsområden.  
Relationerna följer principerna för **1:N** och **N:M** för att undvika dataduplicering.

### 1. `customers`
Lagrar grundläggande information om registrerade kunder.
- En kund kan ha flera adresser.
- Kolumner: `email`, `first_name`, `last_name`, `phone`, `created_at`.

### 2. `addresses`
Hantera flera leveransadresser per kund.
- Relation: `addresses.customer_id` → `customers.id`
- Fältet `is_default` markerar standardadress.

### 3. `categories`
Beskriver olika produktkategorier (t.ex. “Kostymer”, “Godis”, “Dekorationer”).

### 4. `products`
Innehåller huvudinformation om en produkt (namn, beskrivning, aktiv status, etc.).
- Har en SKU (Stock Keeping Unit) för att identifiera produkten.

### 5. `product_variants`
En produkt kan ha flera varianter, t.ex. olika **storlekar** eller **färger**.
- Relation: `product_variants.product_id` → `products.id`
- Innehåller pris, lagerantal och tillåtelse för restorder.
- `price` visar nuvarande försäljningspris i butiken.

### 6. `product_categories`
Kopplingstabell som hanterar **N:M-relationen** mellan `products` och `categories`.
- En produkt kan tillhöra flera kategorier.
- En kategori kan innehålla flera produkter.

### 7. `orders`
Representerar en kundorder.
- Relation: `orders.customer_id` → `customers.id`
- Relation: `orders.shipping_address_id` → `addresses.id`
- Fält: orderstatus, datum, totalbelopp.

### 8. `order_items`
Kopplingstabell mellan `orders` och `product_variants`.
- En order kan innehålla flera produkter.
- En produktvariant kan finnas i flera ordrar.
- Relationer:
  - `order_items.order_id` → `orders.id`
  - `order_items.product_variant_id` → `product_variants.id`
- `subtotal` beräknas som `price * quantity`.

---

## 🔗 Relationer och kardinalitet

| Relation | Typ | Beskrivning |
|-----------|-----|-------------|
| Customer → Address | 1:N | En kund kan ha flera adresser |
| Product → ProductVariant | 1:N | En produkt kan ha flera varianter |
| Product ↔ Category | N:M | Kopplas via `product_categories` |
| Customer → Order | 1:N | En kund kan göra flera ordrar |
| Order ↔ ProductVariant | N:M | Kopplas via `order_items` |

---

## ⚙️ Normalisering

Databasen är normaliserad till minst **3NF** (tredje normalformen):
- Inga upprepade datafält.
- Varje tabell har ett tydligt syfte.
- Primärnycklar och främmande nycklar används konsekvent.
- Kopplingstabeller (`product_categories` och `order_items`) används för alla N:M-relationer.

---

## 💡 Designval och motivering

- **Separata tabeller för adresser:** gör det möjligt för kunder att ha flera leveransadresser utan att duplicera kundinformation.  
- **`product_variants`:** möjliggör hantering av storlek, färg och pris per variant.  
- **`order_items`:** kopplar ordrar till produktvarianter och lagrar kvantitet samt delsumma.  
- **`price` i `product_variants`:** representerar aktuellt försäljningspris; vi har tagit bort `unit_price` för enkelhet i denna version.  
- **Kategorier:** hanteras via en kopplingstabell för att stödja flera kategorier per produkt.

---

## 🕸️ Sammanfattning

Denna struktur gör det enkelt att:
- Lägga till nya produktkategorier.
- Hantera olika storlekar och färger.
- Skapa ordrar med flera produkter.
- Undvika dataduplicering och hålla databasen normaliserad.

---

**Skapat av:** *[Ditt namn / Gruppnamn]*  
**Verktyg:** dbdiagram.io  
**Syfte:** Databasplanering för Halloween Webshop-projektet 🎃
