Timestamps

- 09:30 ás 17:00 = segunda feira
- 19:30 ás 21:00 = segunda feira
- 13:00 ás 16:30 = terça feira
- 00:00 ás 02:50 = quarta feira
- 13:00 ás 14:00 = quarta-feira
- 15:00 ás 18:00 = quarta-feira
- 19:10 ás 21:00 = quarta-feira

# Shopify Theme Project – Setup & Usage Guide

This document explains how to set up the project, run it in development mode, configure the theme inside Shopify, and prepare the required data structures (collections, products, metafields, and metaobjects).

---

# 🚀 1. Requirements

- Node.js installed
- Shopify CLI installed
- A Shopify Partner account
- A development store

Install Shopify CLI (if not installed):

```bash
npm install -g @shopify/cli @shopify/theme
```

---

# ⚙️ 2. Running the Theme in Dev Mode

Inside your project folder:

```bash
shopify theme dev
```

This will:

- Upload your theme to Shopify (temporary dev theme)
- Start a local dev server
- Provide a preview URL
- Enable hot-reload

---

# 🧩 3. Working With the Theme Editor

After running `shopify theme dev`:

1. Open the preview URL
2. Click **Customize**
3. Your sections (banner, footer, reviews, best-sell, etc.) will be available
4. Add them to pages as needed

---

# 📄 4. Adding Sections to Pages

Inside the Theme Editor:

- Go to the desired template (e.g. Home page)
- Click **Add Section**
- Select your custom sections:
  - Banner
  - Best Selling Products
  - Reviews
  - FAQ
  - Footer

---

# 🛍️ 5. Store Data Setup (IMPORTANT)

This theme depends on structured data. You MUST configure the following:

---

## 📦 5.1 Collections

Create collections:

- Go to **Products → Collections**
- Click **Create collection**

Required fields:

- **Title**
- **Image**

These are used in:

- Carousels
- Footer collections

---

## 🛒 5.2 Products

Create products:

- Go to **Products → Add product**

Required:

- Title
- Media (image)

---

## ⭐ 5.3 Product Metafields (CRITICAL)

You must manually create custom metafields:

### Go to:

Settings → Custom data → Products → Add definition

---

### ➤ Rating

- Name: `Rating`
- Namespace/key: `custom.rating`
- Type: **Rating**
- Min: 1
- Max: 5

---

### ➤ Review Count

- Name: `Review Count`
- Namespace/key: `custom.review_count`
- Type: **Number (integer)**

---

### ✅ After creating:

- Open each product
- Fill:
  - Rating (e.g. 4.5)
  - Review Count (e.g. 120)

---

# 🧠 6. Metaobject Setup (Reviews System)

This is required for the **Reviews Section**.

---

## ➤ Step 1: Create Metaobject

Go to:

Settings → Custom data → Metaobjects → Add definition

---

### Name: `Review`

---

## ➤ Fields

Create the following fields EXACTLY:

| Field Name       | Type             |
| ---------------- | ---------------- |
| Persona_img      | Image (file)     |
| Persona_name     | Single line text |
| Persona_location | Single line text |
| Product_img      | Image (file)     |
| Product_name     | Single line text |
| Review_text      | Multi-line text  |
| Review_stars     | Rating (1–5)     |

---

## ➤ Step 2: Add Entries

After creating the metaobject:

- Go to **Content → Metaobjects → Review**
- Add multiple review entries

⚠️ Important:

- You MUST create multiple entries, or only one review will show

---

# 🧪 7. Common Issues

---

## ❌ Images not showing

- Ensure images are uploaded via:
  - Theme Editor OR
  - Shopify Files

- Avoid external URLs (Shopify prefers CDN assets)

---

## ❌ Stars not rendering correctly

- Ensure:
  - `review_stars` is set
  - Value is being converted properly in Liquid:

```liquid
{% assign rating = review.stars.value | remove: '.0' | plus: 0 %}
```

---

## ❌ Only 1 review showing

- Make sure:
  - Multiple metaobject entries exist
  - You are looping correctly:

```liquid
{% for review in shop.metaobjects.review.values %}
```

---

## ❌ Sorting products by metafields not working

Shopify Liquid has limitations when sorting by metafields.

Fallback:

- Use manual product selection via Theme Editor
- Or handle ranking outside Liquid

---

# 🧱 8. Project Structure Overview

- `sections/` → main UI sections (banner, footer, etc.)
- `snippets/` → reusable components (icons, cards)
- `assets/` → images, icons, CSS, JS
- `config/` → theme settings

---

# ✅ 9. Recommended Workflow

1. Run:

   ```bash
   shopify theme dev
   ```

2. Configure data (products, collections, metaobjects)
3. Open Theme Editor
4. Add sections
5. Adjust settings visually
6. Iterate with live reload

---

# 🎯 Final Notes

This project relies heavily on:

- Shopify metafields
- Metaobjects
- Theme editor configuration

Without proper setup, sections may:

- Appear empty
- Show fallback content
- Break expected layout

---

If needed, extend this setup with:

- Pagination for reviews
- Dynamic collections
- CMS-driven content via metaobjects

---
