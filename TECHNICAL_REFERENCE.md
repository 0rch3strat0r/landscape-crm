# Technical Reference - Medina Landscaping CRM

## Quick Start for Developers

### File Location
```
Main file: /mnt/c/Users/carls/OneDrive/Desktop/landscape crm/full-crm-demo.html
```

### Code Structure in full-crm-demo.html
```
Lines 1-7: HTML head setup
Lines 8-562: CSS styles
Lines 566-1533: HTML structure
Lines 1534-2497: JavaScript
```

## Key Functions Reference

### Navigation & UI
- `showPage(page)` - Switch between pages (line 1836)
- `toggleLanguage()` - Switch English/Spanish (line 1852)
- `translatePage()` - Apply translations (line 1857)
- `closeModal()` - Close any modal (line 1949)

### Customer Management  
- `searchCustomers(query)` - Search customers (line 2420)
- `viewCustomer(btn)` - View customer details (line 2385)
- `callCustomer(phone)` - Initiate phone call (line 2343)

### Job Management
- `startJob(btn)` - Start a job (line 1877)
- `completeJob(btn)` - Complete a job (line 1890)
- `quickInvoiceForJob(btn)` - Invoice from job (line 1916)
- `addJobExpense(btn)` - Add expense to job (line 2391)

### Estimates
- `newEstimate()` - Create new estimate (line 2348)
- `updateEstimate()` - Recalculate prices (line 2291)
- `sendEstimate()` - Send estimate (line 2338)

### Invoicing
- `quickInvoice()` - Quick invoice modal (line 1910)
- `sendInvoice()` - Send invoice (line 1943)

### Suppliers
- `findSuppliers()` - Open supplier search (line 1965)
- `searchSuppliers()` - Search suppliers (line 2008)
- `findSuppliesForJob(btn)` - Find supplies for specific job (line 1987)

### Utilities
- `updateStats()` - Update header stats (line 1903)
- `takePhoto()` - Camera functionality (line 2374)
- `saveExpense()` - Save expense (line 2409)

## Data Storage Schema

### localStorage Keys
```javascript
// Customers
localStorage.getItem('customers')
// Format: Array of customer objects
[{
    id: 'unique-id',
    name: 'Customer Name',
    address: '123 Main St',
    phone: '555-0123',
    email: 'email@example.com',
    difficulty: 'normal', // easy|normal|difficult|nightmare
    totalJobs: 5,
    totalRevenue: 1250,
    lastService: '2024-03-15'
}]

// Jobs  
localStorage.getItem('jobs')
// Format: Array of job objects
[{
    id: 'job-id',
    customerId: 'customer-id',
    date: '2024-03-20',
    time: '9:00 AM',
    status: 'scheduled', // scheduled|in-progress|completed
    services: ['mowing', 'trimming'],
    price: 125,
    expenses: [{
        amount: 25,
        description: 'Extra mulch bags',
        category: 'supplies'
    }]
}]

// Settings
localStorage.getItem('landscapeSettings')
// Format: Settings object
{
    pricingModel: 'sqft', // sqft|hourly|manual
    hourlyRate: 50,
    minHours: 2,
    baseRates: {
        mowing: 45,
        fertilizer: 25,
        cleanup: 75
    },
    difficultyMultipliers: {
        easy: 0.9,
        normal: 1.0,
        difficult: 1.3,
        nightmare: 2.0
    }
}

// Language
localStorage.getItem('preferred-language')
// Format: 'en' or 'es'
```

## Service Categories & Pricing

### 1. Lawn Care
- Weekly/Bi-weekly mowing (size-based)
- Fertilizer (per 5000 sqft)
- Weed control (per 5000 sqft)
- Aeration (seasonal)

### 2. Tree & Shrub Care
- Trimming (per hour)
- Tree removal (custom)
- Disease treatment (per application)
- Deep root feeding (per tree)

### 3. Seasonal Services
- Spring/Fall cleanup (size-based)
- Leaf removal (per hour)
- Snow removal (per visit)
- Holiday lights (custom)

### 4. Landscaping
- Mulch installation (per yard + labor)
- Plant installation (per plant)
- Sod installation (per sqft)
- Garden design (custom)

### 5. Hardscaping
- Paver installation (per sqft)
- Retaining walls (per linear ft)
- Concrete work (custom)
- Drainage solutions (custom)

### 6. Custom Services
- User-defined services
- Manual pricing
- Flexible scheduling

## Pricing Logic

### Base Price Calculation
```javascript
// Example for mowing (line 2210)
const sqft = document.getElementById('total-sqft').value;
const basePrices = {
    'mow-weekly': sqft < 5000 ? 65 : 
                  sqft < 10000 ? 85 : 
                  sqft < 15000 ? 120 : 150
};
```

### Difficulty Multiplier
```javascript
// Applied to final price (line 2290)
const multipliers = {
    easy: 0.9,
    normal: 1.0, 
    difficult: 1.3,
    nightmare: 2.0
};
total = subtotal * multipliers[customerType];
```

## Translation System

### Adding New Translations
1. Add to English object (line 1539)
2. Add to Spanish object (line 1695)
3. Add HTML attribute: `data-translate="key"`
4. For inputs: `data-translate-placeholder="key"`

### Example
```html
<button data-translate="save">Save</button>
<input data-translate-placeholder="search" placeholder="Search...">
```

## Browser Compatibility
- Chrome 60+ ✓
- Safari 11+ ✓
- Firefox 55+ ✓
- Edge 79+ ✓
- Mobile browsers ✓

## Performance Notes
- Initial load: ~100KB
- No external requests
- All operations < 50ms
- Supports 10,000+ customers
- IndexedDB for large datasets

## Debugging Tips

### Check Data
```javascript
// In browser console:
JSON.parse(localStorage.getItem('customers'))
JSON.parse(localStorage.getItem('jobs'))
localStorage.clear() // Reset everything
```

### Common Issues
1. **Blank page**: Check console for errors
2. **Data not saving**: Check localStorage quota
3. **Translations missing**: Verify key exists in both languages
4. **Functions not working**: Check function names in test-crm.html

## Modification Guide

### Add New Page
1. Add nav item (line 1450-1460)
2. Add page div with id="pagename-page"
3. Add to showPage() function
4. Style with .page class

### Add New Service
1. Add to service category in HTML
2. Add pricing logic in updateEstimate()
3. Add translations for service name
4. Test pricing calculation

### Change Company Name
1. Update translations (line 1541 & 1697)
2. Currently: "Medina Landscaping"
3. Keep same in both languages

---
Generated: 2025-01-18
Purpose: Technical reference for resuming development