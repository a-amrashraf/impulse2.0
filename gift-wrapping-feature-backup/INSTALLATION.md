# Gift Wrapping Feature - Installation Guide

## 📦 Overview
A complete, smart gift wrapping system for Shopify that allows customers to add gift wrapping to individual cart items. The wrapping product automatically adjusts quantity based on customer selections.

**Features:**
- ✅ Per-item wrapping selection with checkboxes
- ✅ Automatic quantity management
- ✅ Persistent selections across page loads (localStorage)
- ✅ Collapsible accordion UI
- ✅ Full theme settings control
- ✅ AJAX cart integration
- ✅ Smart duplicate prevention
- ✅ Wraps for multiple items of the same product

---

## 🚀 Installation Instructions

### Step 1: Create Wrapping Product in Shopify Admin

1. Go to **Products → Add product**
2. Create a product with these details:
   - **Title**: `Special Wrapping` (or your preferred name)
   - **Price**: Your wrapping price (e.g., $5.00)
   - **Handle**: `special-wrapping` (IMPORTANT: Use this exact handle)
   - Add product image and description as desired
3. **Publish** the product

---

### Step 2: Add Wrapping Snippet

1. In Shopify Admin, go to **Online Store → Themes → Actions → Edit code**
2. In the **Snippets** folder, click **Add a new snippet**
3. Name it: `cart-gift-wrapping`
4. Copy the entire contents of `cart-gift-wrapping.liquid` from this backup folder
5. Paste into the new snippet and **Save**

---

### Step 3: Add JavaScript Manager to Theme Layout

1. In the **Layout** folder, open `theme.liquid`
2. Scroll to the bottom, just **before the closing `</body>` tag**
3. Copy the entire contents of `gift-wrapping-manager.liquid` from this backup folder
4. Paste it before `</body>` and **Save**

---

### Step 4: Add to Cart Drawer

1. In the **Snippets** folder, open `cart-drawer.liquid`
2. Find the section that displays cart items (look for `<div data-products>`)
3. After the cart items div, add this code:

```liquid
<div data-gift-wrapping-slot>
  {%- render 'cart-gift-wrapping' -%}
</div>
```

**Example placement:**
```liquid
<div class="drawer__scrollable">
  <div data-products class="appear-animation appear-delay-2"></div>

  <div data-gift-wrapping-slot>
    {%- render 'cart-gift-wrapping' -%}
  </div>

  {% if settings.cart_notes_enable %}
    <!-- Cart notes code -->
  {% endif %}
```

4. **Save** the file

---

### Step 5: Add Theme Settings

1. In the **Config** folder, open `settings_schema.json`
2. Find the **Cart** section (search for `"name": "Cart"` or similar)
3. Inside the `settings` array for Cart, add the contents of `settings-schema-additions.json`
4. Place it before the closing `]` of the Cart section
5. **Save** the file

**Example:**
```json
{
  "name": "Cart",
  "settings": [
    {
      "type": "select",
      "id": "cart_type",
      "label": "Cart type",
      ...
    },
    // ... other cart settings ...
    
    // ADD THE GIFT WRAPPING SETTINGS HERE
    {
      "type": "header",
      "content": "Gift Wrapping Options"
    },
    {
      "type": "checkbox",
      "id": "cart_wrapping_enable",
      "label": "Enable gift wrapping",
      "default": true
    },
    // ... rest of wrapping settings ...
  ]
}
```

---

### Step 6: Enable in Theme Customizer

1. Go to **Online Store → Themes → Customize**
2. Navigate to **Theme Settings → Cart**
3. Scroll to **Gift Wrapping Options**
4. Check **Enable gift wrapping** ✓
5. Verify **Wrapping product handle** is set to: `special-wrapping`
6. Customize the text, font, and colors as desired
7. Click **Save**

---

## 🎨 Customization Options

### Theme Settings Available:

| Setting | Description | Default |
|---------|-------------|---------|
| Enable gift wrapping | Toggle feature on/off | ON |
| Wrapping product handle | Product handle to use | `special-wrapping` |
| Wrapping checkbox label | Text displayed in header | "Add special gift wrapping" |
| Wrapping text font | Choose font family | Body font |
| Wrapping text font size | Size in pixels | 14px |
| Wrapping text color | Text color | #000000 |

### Visual Customization:

To modify the appearance, edit `cart-gift-wrapping.liquid` in the Snippets folder:

- **Container spacing**: `.cart-gift-wrapping` → `margin`, `padding`
- **Item cards**: `.wrapping-item` → `gap`, `padding`, `margin-bottom`
- **Checkbox size**: `.wrapping-checkbox` → `width`, `height`
- **Font sizes**: `.wrapping-item-label`, `.wrapping-item-title`
- **Product images**: `.wrapping-item-image` → `width`, `height`
- **Toggle button**: `.wrapping-toggle-btn` → `width`, `height`, `font-size`

---

## 🔧 How It Works

### Customer Experience:

1. Customer adds products to cart
2. In cart drawer, sees collapsible "🎁 Add special gift wrapping" section
3. Clicks to expand and sees list of cart items
4. Checks boxes for items they want wrapped
5. Wrapping product automatically added with correct quantity
6. Selections persist across page reloads

### Technical Flow:

1. **Detection**: JavaScript detects wrapping checkboxes in cart
2. **State Management**: Selections stored in localStorage by variant ID
3. **Quantity Calculation**: Sums quantities of all checked items
4. **Cart API**: Uses AJAX to add/update/remove wrapping product
5. **Smart Sync**: Prevents wrapping product from appearing in its own list
6. **Auto Refresh**: Updates cart UI after changes

---

## 📁 File Structure

```
gift-wrapping-feature-backup/
├── INSTALLATION.md                      ← You are here
├── cart-gift-wrapping.liquid            ← Snippet with UI and styles
├── gift-wrapping-manager.liquid         ← JavaScript manager
├── settings-schema-additions.json       ← Theme settings config
└── README.md                            ← Feature overview (optional)
```

---

## 🐛 Troubleshooting

### Wrapping section not appearing?
- ✅ Check **Enable gift wrapping** is ON in Theme Settings → Cart
- ✅ Verify product handle is `special-wrapping`
- ✅ Make sure product is published and available
- ✅ Clear browser cache and hard reload (Ctrl+Shift+R)

### Quantity not updating correctly?
- ✅ Check browser console for JavaScript errors (F12)
- ✅ Verify wrapping product has sufficient inventory
- ✅ Clear localStorage: Run `localStorage.removeItem('gift_wrapping_variant_ids')` in console

### Wrapping product appears in the wrapping list?
- ✅ The system should automatically hide it
- ✅ Verify the product handle is exactly `special-wrapping`
- ✅ Check that `_gift_wrapping: true` property is being added

### Selections not persisting?
- ✅ Make sure localStorage is enabled in the browser
- ✅ Check if privacy/incognito mode is blocking storage
- ✅ Verify JavaScript is not being blocked

### Multiple wrapping containers appearing?
- ✅ The system has built-in duplicate prevention
- ✅ Check that you only included the wrapping render once
- ✅ Clear browser cache

---

## 🔄 Updating/Removing

### To Update:
1. Edit `snippets/cart-gift-wrapping.liquid` for UI changes
2. Edit the JavaScript in `layout/theme.liquid` for logic changes
3. Modify `config/settings_schema.json` for new settings

### To Temporarily Disable:
1. Go to **Theme Settings → Cart**
2. Uncheck **Enable gift wrapping**
3. Save

### To Completely Remove:
1. Delete `snippets/cart-gift-wrapping.liquid`
2. Remove the JavaScript block from `layout/theme.liquid` (lines with `{% if settings.cart_wrapping_enable %}` to `{% endif %}`)
3. Remove the wrapping code from `snippets/cart-drawer.liquid`
4. Remove the settings from `config/settings_schema.json`
5. Optionally: Delete or unpublish the wrapping product

---

## 💡 Advanced Customization

### Change the wrapping product handle:
If you want to use a different product:
1. Update **Wrapping product handle** in Theme Settings
2. Update the default in `settings_schema.json` if desired

### Add bulk wrapping option:
Instead of per-item, add a single checkbox for all items:
1. Modify the snippet to show one checkbox
2. Set quantity = total cart items
3. Simplify the UI (remove per-item list)

### Customize validation messages:
Edit the `validateWrappingQuantity()` method in the JavaScript manager to change alert messages.

### Add visual indicators:
Modify `.wrapping-item` styles to show checked state:
```css
.wrapping-item:has(.wrapping-checkbox:checked) {
  background-color: #e8f5e9;
  border-color: #4caf50;
}
```

---

## 📞 Support

For issues or questions:
1. Check this INSTALLATION.md file thoroughly
2. Review browser console for errors (F12)
3. Verify all steps were completed correctly
4. Test in incognito mode to rule out caching issues

---

## ✅ Checklist

Before going live, verify:
- [ ] Wrapping product created with handle `special-wrapping`
- [ ] Snippet `cart-gift-wrapping` added
- [ ] JavaScript manager added to `layout/theme.liquid`
- [ ] Wrapping render added to `cart-drawer.liquid`
- [ ] Theme settings added to `settings_schema.json`
- [ ] Feature enabled in Theme Customizer
- [ ] Tested adding items to cart
- [ ] Tested checking/unchecking wrap boxes
- [ ] Tested quantity updates
- [ ] Tested page reload (selections persist)
- [ ] Tested on mobile devices

---

## 🎉 You're Done!

The gift wrapping feature should now be fully functional. Customers can select individual items to wrap, and the system will automatically manage the wrapping product quantity in the cart.

**Enjoy your new feature!**
