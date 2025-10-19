# DIJI Date Range Picker

A JavaScript component for choosing date ranges, dates and times. This is a fork of [Date Range Picker](https://www.daterangepicker.com/) with additional features.

## Features Added

### Inline Mode
You can now use the date range picker as an inline component without requiring an input field. This is useful when you want to display the calendar permanently on the page.

```javascript
$('#inline-datepicker').daterangepicker({
    inline: true,
    autoApply: true,
    startDate: moment().startOf('hour'),
    endDate: moment().startOf('hour').add(32, 'hour')
});
```

### onFirstDateSelected Callback
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

## Documentation
For complete documentation, usage, and examples, visit the original project website:
[https://www.daterangepicker.com/](https://www.daterangepicker.com/)

## Credits
- Original project by Dan Grossman: [Date Range Picker](https://www.daterangepicker.com/)
- Inline mode and other enhancements by DIJI Tech

## License
MIT License