# Ohio School Districts Interactive Map

An interactive map showing all 612 Ohio school districts with hover functionality to display district information. Built for the [Vouchers Hurt Ohio](https://vouchershurtohio.com/) coalition.

## Live Demo

*(Add your GitHub Pages URL here after deployment)*

## Features

- ✅ Interactive hover to show district info (name, IRN, county, tax ID)
- ✅ Coalition member highlighting (green for members, blue for others)
- ✅ Side panel with district details
- ✅ Click to zoom into a district
- ✅ Responsive design for mobile
- ✅ Clean, professional styling

## Quick Start

### 1. Download the GeoJSON data

**Option A: From the API Explorer (Recommended)**
1. Go to: https://ohio-framework-datasets-geohio.hub.arcgis.com/datasets/13c69be53f854a3cb5806a9422da2bf5/api
2. Click "Open in API Explorer"
3. Under "Output Options", set format to GeoJSON
4. Click "Get Response" and save the result

**Option B: Direct API URL**
```
https://maps.ohio.gov/arcgis/rest/services/Hosted/Ohio_School_Districts_2025/FeatureServer/0/query?where=1%3D1&outFields=*&outSR=4326&f=geojson
```
Open this URL in your browser and save the page as `ohio-school-districts.geojson`

### 2. Add the file to this project

Place `ohio-school-districts.geojson` in the same folder as `index.html`

### 3. Run locally

You need a local web server (browsers block loading local JSON files directly):

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .

# PHP
php -S localhost:8000
```

Then open http://localhost:8000 in your browser.

## Data Sources

### District Boundaries (GeoJSON)

| Resource | URL |
|----------|-----|
| Data Portal | https://ohio-framework-datasets-geohio.hub.arcgis.com/datasets/13c69be53f854a3cb5806a9422da2bf5/api |
| API (JSON) | `https://maps.ohio.gov/arcgis/rest/services/Hosted/Ohio_School_Districts_2025/FeatureServer/0/query?where=1%3D1&outFields=*&outSR=4326&f=json` |
| API (GeoJSON) | `https://maps.ohio.gov/arcgis/rest/services/Hosted/Ohio_School_Districts_2025/FeatureServer/0/query?where=1%3D1&outFields=*&outSR=4326&f=geojson` |

### Available Fields

| Field | Description |
|-------|-------------|
| `irn` | Ohio Information Retrieval Number (unique district ID) |
| `name` | District name |
| `taxid` | Tax ID |
| `countycode` | Ohio county code (1-88) |
| `SHAPE__Length` | Perimeter (not displayed) |
| `SHAPE__Area` | Area (not displayed) |
| `globalid` | Internal ID (not displayed) |

### Additional Data Sources

To add enrollment, funding, or performance data:

| Data Type | Source |
|-----------|--------|
| Enrollment Data | https://education.ohio.gov/Topics/Data/Frequently-Requested-Data/Enrollment-Data |
| Report Cards | https://reportcard.education.ohio.gov/download |
| All District Data | https://oeds.ode.state.oh.us/dataextract |

Match additional data to districts using the `IRN` field - it's the unique identifier used across all Ohio education data.

## Coalition Member List

The map highlights Vouchers Hurt Ohio coalition members in green. To update the list:

1. Get the current list from: https://vouchershurtohio.com/districts/
2. Edit `index.html` and find the `coalitionMembers` Set (around line 280)
3. Add district names in UPPERCASE, matching how they appear in the GeoJSON

Example:
```javascript
const coalitionMembers = new Set([
    'AKRON CITY',
    'TOLEDO CITY',
    'COLUMBUS CITY',
    // ... add all members
]);
```

## Deployment Options

### Option 1: GitHub Pages (Free, Recommended)

1. Push this repo to GitHub
2. Go to Settings → Pages
3. Set source to "main" branch
4. Your map will be live at `https://yourusername.github.io/VHO/`

**Note:** If the GeoJSON is over 25MB, use [mapshaper.org](https://mapshaper.org) to simplify it first.

### Option 2: WordPress Embed

Host the files somewhere (GitHub Pages, your server, a CDN) and embed with an iframe:

```html
<iframe 
    src="https://yourusername.github.io/VHO/" 
    width="100%" 
    height="700" 
    frameborder="0"
    title="Ohio School Districts Map">
</iframe>
```

### Option 3: WordPress Direct Integration

1. Upload `ohio-school-districts.geojson` to your WordPress media library
2. Use a plugin like "WPCode" to add the HTML/CSS/JS
3. Update the `GEOJSON_URL` in the JavaScript to point to your uploaded file

## File Structure

```
VHO/
├── index.html                      # Main map application
├── ohio-school-districts.geojson   # District boundaries (you add this)
└── README.md                       # This file
```

## Future Enhancements

- [ ] Add full coalition member list
- [ ] Include enrollment data on hover
- [ ] Add voucher impact data ($ lost per district)
- [ ] Search/filter functionality
- [ ] Accessibility improvements (keyboard navigation, screen reader support)
- [ ] Alternative table view for accessibility

## Technical Details

- **Mapping Library:** [Leaflet.js](https://leafletjs.com/) v1.9.4
- **Basemap:** CartoDB Positron (light theme)
- **Fonts:** Playfair Display (headings), Source Sans Pro (body)
- **No build process required** - pure HTML/CSS/JS

## License

- Map code: MIT License
- District boundary data: Public domain (Ohio OGRIP)
- Leaflet.js: BSD-2-Clause License

## Credits

- District boundaries from [Ohio Geographically Referenced Information Program (OGRIP)](https://ogrip.oit.ohio.gov/)
- Built for [Vouchers Hurt Ohio](https://vouchershurtohio.com/)
