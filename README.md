```markdown
# FedPipe - Federal Sales Pipeline Visualizer

A standalone, self-contained HTML application for federal sales account managers to visualize, analyze and report on their sales pipeline data.

![FedPipe Dashboard](https://github.com/flourcode/fedpipe/raw/main/screenshot.png)

## Overview

FedPipe is a lightweight, browser-based tool designed specifically for government sales professionals. It enables account managers to:

- Import their pipeline data from CSV or Excel files
- Generate interactive visualizations and analytics
- Export presentation-ready charts and reports
- Identify key trends and opportunities in federal sales data

The entire application runs in your web browser with no server requirements, ensuring your sensitive pipeline data never leaves your computer.

## Getting Started

### Option 1: Direct Download and Use
1. **Download**: Get the HTML file from the [Releases](https://github.com/flourcode/fedpipe/releases) section
2. **Open**: Double-click the file to open it in any modern web browser
3. **Import Data**: Either use the sample data or upload your own CSV/Excel file

### Option 2: Clone the Repository
```bash
git clone https://github.com/flourcode/fedpipe.git
cd fedpipe
```
Then open `fedpipe.html` in your browser.

## Features

- **Offline-First**: All processing happens in your browser - no data ever leaves your computer
- **Multi-format Support**: Upload data from CSV or Excel (XLSX/XLS) files
- **Interactive Dashboard**: View key metrics including active opportunities, pipeline value, win rates, and days to close
- **Visualization Suite**: Multiple chart types to analyze your pipeline from different angles
- **Executive Reports**: Generate presentation-ready summaries for QBRs and MBRs
- **Mobile Optimized**: Works seamlessly on tablets and smartphones
- **Export Capabilities**: Download charts and reports as images for presentations

## Data Format

Your CSV or Excel file should include the following columns:

| Column Name | Description | Example |
|-------------|-------------|---------|
| OpportunityName | Name of the opportunity | "Cloud Migration Services" |
| Agency | Federal agency name | "DoD", "DHS", etc. |
| Stage | Current pipeline stage | "Identify", "Qualify", "Propose", "Negotiate", "Closed Won", "Closed Lost" |
| Value | Estimated value in dollars | 750000 |
| CloseDate | Expected close date (YYYY-MM-DD) | 2025-07-15 |
| Probability | Win probability percentage (0-100) | 40 |

## Calculations and Methodology

### Key Metrics

#### Active Opportunities
The count of all opportunities that are not in "Closed Won" or "Closed Lost" stages.

#### Pipeline Value
The sum of the estimated value for all active opportunities.

#### Win Rate
Historical win rate calculated as the percentage of closed opportunities that were won:

```javascript
const closedOpps = pipelineData.filter(item => item.Stage.includes('Closed'));
const wonOpps = pipelineData.filter(item => item.Stage === 'Closed Won');
const winRate = closedOpps.length > 0 ? (wonOpps.length / closedOpps.length) * 100 : 0;
```

#### Average Days to Close
For active opportunities, this represents the average number of days until their expected close dates:

```javascript
const today = new Date();
const avgDaysToClose = activeOpps.length > 0 ? 
    activeOpps.reduce((sum, item) => {
        const closeDate = new Date(item.CloseDate);
        const daysDiff = Math.ceil((closeDate - today) / (1000 * 60 * 60 * 24));
        return sum + (daysDiff > 0 ? daysDiff : 0);
    }, 0) / activeOpps.length : 0;
```

This calculation:
1. Takes each active opportunity's close date
2. Calculates the number of days between today and that close date
3. Averages these values across all active opportunities

### Chart Visualizations

#### Pipeline by Stage
Shows the total pipeline value broken down by stage, with values converted to millions for readability. This helps identify which stages have the most value concentration.

#### Pipeline by Agency
Visualizes your pipeline distribution across different federal agencies, showing where your largest opportunities are concentrated.

#### Opportunity Trend
Projects pipeline value over the next 6 months based on opportunity close dates, helping forecast future business.

#### Win Rate Analysis
Displays two data points:
1. The average probability percentage for opportunities in each stage
2. A horizontal line showing the historical win rate based on closed opportunities

This helps identify gaps between forecasted probabilities and actual performance.

#### Agency Breakdown
A stacked bar chart showing pipeline value by agency and stage, helping identify which agencies have the most mature opportunities.

## Privacy & Security

FedPipe is designed with privacy in mind:
- All data processing happens in your browser
- No data is ever sent to any server
- No analytics or tracking code is included
- Works offline once the page is loaded

## Browser Compatibility

FedPipe works in all modern browsers including:
- Chrome
- Firefox
- Safari
- Edge

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Known Issues

- When loading sample data, charts may sometimes continue expanding down the screen. This is fixed by setting fixed heights for chart containers.
- Some mobile browsers may have rendering issues with certain chart types.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Chart.js for visualization capabilities
- SheetJS for Excel file support
- html2canvas for report exports
- FontAwesome for icons

---

Created by [flourcode](https://github.com/flourcode)
```

