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