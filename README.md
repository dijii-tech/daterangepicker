# DIJI Date Range Picker

A JavaScript component for choosing date ranges, dates and times. This is a fork of [Date Range Picker](https://www.daterangepicker.com/) with additional features.

## ✨ Key Enhancements

- 📅 **Holidays Feature** - Visual holiday marking with collapsible header list
- 🌍 **Localization Support** - Full locale support including holiday labels
- 📌 **Inline Mode** - Display calendar permanently without input field
- ⚡ **First Date Callback** - React immediately to user's first date selection

## Features Added

### 1. Inline Mode
You can now use the date range picker as an inline component without requiring an input field. This is useful when you want to display the calendar permanently on the page.

```javascript
$('#inline-datepicker').daterangepicker({
    inline: true,
    autoApply: true,
    startDate: moment().startOf('hour'),
    endDate: moment().startOf('hour').add(32, 'hour')
});
```

### 2. Holidays Feature
Mark and display holidays in the calendar with visual highlighting and optional header list.

#### Basic Holiday Usage
```javascript
$('#datepicker').daterangepicker({
    holidays: [
        // Single date formats
        '2025-01-01',  // Simple string format
        { date: '2025-07-04', name: 'Independence Day' },  // With name
        { date: '2025-12-25', name: 'Christmas', class: 'special' },  // With custom class

        // Holiday range formats (NEW!)
        {
            startDate: '2025-07-20',
            endDate: '2025-07-24',
            name: 'Summer Break Week'
        },
        {
            range: ['2025-12-24', '2025-12-26'],  // Alternative array format
            name: 'Christmas Holiday Period'
        }
    ]
});
```

#### Holiday Header
Display a collapsible header showing all holidays in visible months:

```javascript
$('#datepicker').daterangepicker({
    holidays: [
        { date: '2025-01-01', name: 'New Year\'s Day' },
        { date: '2025-07-04', name: 'Independence Day' }
    ],
    showHolidayHeader: true,
    locale: {
        holidayLabel: 'Holidays'  // Customize the header label
    }
});
```

**Features:**
- Visual highlighting of holiday dates
- **Holiday ranges** - Define multi-day holiday periods
- Tooltip support for holiday names
- Collapsible header with holiday list
- Automatically filters holidays for visible months
- Localization support
- Custom CSS classes per holiday

**Examples:**
- See `example-holidays.html` for comprehensive examples
- See `HOLIDAYS_FEATURE.md` for detailed documentation
- See `HOLIDAY_HEADER_FEATURE.md` for Turkish documentation

#### Localization Example (Turkish)
```javascript
$('#datepicker').daterangepicker({
    holidays: [
        { date: '2025-01-01', name: 'Yılbaşı' },
        { date: '2025-04-23', name: 'Ulusal Egemenlik ve Çocuk Bayramı' },
        { date: '2025-10-29', name: 'Cumhuriyet Bayramı' }
    ],
    showHolidayHeader: true,
    locale: {
        format: 'DD/MM/YYYY',
        holidayLabel: 'Tatiller',
        applyLabel: 'Uygula',
        cancelLabel: 'İptal',
        daysOfWeek: ['Paz', 'Pzt', 'Sal', 'Çar', 'Per', 'Cum', 'Cmt'],
        monthNames: ['Ocak', 'Şubat', 'Mart', 'Nisan', 'Mayıs', 'Haziran',
                    'Temmuz', 'Ağustos', 'Eylül', 'Ekim', 'Kasım', 'Aralık']
    }
});
```

### 3. onFirstDateSelected Callback
A new callback function that fires immediately when the first date is selected, without waiting for the "Apply" button to be clicked. This is useful for scenarios where you need to perform actions (like fetching data, updating UI, or making API calls) as soon as the user selects the start date.

#### Usage
```javascript
$('#daterange').daterangepicker({
    startDate: moment().subtract(6, 'days'),
    endDate: moment(),

    // Fires immediately when first date is selected (before Apply)
    onFirstDateSelected: function(firstDate) {
        console.log('First date selected:', firstDate.format('YYYY-MM-DD'));

        // Example: Fetch data for the selected start date
        fetchDataForDate(firstDate);

        // Example: Update UI elements
        updateDashboard(firstDate);
    }
}, function(start, end, label) {
    // Standard callback - fires when Apply is clicked or selection is complete
    console.log('Date range applied:', start.format('YYYY-MM-DD'), 'to', end.format('YYYY-MM-DD'));
});
```

#### Real-World Example
```javascript
// Load data immediately when user selects the first date
$('#report-daterange').daterangepicker({
    onFirstDateSelected: function(firstDate) {
        // Show loading indicator
        $('#loading').show();

        // Fetch preliminary data for the start date
        $.ajax({
            url: '/api/data',
            data: { startDate: firstDate.format('YYYY-MM-DD') },
            success: function(data) {
                updatePreview(data);
                $('#loading').hide();
            }
        });
    }
}, function(start, end) {
    // Final data load when complete range is selected
    loadCompleteRangeData(start, end);
});
```

The callback receives a Moment.js object representing the selected first date, allowing you to format and use it as needed. See `example-first-date-callback.html` for interactive examples.

## Quick Start

### Include Files via CDN
```html
<!-- CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/dijii-tech/daterangepicker@latest/daterangepicker.min.css">

<!-- Dependencies -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.22.1/moment.min.js"></script>

<!-- Date Range Picker -->
<script src="https://cdn.jsdelivr.net/gh/dijii-tech/daterangepicker@latest/daterangepicker.min.js"></script>
```

### Basic Usage
```javascript
// Basic
$('input[name="daterange"]').daterangepicker();

// With options
$('input[name="daterange"]').daterangepicker({
    startDate: moment().startOf('hour'),
    endDate: moment().startOf('hour').add(32, 'hour')
});

// Inline mode
$('#calendar-container').daterangepicker({
    inline: true,
    autoApply: true
});
```

## API Reference

### New Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `inline` | Boolean | `false` | Display calendar inline without input field |
| `holidays` | Array | `[]` | Array of holiday dates (strings or objects) |
| `showHolidayHeader` | Boolean | `false` | Show collapsible header with holiday list |
| `onFirstDateSelected` | Function | `null` | Callback when first date is selected |

### Locale Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `holidayLabel` | String | `'Holidays'` | Label for holiday header toggle |

### Holiday Object Formats

#### Single Date Holiday
```javascript
{
    date: 'YYYY-MM-DD',     // Required: Holiday date
    name: 'Holiday Name',   // Optional: Display name (shown in tooltip and header)
    class: 'custom-class'   // Optional: Custom CSS class
}
```

#### Holiday Range (Format 1: startDate/endDate)
```javascript
{
    startDate: 'YYYY-MM-DD',  // Required: Range start date
    endDate: 'YYYY-MM-DD',    // Required: Range end date
    name: 'Holiday Period'    // Optional: Display name
}
```

#### Holiday Range (Format 2: range array)
```javascript
{
    range: ['YYYY-MM-DD', 'YYYY-MM-DD'],  // Required: [startDate, endDate]
    name: 'Holiday Period'                 // Optional: Display name
}
```

## Examples

- **`demo.html`** - Interactive configuration builder with all features
- **`example-holidays.html`** - Comprehensive holiday feature examples (7 examples)
- **`example-first-date-callback.html`** - First date callback examples

## Documentation Files

- **`HOLIDAYS_FEATURE.md`** - Complete holiday feature documentation (English)
- **`HOLIDAY_HEADER_FEATURE.md`** - Holiday header documentation (Turkish)
- Original documentation: [https://www.daterangepicker.com/](https://www.daterangepicker.com/)

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- IE 11 (with polyfills)

## Credits
- Original project by Dan Grossman: [Date Range Picker](https://www.daterangepicker.com/)
- Inline mode, holidays feature, and other enhancements by DIJI Tech

## License
MIT License