# Green Building Evaluator

Full-featured desktop app for searching and rating green building projects. Offers a user-friendly interface to browse building sustainability information, certifications, and environmental performance indicators.

## Features

- **Advanced Search**: Smart search algorithm with fuzzy matching and multi-word capability
- **Project Rating System**: Automatic calculation of building sustainability ratings (1-10 scale)
- **Interactive Interface**: Simple, contemporary GUI with tabbed interface
- **Customizable Themes**: Several color themes with simple switching
- **Detailed Project Information**: Extensive overview of building certifications, energy efficiency, and sustainability features
- **Real-time Search Results**: Immediate feedback with clickable project listings

## Installation

### Prerequisites

Prior to executing the application, make sure to have Python 3.7+ on your system.

### Required Dependencies

Install the necessary Python packages with pip:

```bash
pip install customtkinter pandas openpyxl
```

**Package Details:**
- `customtkinter`: Fresh GUI framework for the user interface
- `pandas`: Library for data manipulation and analysis
- `openpyxl`: Reading and writing Excel files

### File Structure

Make sure that your project directory is structured as shown below:

```
Green-Building-Evaluator/
    ├── main.py                          # Main application entry point
    ├── App_Data/
```
│   ├── GetData.py                   # Data management and search logic
│   ├── widgets.py                   # Main tab interface components
│   ├── setting_frame.py             # Implementation of settings panel
│   ├── Database.xlsx                # Spreadsheet containing building data
│   └── themes/                      # Custom theme files (optional)
│       ├── custom_theme1.json
│       └── custom_theme2.json
├── settings.txt                     # Storage of theme preference
└── README.md                        # This document
```


## Database Setup

### Excel File Requirements

The application requires a file called `Database.xlsx` in the `App_Data/` folder. This Excel file must have building project data with the following structure:

**Required Column:**
- `ProjectName`: The building/project name (should be present)

**Optional Columns (for additional functionality):**
- `LEED_Rating`: LEED certification level
- `BREEAM_Rating`: BREEAM certification level
- `Green_Star_Rating`: Green Star certification level
- `Certification`: General certification details
- `Energy_Rating`: Energy efficiency rating
- `Energy_Efficiency`: Energy performance values
- `Solar_Panels`: Solar installation details
- `Renewable_Energy`: Renewable energy use
- `Water_Efficiency`: Water conservation practices
- `Waste_Management`: Waste reduction practices
- `Green_Roof`: Green roof installation
- `Rain_Water_Harvesting`: Rainwater harvesting systems
- `Location_Rating`: Location sustainability score
- `Transport_Access`: Transportation accessibility
- `Public_Transport`: Public transportation connectivity

### Sample Data Format

| ProjectName | LEED_Rating | Energy_Rating | Water_Efficiency | Location_Rating |
|-------------|-------------|---------------|------------------|-----------------|
| Empire State Building | Gold | A+ | Excellent | A |
| One World Trade Center | Platinum | A++ | Good | A |
| The Edge Amsterdam | Outstanding | 100% Renewable | Excellent | A |

## Usage Guide

### Starting the Application

1. **Start the application:**
   ```bash
   python main.py
   ```

2. **Loading Screen:**
   - The application shows a loading screen when processing the database
   - Progress indicators display:
- Reading Database
     - Processing project data
     - Optimizing search index
     - Finalizing

3. **Error Handling:**
   - If database loading fails, a retry button will appear
   - Check that `App_Data/Database.xlsx` exists and is correctly formatted

### Main Interface

The application includes a three-tab interface:

#### 1. Search Tab

**Search Functionality:**
- Type building or project names into the search box
- Press Enter or click "Search" to run
- Search is supported for:
  - Exact matches (most important)
  - Partial matches (all words exist)
  - Fuzzy matching (some words exist)
  - Individual word matching

**Search Examples:**
- ` "\"Empire State Building\""` - returns exact matches
- ` "\"Empire State\""` - returns buildings with both words
- `""Building"` - retrieves all projects containing "building" in the name
- `""LEED Gold"` - retrieves projects with LEED Gold certification

**Results Display:**
- clickable buttons for each matching project
- Results sorted by relevance score
- up to 8 top matches listed
- "No results found" message if no matches

#### 2. Results Tab

**Detailed Project View:**
- Opens automatically when a search result is clicked
- Displays extensive project details
- Displays calculated sustainability rating (1-10 scale with star display)

**Rating System:**
The app computes ratings based on:
- **Green Certifications** (highest weight):
  - Platinum/Outstanding/6-Star: 10 points
  - Gold/Excellent/5-Star: 8.5 points
  - Silver/Very Good/4-Star: 7 points
  - Bronze/Good/3-Star: 5.5 points
  - Certified/Pass: 4 points

- **Energy Efficiency**:
  - Excellent/A++/A+/90%+: 9 points
  - Good/A/B+/80%+: 7 points
  - Average/B/C+/70%+: 5 points
  - Basic implementation: 6 points

- **Sustainability Features**:
  - Advanced systems: 8 points
  - Standard implementation: 6 points
  - Basic features: 4 points

- **Location & Accessibility**:
  - Excellent location: 7 points
  - Good accessibility: 5 points
  - Average location: 3 points

#### 3. Settings Tab

**Theme Management:**
- Dropdown menu with available themes
- Built-in themes: Blue, Green, Dark-Blue
- Custom themes (if available in `themes/` folder)
- Theme changes require application restart

**Theme Files:**
Custom themes should be JSON files in `App_Data/themes/` following CustomTkinter's color theme format.

### Advanced Features

#### Search Algorithm Details

The search system uses a tiered scoring approach:

1. **Tier 1 (2000 points)**: Exact matches
2. **Tier 2 (1000+ points)**: All query words present
3. **Tier 3 (500+ points)**: Most query words present (2/3+)
4. **Tier 4 (50+ points)**: Individual word matches

#### Debug Mode

For troubleshooting search issues, the application includes debug output in the console showing:
- Normalized search terms
- Match scores per project
- Explanation of rankings

## Troubleshooting

### Issues

**"No results found" even with data:**
- Verify `ProjectName` column in Excel file
- Check project names don't contain too many special characters
- Use simpler search terms (single words)

**Application not starting:**
- Verify all required dependencies are installed
- Verify `App_Data/Database.xlsx` exists
- Check Python version (3.7+ required)

**Theme not working:**
- Verify theme file is correctly formatted JSON
- Restart app after theme selection
- Look at console for theme loading error

**Search results appear to be wrong:**
- Inspect debug output in console
- Ensure no spelling errors in search string
- Use different search terms

### Performance Enhancement

**For large databases:**
- Keep Excel file size below 10MB for optimal performance
- Delete blank rows and columns
- Employ consistent naming convention

**Memory usage:**
- Application loads entire database into memory
- Close application when idle for prolonged periods
- Periodic restart for big data

## Technical Details

### Architecture

- **Frontend**: CustomTkinter for contemporary GUI
- **Backend**: Pandas for data processing
- **Search Engine**: Custom algorithm with text normalization
- **Threading**: Asynchronous loading of data
- **Storage**: Excel files with pandas integration

### Data Flow

1. Application start loads Excel data into pandas DataFrame
2. Search index constructed with normalized text and partial matching
3. User queries processed using multi-tier search algorithm
4. Results ranked and displayed with clickable interface
5. High-level views computed using rating algorithm

### Customization

**Adding New Data Fields:**
1. Append columns to Excel file
2. Change rating calculation in `_calculate_project_rating()` method
3. Add new fields in display logic

**Modifying Search Behavior:**
- Change scoring weights in `get_top_matches()` function
- Alter text normalization in `_normalize_text()` method
- Change search tiers and point values

## Support

For bug issues or feature requests, try the following:

1. **Console Output**: Check for error messages and debug information
2. **File Permissions**: Provide read/write access to application directory
3. **Data Format**: Check that Excel file structure is according to requirements
4. **Dependencies**: Check all the packages required are installed

## Contributing

When changing the application:

1. Test with different database sizes and search terms
2. Test rating calculations with known building data
3. Test theme compatibility across multiple systems
4. Update documentation for new features

## License

This application is intended for academic and research use. Ensure building data is compliant with applicable privacy and usage policies.
