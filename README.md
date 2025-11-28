# Data Extractor Chrome Extension

A powerful Chrome extension that automatically detects and collects unique phone numbers and email addresses from web pages with rich context information.

## Features

### 🔍 Comprehensive Data Extraction
- **Unique Detection**: Automatically identifies unique phone numbers and email addresses
- **Deep Scanning**: Scans all page elements including:
  - Visible text content
  - Hidden elements (buttons, inputs, code blocks)
  - HTML attributes (data-*, href, value, placeholder, title, alt, etc.)
  - `mailto:` and `tel:` links
  - Form fields and textareas
  - Code blocks (`<code>`, `<pre>`)

### 📊 Rich Data Context
Each extracted item includes:
- **Value**: The email or phone number
- **Context**: Nearby text that provides context (labels, parent text, aria-labels)
- **URL**: The page where it was found
- **Timestamp**: When it was detected (ISO 8601 format)

### 💾 Persistent Storage
- Data is saved and remembered until manually cleared
- Survives browser restarts
- Works across multiple tabs

### 🎯 Real-time UI Feedback
- **Bottom-right panel** shows:
  - Current extraction status
  - Total count of collected items
  - Check icon animation when new data is detected

### 🎛️ Popup Interface
- **Start/Stop Control**: Toggle extraction on/off
- **Live Statistics**: Separate counts for emails and phones
- **Data Preview**: View collected items with context
- **CSV Export**: Download all data with full details
- **Clear Data**: Reset storage with one click

### 📥 CSV Export
Download includes all fields:
- Type (email/phone)
- Value
- Context (nearby text)
- URL (source page)
- Timestamp

## Installation

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable **Developer mode** (toggle in top-right corner)
3. Click **Load unpacked**
4. Select the `data_extractor` directory
5. Pin the extension to your toolbar for easy access

## Usage

1. **Start Extraction**:
   - Click the extension icon
   - Click "Start Extraction" button
   - A panel will appear in the bottom-right corner

2. **Browse the Web**:
   - The extension automatically scans pages as you browse
   - Watch the counter increase as unique items are found
   - Check icon flashes when new data is detected

3. **View Collected Data**:
   - Click the extension icon to see statistics
   - Preview recent items with context
   - See separate counts for emails and phones

4. **Export Data**:
   - Click "Download CSV" to export all data
   - File includes: Type, Value, Context, URL, Timestamp

5. **Clear Data**:
   - Click "Clear Data" to reset storage
   - Confirmation not required (be careful!)

6. **Stop Extraction**:
   - Click "Stop Extraction" to pause scanning
   - Data remains saved

## Technical Details

### Regex Patterns
- **Email**: `/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/g`
- **Phone**: `/(?:\+?\d{1,3}[ -]?)?\(?\d{3}\)?[ -]?\d{3}[ -]?\d{4}/g`

### Context Extraction
The extension intelligently extracts context by:
1. Checking for associated labels (form elements)
2. Extracting nearby parent text (up to 100 chars)
3. Using aria-label or title attributes
4. Limiting context to prevent data bloat

### Storage
- Uses Chrome's `chrome.storage.local` API
- Serialized saving prevents race conditions
- No storage limits imposed by extension

### Performance
- Efficient MutationObserver for dynamic content
- Deduplication using Set data structure
- Background script handles concurrent saves

## File Structure

```
data_extractor/
├── manifest.json          # Extension configuration
├── background.js          # Service worker for data management
├── content.js            # Content script for page scanning
├── content.css           # Styles for injected UI
├── popup.html            # Extension popup interface
├── popup.js              # Popup logic
├── popup.css             # Popup styles
└── icons/                # Extension icons
    ├── icon16.png
    ├── icon48.png
    └── icon128.png
```

## Privacy & Security

- **No external servers**: All data stays local in your browser
- **No tracking**: Extension doesn't send data anywhere
- **Manual control**: You control when extraction starts/stops
- **Local storage only**: Data stored using Chrome's secure storage API

## Limitations

- Phone regex may need adjustment for international formats
- Context extraction limited to 100 characters
- Requires page reload for content scripts on existing tabs (first install)

## Future Enhancements

- Custom regex patterns
- Filter by domain
- Export to JSON
- Import/merge data
- Advanced search and filtering
- Duplicate detection across similar formats

## License

MIT License - Feel free to modify and distribute

## Support

For issues or feature requests, please contact the developer.
