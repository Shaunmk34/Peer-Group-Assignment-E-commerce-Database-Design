# Peer-Group-Assignment-E-commerce-Database-Design

**Course:** Database design & programming with SQL 
**Submission Date:** 04/25/2025

**Group Members:** 
marvine	odhiambo	okothmarvine4@gmail.com	
bongani	sihlangu	gidson03@gmail.com	
andile	makhanya	shaunskhosana66@gmail.com 	
iam	muigai	ianngash41@gmail.com	
joshua	ojeowain	joshuaojewain@gmail.com	
scelo	phoswa	sphoswa2@gmail.com	
kepher	ogalo	ogalokepher22@gmail.com	
martin	kabui	martingitaukabui@gmail.com


## 🎯 Project Overview

Dear Professor Gerald Macherechedze,

Our team has designed a comprehensive e-commerce database system that handles all core aspects of online retail operations. This system manages products with their variations, inventory, media assets, and extensive attribute systems.

## 🏗️ Database Structure Explanation

### 1. Core Product Architecture

We built the system around three central tables:
- **`product`**: The foundation containing all base product information
- **`brand`**: Stores manufacturer details to maintain brand consistency
- **`product_category`**: Implements a hierarchical categorization system (with parent-child relationships)

```sql
-- Example: Creating a new product
INSERT INTO brand (brand_name) VALUES ('Nike');
INSERT INTO product_category (category_name) VALUES ('Running Shoes');
INSERT INTO product (product_name, brand_id, category_id) 
VALUES ('Air Max', 1, 1);
```

### 2. Variation Management System

We implemented a flexible variation system to handle:
- **Sizes** (organized by categories like clothing, shoes)
- **Colors** (with both names and hex codes for UI display)
- **Inventory items** (physical stock tracking)

```sql
-- Adding size options
INSERT INTO size_category (category_name) VALUES ('Shoes');
INSERT INTO size_option (size_category_id, size_value) 
VALUES (1, 'US 10'), (1, 'US 11');

-- Creating product variations
INSERT INTO product_variation (product_id, size_id, color_id)
VALUES (1, 1, 3); -- Product 1, Size US 10, Color Red
```

### 3. Advanced Attribute System

Our attribute system allows for:
- Custom product specifications
- Multiple data types (text, number, boolean)
- Logical grouping of attributes

```sql
-- Defining attribute types
INSERT INTO attribute_category (category_name) VALUES ('Technical Specifications');
INSERT INTO attribute_type (attr_category_id, type_name, data_type)
VALUES (1, 'Weight', 'number');

-- Assigning attributes to products
INSERT INTO product_attribute (product_id, attr_type_id, attr_value)
VALUES (1, 1, '0.5'); -- Product 1 weighs 0.5kg
```

## 🔍 Key Design Decisions

1. **Referential Integrity**: We used foreign key constraints with appropriate ON DELETE actions:
   - CASCADE for dependent records (like product images)
   - SET NULL for optional relationships (like brand associations)

2. **Inventory Management**: The `product_item` table tracks actual physical inventory separate from product definitions.

3. **Media Handling**: The `product_image` table supports multiple images per product with ordering and primary image designation.

## 🛠️ Implementation Challenges

1. **Variation Complexity**: We initially struggled with representing multi-dimensional variations (size × color × other attributes) but solved this through our `product_variation` junction table.

2. **Attribute Flexibility**: Creating a system that could handle diverse product types required careful planning of the attribute type system.

3. **Performance Considerations**: We added indexes on frequently queried fields like SKU and barcode to ensure quick lookups.

## 📊 Sample Queries

Here are some practical examples of how the database would be used:

```sql
-- Get all available colors for a product
SELECT c.color_name 
FROM product_variation pv
JOIN color c ON pv.color_id = c.color_id
WHERE pv.product_id = 1
GROUP BY c.color_id;

-- Check stock levels
SELECT pi.quantity_in_stock, so.size_value, c.color_name
FROM product_item pi
JOIN product_variation pv ON pi.variation_id = pv.variation_id
JOIN size_option so ON pv.size_id = so.size_id
JOIN color c ON pv.color_id = c.color_id
WHERE pv.product_id = 1;

-- Get product details with attributes
SELECT p.product_name, at.type_name, pa.attr_value
FROM product p
LEFT JOIN product_attribute pa ON p.product_id = pa.product_id
LEFT JOIN attribute_type at ON pa.attr_type_id = at.attr_type_id
WHERE p.product_id = 1;
```

## 🙏 Acknowledgments

We appreciate your guidance throughout this project. The database design principles you taught us were invaluable in creating this system. We welcome any feedback you may have on our implementation.


#Group Number 695  
#POWER LEARN PROJECT 
#4/28/2025 
