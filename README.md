# Sales Analytics Dashboard 📊💼

**Interactive HTML sales analytics dashboard with real-time data visualization**

## Features
- 📈 Interactive charts with Chart.js
- 📊 Real-time sales data updates
- 🗓️ Date range filtering
- 📱 Responsive design (mobile-friendly)
- 🔍 Product category analysis
- 📦 Sales by region/territory
- 💰 Revenue and profit tracking
- 📤 Export to PDF and Excel

## Tech Stack
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Charts**: Chart.js 4.0+
- **Data Processing**: Python 3.9+
- **Backend**: Flask (optional for live data)
- **Data Storage**: JSON/CSV or SQLite
- **Export**: jsPDF, ExcelJS

## Installation

### Option 1: Static HTML Version
```bash
# Clone repository
git clone https://github.com/blistartunivers-afk/sales-dashboard.git
cd sales-dashboard

# Open index.html in browser
# No server required for static version
```

### Option 2: Flask Live Version
```bash
# Install dependencies
pip install flask pandas numpy flask-cors

# Run Flask server
python app.py

# Open http://localhost:5000 in browser
```

## Quick Start

### Static Version
1. Edit `data/sales_data.json` with your data
2. Open `index.html` in any modern browser
3. Dashboard loads automatically

### Live Version
1. Update `app.py` with your data source
2. Run `python app.py`
3. Access dashboard at `http://localhost:5000`

## Project Structure
```
sales-dashboard/
├── index.html                # Main dashboard HTML
├── app.py                   # Flask backend (optional)
├── static/                  # Static assets
│   ├── css/                 # Stylesheets
│   │   ├── style.css         # Main styles
│   │   ├── charts.css        # Chart-specific styles
│   │   └── responsive.css    # Responsive design
│   ├── js/                  # JavaScript
│   │   ├── main.js           # Main application logic
│   │   ├── charts.js         # Chart configurations
│   │   ├── data.js           # Data processing
│   │   ├── filters.js        # Filter functionality
│   │   └── export.js         # Export functions
│   ├── lib/                 # Third-party libraries
│   │   ├── chart.js          # Chart.js library
│   │   ├── jspdf.min.js      # PDF export
│   │   └── exceljs.min.js   # Excel export
│   └── img/                 # Images and icons
├── data/                    # Sample data
│   ├── sales_data.json      # Main sales data
│   ├── products.json        # Product catalog
│   ├── regions.json         # Regional data
│   └── sample_data.csv      # CSV sample
├── templates/               # Flask templates
│   └── dashboard.html       # Flask template
├── requirements.txt         # Python dependencies
├── README.md                # This file
└── LICENSE                   # License file
```

## Data Format

### sales_data.json
```json
{
  "metadata": {
    "company": "Acme Corp",
    "period": "Q1 2023",
    "currency": "USD",
    "last_updated": "2023-03-31"
  },
  "sales": [
    {
      "id": "SAL-2023-001",
      "date": "2023-01-15",
      "product_id": "PROD-001",
      "product_name": "Premium Widget",
      "category": "Widgets",
      "quantity": 150,
      "unit_price": 29.99,
      "total": 4498.50,
      "cost": 2249.25,
      "profit": 2249.25,
      "region": "North",
      "salesperson": "John Doe",
      "payment_method": "Credit Card",
      "status": "Completed"
    },
    {
      "id": "SAL-2023-002",
      "date": "2023-01-18",
      "product_id": "PROD-002",
      "product_name": "Deluxe Gadget",
      "category": "Gadgets",
      "quantity": 75,
      "unit_price": 49.99,
      "total": 3749.25,
      "cost": 1874.63,
      "profit": 1874.62,
      "region": "South",
      "salesperson": "Jane Smith",
      "payment_method": "PayPal",
      "status": "Completed"
    }
  ],
  "summary": {
    "total_sales": 8247.75,
    "total_profit": 4123.87,
    "average_order": 4123.88,
    "top_product": "PROD-001",
    "top_category": "Widgets",
    "top_region": "North"
  }
}
```

## Dashboard Components

### 1. Summary Cards
- Total Sales
- Total Profit
- Average Order Value
- Conversion Rate
- Top Performing Product

### 2. Time Series Charts
- Daily Sales Trend (30 days)
- Monthly Sales Comparison
- Year-over-Year Growth

### 3. Category Analysis
- Sales by Product Category (Pie Chart)
- Top 10 Products (Bar Chart)
- Category Growth (Line Chart)

### 4. Regional Breakdown
- Sales by Region (Map Chart)
- Regional Performance (Bar Chart)
- Territory Comparison

### 5. Sales Team Performance
- Top Salespeople (Leaderboard)
- Individual Performance (Radar Chart)
- Target Achievement (%)

## Chart Configurations

### Sales Trend Chart
```javascript
const salesTrendChart = new Chart(ctx, {
    type: 'line',
    data: {
        labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
        datasets: [{
            label: 'Sales ($)',
            data: [12000, 19000, 15000, 22000, 18000, 25000],
            borderColor: '#4e73df',
            backgroundColor: 'rgba(78, 115, 223, 0.05)',
            tension: 0.3,
            fill: true
        }]
    },
    options: {
        responsive: true,
        plugins: {
            title: {
                display: true,
                text: 'Monthly Sales Trend'
            }
        },
        scales: {
            y: {
                beginAtZero: true,
                ticks: {
                    callback: function(value) {
                        return '$' + value.toLocaleString();
                    }
                }
            }
        }
    }
});
```

## Customization

### Color Scheme
Edit `static/css/style.css`:
```css
:root {
    --primary-color: #4e73df;
    --secondary-color: #1cc88a;
    --danger-color: #e74a3b;
    --warning-color: #f6c23e;
    --info-color: #36b9cc;
}
```

### Charts
Modify `static/js/charts.js`:
- Change chart types (line, bar, pie, doughnut)
- Adjust colors and styles
- Add/remove datasets

### Data Sources
Update `static/js/data.js`:
```javascript
// Load data from JSON
async function loadData() {
    const response = await fetch('data/sales_data.json');
    return await response.json();
}

// Or from API
async function loadData() {
    const response = await fetch('https://api.example.com/sales');
    return await response.json();
}
```

## Export Functionality

### PDF Export
```javascript
function exportToPDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    
    // Add title
    doc.text('Sales Dashboard Report', 105, 15, { align: 'center' });
    
    // Add charts as images
    const charts = document.querySelectorAll('.chart-container');
    charts.forEach((chart, index) => {
        // Capture chart and add to PDF
    });
    
    // Save PDF
    doc.save('sales-report.pdf');
}
```

### Excel Export
```javascript
function exportToExcel() {
    const workbook = new ExcelJS.Workbook();
    const worksheet = workbook.addWorksheet('Sales Data');
    
    // Add headers
    worksheet.columns = [
        { header: 'Date', key: 'date', width: 15 },
        { header: 'Product', key: 'product', width: 30 },
        { header: 'Sales', key: 'sales', width: 15 },
        { header: 'Profit', key: 'profit', width: 15 }
    ];
    
    // Add data
    salesData.forEach(sale => {
        worksheet.addRow({
            date: sale.date,
            product: sale.product_name,
            sales: sale.total,
            profit: sale.profit
        });
    });
    
    // Save file
    workbook.xlsx.writeBuffer().then(buffer => {
        saveAs(new Blob([buffer]), 'sales-data.xlsx');
    });
}
```

## Deployment

### Netlify/Vercel (Static)
1. Drag and drop `index.html` to Netlify
2. Or connect GitHub repository
3. Automatic deployment on push

### Heroku (Flask)
```bash
heroku create sales-dashboard-app
heroku config:set FLASK_APP=app.py
git push heroku main
heroku open
```

### Docker
```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]
```

Build and run:
```bash
docker build -t sales-dashboard .
docker run -p 5000:5000 sales-dashboard
```

## Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (responsive)

## Performance Optimization
- Lazy loading for charts
- Data pagination for large datasets
- Web workers for data processing
- Caching API responses

## Contributing

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Open Pull Request

## License

MIT License - See [LICENSE](LICENSE) for details.

## Contact

**blistartunivers-afk** - [GitHub Profile](https://github.com/blistartunivers-afk)

Project Link: [https://github.com/blistartunivers-afk/sales-dashboard](https://github.com/blistartunivers-afk/sales-dashboard)

---