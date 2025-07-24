# Green Building Evaluator

A comprehensive desktop application for searching and evaluating green building projects. This tool provides an intuitive interface to explore building sustainability data, certifications, and environmental performance metrics.

## Features

- **Advanced Search**: Intelligent search algorithm with fuzzy matching and multi-word support
- **Project Rating System**: Automated calculation of building sustainability ratings (1-10 scale)
- **Interactive Interface**: Clean, modern GUI with tabbed navigation
- **Customizable Themes**: Multiple color themes with easy switching
- **Detailed Project Information**: Comprehensive view of building certifications, energy efficiency, and sustainability features
- **Real-time Search Results**: Instant feedback with clickable project listings

## Installation

### Prerequisites

Before running the application, ensure you have Python 3.7+ installed on your system.

### Required Dependencies

Install the required Python packages using pip:

```bash
pip install customtkinter pandas openpyxl
```

**Package Details:**
- `customtkinter`: Modern GUI framework for the user interface
- `pandas`: Data manipulation and analysis library
- `openpyxl`: Excel file reading and writing support

### File Structure

Ensure your project directory is organized as follows:

```
Green-Building-Evaluator/
├── main.py                          # Main application entry point
├── App_Data/
│   ├── GetData.py                   # Data management and search logic
│   ├── widgets.py                   # Main tab interface components
│   ├── setting_frame.py             # Settings panel implementation
│   ├── Database.xlsx                # Building data spreadsheet
│   └── themes/                      # Custom theme files (optional)
│       ├── custom_theme1.json
│       └── custom_theme2.json
├── settings.txt                     # Theme preference storage
└── README.md                        # This file
```

## Database Setup

### Excel File Requirements

The application expects a file named `Database.xlsx` in the `App_Data/` directory. This Excel file should contain building project data with the following structure:

**Required Column:**
- `ProjectName`: The name of the building/project (must be present)

**Optional Columns (for enhanced functionality):**
- `LEED_Rating`: LEED certification level
- `BREEAM_Rating`: BREEAM certification level
- `Green_Star_Rating`: Green Star certification level
- `Certification`: General certification information
- `Energy_Rating`: Energy efficiency rating
- `Energy_Efficiency`: Energy performance metrics
- `Solar_Panels`: Solar installation details
- `Renewable_Energy`: Renewable energy usage
- `Water_Efficiency`: Water conservation measures
- `Waste_Management`: Waste reduction strategies
- `Green_Roof`: Green roof implementation
- `Rain_Water_Harvesting`: Rainwater collection systems
- `Location_Rating`: Location sustainability rating
- `Transport_Access`: Transportation accessibility
- `Public_Transport`: Public transit connectivity

### Sample Data Format

| ProjectName | LEED_Rating | Energy_Rating | Water_Efficiency | Location_Rating |
|-------------|-------------|---------------|------------------|-----------------|
| Empire State Building | Gold | A+ | Excellent | A |
| One World Trade Center | Platinum | A++ | Good | A |
| The Edge Amsterdam | Outstanding | 100% Renewable | Excellent | A |

## Usage Guide

### Starting the Application

1. **Launch the application:**
   ```bash
   python main.py
   ```

2. **Loading Screen:**
   - The app will display a loading screen while processing the database
   - Progress indicators show:
     - Reading Database
     - Processing project data
     - Optimizing search index
     - Finalizing

3. **Error Handling:**
   - If database loading fails, a retry button will appear
   - Check that `App_Data/Database.xlsx` exists and is properly formatted

### Main Interface

The application features a three-tab interface:

#### 1. Search Tab

**Search Functionality:**
- Enter building or project names in the search field
- Press Enter or click "Search" to execute
- Search supports:
  - Exact matches (highest priority)
  - Partial matches (all words present)
  - Fuzzy matching (some words present)
  - Individual word matching

**Search Examples:**
- `"Empire State Building"` - finds exact matches
- `"Empire State"` - finds buildings containing both words
- `"Building"` - finds all projects with "building" in the name
- `"LEED Gold"` - finds projects with LEED Gold certification

**Results Display:**
- Clickable buttons for each matching project
- Results ranked by relevance score
- Up to 8 top matches displayed
- "No results found" message if no matches

#### 2. Results Tab

**Detailed Project View:**
- Automatically opens when clicking a search result
- Displays comprehensive project information
- Shows calculated sustainability rating (1-10 scale with star display)

**Rating System:**
The application calculates ratings based on:
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
- Custom themes (if present in `themes/` folder)
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
- Normalized search queries
- Match scores for each project
- Ranking explanations

## Troubleshooting

### Common Issues

**"No results found" despite having data:**
- Check that `ProjectName` column exists in Excel file
- Verify project names don't have excessive special characters
- Try simpler search terms (single words)

**Application won't start:**
- Ensure all dependencies are installed
- Check that `App_Data/Database.xlsx` exists
- Verify Python version (3.7+ required)

**Theme not applying:**
- Ensure theme file is properly formatted JSON
- Restart application after theme selection
- Check console for theme loading errors

**Search results seem incorrect:**
- Review debug output in console
- Check for typos in search terms
- Try alternative search phrases

### Performance Optimization

**For large databases:**
- Keep Excel file under 10MB for optimal performance
- Remove empty rows and columns
- Use consistent naming conventions

**Memory usage:**
- The application loads entire database into memory
- Close application when not in use for extended periods
- Restart periodically for large datasets

## Technical Details

### Architecture

- **Frontend**: CustomTkinter for modern GUI
- **Backend**: Pandas for data manipulation
- **Search Engine**: Custom implementation with text normalization
- **Threading**: Asynchronous data loading
- **Storage**: Excel files with pandas integration

### Data Flow

1. Application startup loads Excel data into pandas DataFrame
2. Search index built with normalized text and partial matching
3. User queries processed through multi-tier search algorithm
4. Results ranked and displayed with clickable interface
5. Detailed views calculated with rating algorithm

### Customization

**Adding New Data Fields:**
1. Add columns to Excel file
2. Update rating calculation in `_calculate_project_rating()` method
3. Include new fields in display logic

**Modifying Search Behavior:**
- Adjust scoring weights in `get_top_matches()` function
- Modify text normalization in `_normalize_text()` method
- Update search tiers and point values

## Support

For technical issues or feature requests, check the following:

1. **Console Output**: Look for error messages and debug information
2. **File Permissions**: Ensure read/write access to application directory
3. **Data Format**: Verify Excel file structure matches requirements
4. **Dependencies**: Confirm all required packages are installed

## Contributing

When modifying the application:

1. Test with various database sizes and search terms
2. Validate rating calculations with known building data
3. Ensure theme compatibility across different systems
4. Update documentation for new features

## License

This application is designed for educational and research purposes. Ensure building data complies with relevant privacy and usage policies.
