# Kenjie Minimart Website — Complete Build Guide

## PROJECT OVERVIEW

**Business:** Kenjie Minimart — 24/7 neighborhood store  
**Owner:** Clarence Gono  
**Location:** Purok 3 Macasandal Along the Highway  
**Phone:** 0975 776 0971  
**Domain:** kenjieminimart.com  
**Live URL:** https://kenjieminimart.com  

---

## HOSTING & DEPLOYMENT

**Domain Registrar:** Hostinger (kenjieminimart.com)  
**Web Hosting:** Netlify (connected to GitHub)  
**GitHub Repo:** plutodx/kenjie-minimart  
**GitHub Branch:** main  
**Netlify Site:** kenjieminimart.netlify.app  

### DNS Configuration (Hostinger)
- A Record @ → 75.2.60.5 (Netlify IP)
- CNAME www → kenjieminimart.com
- SSL: Auto-provisioned by Netlify

---

## FILE STRUCTURE & WHAT EACH FILE DOES

### 1. **index.html** (Public Site)
**What it does:** The customer-facing website. Shows announcements, product prices, and a contact form.

**Sections:**
- **Header:** Logo, tagline, address, open 24/7 badge
- **Nav Tabs:** 
  - 📢 Announcements
  - 💰 Price Lookup
  - ✉️ Message Us
- **Announcements Tab:** Displays announcements + featured products grid + link to all products
- **Price Lookup Tab:** Search bar, category filters, full product list with prices
- **Message Us Tab:** Contact form (Netlify Forms)

**How it works:**
- On page load, fetches `inventory.csv` from GitHub automatically
- Parses the CSV and reads the "Featured" column
- Shows products where Featured = 1
- All data stored in `localStorage` (browser-local storage)

**No admin login needed** — fully public

---

### 2. **manage.html** (Admin Panel)
**What it does:** Password-protected admin panel for managing announcements, inventory, and featured products.

**Access:** Go to `kenjieminimart.com/manage` (requires password)  
**Password:** `Thepowerofsix_13`

**Features:**
- **Manage Announcements:** Add, edit, delete announcements with timestamps
- **Update Inventory:** Upload CSV file to see products locally
- **Manage Featured Products:** Checkbox list to select which products get Featured = 1

**Important:**
- All changes are local only (stored in browser)
- To make changes go live, you must upload updated CSV to GitHub
- GitHub auto-sync not yet implemented (see KNOWN LIMITATIONS below)

---

### 3. **inventory.csv** (Product Data)
**Location:** GitHub root (plutodx/kenjie-minimart/inventory.csv)

**Format:**
```
ID,Name,Category,Supplier,Price,Puhunan,Stock,Profit per piece,Margin %,Featured
1,"Jack n Jill Chips",Snacks,"Puregold",20,16.2,,3.80,19.0,1
2,"Oishi Crackers",Snacks,"Puregold",9,8,,1.00,11.1,0
```

**Columns:**
- `ID` — unique product identifier
- `Name` — product name
- `Category` — product category (used for filter tabs)
- `Supplier` — supplier name
- `Price` — retail price in PHP
- `Puhunan`, `Stock`, `Profit per piece`, `Margin %` — cost tracking (for your reference)
- `Featured` — **1 = show on homepage, 0 = don't show**

**How to update:**
1. Edit inventory.csv locally or in Excel
2. Set Featured = 1 for products you want on homepage
3. Upload to GitHub (replace existing inventory.csv)
4. Website auto-pulls within 2-5 minutes

---

### 4. **favicon.png** (Logo)
**Location:** GitHub root  
**What it is:** The pink circular Kenjie Minimart logo in browser tabs

**How to update:**
1. Export logo as favicon.png (PNG format)
2. Upload to GitHub root
3. Commit & push

---

## HOW TO MODIFY & UPDATE

### Update Product Prices & Inventory

1. **Export from POS:**
   - Go to your POS system inventory tab
   - Export as CSV
   - Should have columns: ID, Name, Category, Supplier, Price, ..., Featured

2. **Upload to GitHub:**
   - Go to github.com/plutodx/kenjie-minimart
   - Click "Add file" → "Upload files"
   - Select your CSV
   - Name it exactly: `inventory.csv`
   - Commit & push

3. **Website updates automatically:**
   - Within 2-5 minutes, the live site pulls the new CSV
   - All customers see updated prices & products

---

### Mark Products as Featured

**Option A — Via Admin Panel:**
1. Go to kenjieminimart.com/manage
2. Enter password: `Thepowerofsix_13`
3. Scroll to "Manage Featured Products"
4. Check boxes next to products you want featured
5. Click "Save Featured Products"
6. Export your updated CSV from the admin panel
7. Upload to GitHub (replace inventory.csv)

**Option B — Direct CSV Edit:**
1. Open inventory.csv in Excel or Google Sheets
2. Find the "Featured" column (last column)
3. Change to 1 for products you want featured, 0 for others
4. Save as inventory.csv
5. Upload to GitHub

**Featured Products Display:**
- Shown as a grid on the Announcements tab homepage
- If no products marked as featured, defaults to first 6 items
- Customers see all products in Price Lookup tab regardless

---

### Add/Edit Announcements

1. **Via Admin Panel:**
   - Go to kenjieminimart.com/manage
   - Enter password: `Thepowerofsix_13`
   - Click "Manage Announcements"
   - Click "Add Announcement" button
   - Type your message
   - Click "Add"

2. **Examples:**
   - "Fresh supplies arrived! Check prices in Price Lookup"
   - "Temporarily out of stock: Cooking Oil"
   - "Special weekend promo: Buy 2 instant noodles, get 1 free"

**Note:** Announcements are stored locally in your browser, not synced to GitHub. They don't appear for other customers or devices.

---

### Update Logo/Favicon

1. **Export your Kenjie Minimart logo:**
   - Format: PNG
   - Size: 32x32px or larger
   - Save as: favicon.png

2. **Upload to GitHub:**
   - Go to github.com/plutodx/kenjie-minimart
   - Click "Add file" → "Upload files"
   - Select favicon.png
   - Commit & push

3. **Website updates:**
   - Appears in browser tabs within minutes
   - Clear cache if you don't see it immediately

---

## CONTACT FORM (Message Us Tab)

**How it works:**
- Customers fill in name (optional), phone (optional), message (required)
- Form submissions go to Netlify Forms
- Emails sent to your registered Netlify account

**To receive submission emails:**
1. Go to netlify.com → your site → Forms
2. Add your email address in notification settings
3. Netlify will email you when customers submit messages

---

## GITHUB SETUP & HOW TO PUSH FILES

### To Update Files

**Easiest — GitHub Web UI:**
1. Go to github.com/plutodx/kenjie-minimart
2. Click on the file you want to update (e.g., inventory.csv)
3. Click the pencil icon (edit)
4. Paste your new content
5. Scroll down → click "Commit changes"
6. Add a commit message (e.g., "Update prices - June 9")
7. Click "Commit"

**Using Git (command line):**
1. Clone repo: `git clone https://github.com/plutodx/kenjie-minimart.git`
2. Update files locally
3. `git add .`
4. `git commit -m "Update inventory"`
5. `git push origin main`

---

## NETLIFY DEPLOYMENT

**How it works:**
- Every time you push to GitHub (main branch), Netlify automatically rebuilds the site
- Takes 30 seconds to 2 minutes
- Your site updates without doing anything

**To check deployment status:**
1. Go to netlify.com → your site
2. Look at "Deploys" tab
3. Green checkmark = live

---

## KNOWN LIMITATIONS & TODO

### GitHub Token Sync NOT Implemented

**Status:** Automatic syncing from /manage to GitHub is disabled due to token security issues.

**What this means:**
- You can manage everything in `/manage` locally
- But changes don't automatically push to GitHub
- You must manually upload files to GitHub for the live site to update

**Workaround (Current):**
1. Update inventory/announcements in `/manage`
2. Export or save the updated CSV
3. Upload to GitHub manually (click "Add file" → "Upload files")

**Future Solution (TODO):**
- Move GitHub token to Netlify environment variables (secure)
- Create a Netlify Function to handle syncs server-side
- Timeline: TBD — but manual uploads work fine for now

---

## QUICK REFERENCE

**Public Site:** kenjieminimart.com  
**Admin Panel:** kenjieminimart.com/manage  
**Admin Password:** Thepowerofsix_13  
**GitHub Repo:** github.com/plutodx/kenjie-minimart  
**Store Phone:** 0975 776 0971  
**Store Address:** Purok 3 Macasandal Along the Highway  

**Owner Profile Link:** clarencegono.com (shown in header & footer)

---

## NEXT STEPS (After Going Live)

1. Add your first announcement in /manage
2. Test the contact form by submitting a message
3. Upload real inventory CSV to GitHub
4. Set Featured = 1 for products you want on homepage
5. Share kenjieminimart.com link with customers
6. Update prices in CSV whenever inventory changes in POS

---

## COLOR SCHEME

- Primary Pink: #E5358B (main brand color)
- Deep Pink: #BD2470 (hover/active states)
- Light Pink BG: #FFF5FA (header/nav background)
- White: #FFFFFF (cards, modals)
- Dark Gray: #333333 (text)
- Light Gray: #FAFAFA (page background)

---

**Built:** June 9, 2026  
**Last Updated:** June 9, 2026 (Featured column added, token sync parked)  
**Hosting:** Netlify + GitHub + Hostinger DNS
