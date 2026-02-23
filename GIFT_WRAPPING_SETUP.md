# Gift Wrapping Feature - Setup Guide

## Overview
A smart, dynamic gift wrapping system that automatically manages wrapping products in your cart based on customer selections.

## Features
✅ Automatic quantity management
✅ Per-item or bulk wrapping modes
✅ Full theme settings control
✅ Smart cart integration
✅ Automatic wrapping removal when unchecked

## Setup Instructions

### 1. Product Configuration
Your wrapping product is already set up:
- **Product URL**: https://heliostreetwear.com/products/special-wrapping
- **Handle**: `special-wrapping`

### 2. Theme Settings (Admin Panel)
Go to **Online Store > Themes > Customize > Theme Settings > Cart**

#### Gift Wrapping Options:
- **Enable gift wrapping**: Toggle on/off
- **Wrapping product handle**: `special-wrapping` (already configured)
- **Wrapping checkbox label**: Customize the text (default: "Add special gift wrapping")
- **Wrapping text font**: Choose from:
  - Body font
  - Header font
  - Poppins
- **Wrapping text font size**: 12px - 24px (default: 14px)
- **Wrapping text color**: Pick any color
- **Enable per-item wrapping**: 
  - **OFF** (default): One checkbox for all items
  - **ON**: Separate checkbox for each cart item

### 3. How It Works

#### Bulk Mode (Default)
- Single checkbox: "🎁 Add special gift wrapping"
- Adds wrapping with quantity = total cart items
- Unchecking removes wrapping from cart

#### Per-Item Mode
- Individual checkboxes for each product
- Shows product thumbnail and name
- Wrapping quantity = sum of checked items
- Smart quantity adjustment

### 4. Customer Experience

**When customer checks the box:**
1. Wrapping product automatically added to cart
2. Quantity matches number of items to wrap
3. Cart updates without page reload

**When customer unchecks:**
1. Wrapping product removed from cart
2. Clean, automatic removal

**Quantity adjustments:**
- If customer changes product quantities, wrapping auto-updates
- If cart items change, wrapping adjusts accordingly

### 5. Customization Examples

#### Example 1: Simple Setup
```
Label: "Add gift wrapping (+$5)"
Font: Body font
Size: 14px
Color: #000000
Mode: Bulk (one checkbox)
```

#### Example 2: Premium Setup
```
Label: "🎁 Premium Gift Wrap - Make it special!"
Font: Poppins
Size: 16px
Color: #D4AF37 (gold)
Mode: Per-item (individual selection)
```

### 6. Technical Details

**Files Modified:**
- `config/settings_schema.json` - Theme settings
- `snippets/cart-gift-wrapping.liquid` - Main wrapping feature
- `snippets/cart-drawer.liquid` - Drawer cart integration
- `sections/main-cart.liquid` - Cart page integration

**Smart Features:**
- Detects wrapping product by handle
- Prevents infinite loops
- Handles edge cases (empty cart, quantity changes)
- Works with both drawer and page carts
- API-based cart updates (no page reloads)

### 7. Troubleshooting

**Wrapping not appearing?**
- Check "Enable gift wrapping" is ON in theme settings
- Verify product handle is correct: `special-wrapping`
- Make sure product is published and available

**Quantity not updating?**
- Clear browser cache
- Check browser console for errors
- Verify product has inventory available

**Styling issues?**
- Adjust font size in theme settings
- Choose different font family
- Modify text color for better contrast

### 8. Advanced Customization

Want to customize further? Edit the file:
`snippets/cart-gift-wrapping.liquid`

You can modify:
- Checkbox styles (`.wrapping-checkbox`)
- Container appearance (`.cart-gift-wrapping`)
- Label text and icons
- Additional logic/conditions

## Support Notes

The system is designed to be "smart" and handles:
- Multiple items selection
- Quantity changes
- Item removals
- Cart clearing
- Different cart types (drawer/page)

All controlled through Theme Settings - no code editing needed for basic customization!
