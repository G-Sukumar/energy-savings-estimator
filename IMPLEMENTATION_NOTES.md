# Energy Savings Estimator - Implementation Notes

## Overview
A professional web application for calculating energy savings when replacing standard motors with energy-efficient motors in centrifugal fan applications, based on Affinity Law principles.

## Features Implemented

### ✅ Core Functionality
- **Scientific Estimation Method**: Uses Affinity Law (power ∝ speed³) for accurate predictions
- **Instant Calculations**: Real-time JavaScript calculations without backend
- **Form Validation**: Prevents submission with invalid/incomplete data
- **Professional UI**: Industrial blue/white/grey theme with responsive design

### ✅ Input Sections

#### Technical Inputs
1. **Standard Motor (Old)**
   - Synchronous Speed (Ns) - rpm
   - Operating Speed (N1) - rpm
   - Efficiency at Operating Point (η1) - %
   - Energy Consumption per hour (E1) - kWh

2. **Energy Efficient Motor (New)**
   - Efficiency (η2) - %
   - Estimated New Operating Speed (N2) - rpm

#### Financial Inputs
- Electricity Cost (₹ per kWh)
- Motor Replacement Cost (₹)
- Scrap Value of Old Motor (₹)
- Operating Hours per Year

### ✅ Calculation Logic

**Step 1: Energy Savings %**
```
Energy Savings (%) = ((η2 × N1³) − (η1 × N2³)) / (η2 × N1³) × 100
```

**Step 2: New Energy Consumption**
```
E2 = E1 × (1 − (Energy Savings % / 100))
```

**Step 3: Annual Energy Savings**
```
Annual Energy Savings (kWh) = (E1 − E2) × Operating Hours per Year
```

**Step 4: Annual Cost Savings**
```
Annual Cost Savings = Annual Energy Savings × Electricity Cost
```

**Step 5: Payback Period**
```
Payback Period (Years) = (Motor Cost − Scrap Value) ÷ Annual Cost Savings
```
If Annual Cost Savings ≤ 0, displays "Not Achievable"

### ✅ Output Dashboard

#### Technical Analysis Card
- Large percentage display with color coding
- Old vs New motor energy comparison
- Status indicator (Increases/Decreases)
- Bar chart comparison

#### Financial Analysis Card
- Annual energy savings (kWh)
- Annual cost savings (₹)
- Payback period (years)

#### Decision Box (Color Coded)
- 🟢 **Green**: Recommended (Savings > 0 AND Payback < 3 years)
- 🔴 **Red**: Not Recommended (otherwise)
- Large, prominent display with explanation

### ✅ Visual Features
- **Bar Chart**: Recharts-based comparison of old vs new motor energy
- **Color Coding**: 
  - Green = Positive savings
  - Red = Negative savings/not viable
  - Blue = Neutral/informational
- **Responsive Design**: Mobile-friendly layout
- **Industrial Theme**: Professional engineering dashboard aesthetic

### ✅ Extra Features
1. **Reset Button**: Clears all inputs and results
2. **Download PDF**: Generates comprehensive report using jsPDF
3. **Affinity Law Tooltip**: Info icon in header explains the principle
4. **Formula Display**: Toggle to show/hide calculation formulas
5. **Instant Updates**: Calculations trigger on button click

## Technical Stack
- **React 18** with TypeScript
- **Tailwind CSS v4** for styling
- **Recharts** for data visualization
- **jsPDF** for PDF generation
- **Lucide React** for icons
- **Radix UI** components for accessibility

## File Structure
```
/src/app/
├── App.tsx                          # Main application component
├── types.ts                         # TypeScript interfaces
├── components/
│   ├── InputForm.tsx               # User input form with validation
│   ├── ResultsDashboard.tsx        # Results display with cards
│   ├── EnergyComparisonChart.tsx   # Bar chart component
│   └── FormulaDisplay.tsx          # Formula explanation component
└── utils/
    ├── calculations.ts             # Core calculation logic
    └── pdfGenerator.ts             # PDF report generation
```

## Key Design Decisions

### 1. State Management
- Used React hooks (useState) for simplicity
- Separate state for motor inputs, financial inputs, and results
- Formula display toggle state

### 2. Validation
- Client-side validation in InputForm component
- Disabled calculate button until all required fields are filled
- No negative values accepted

### 3. User Experience
- Clear visual feedback with color coding
- Informative placeholder values in inputs
- Unit labels on all input fields
- Comprehensive explanations in decision box
- Professional industrial aesthetic

### 4. Calculations
- All calculations performed client-side
- Efficiency converted from percentage to decimal
- Speed cubed for Affinity Law application
- Handles edge cases (negative savings, zero cost savings)

### 5. Responsive Design
- Desktop: Two-column layout (inputs | results)
- Mobile: Stacked single-column layout
- Grid system for input fields
- Flexible card layouts

## Usage Example

**Sample Input:**
- Old Motor: 3000 rpm (Ns), 2880 rpm (N1), 85% efficiency, 10 kWh/hr
- New Motor: 92% efficiency, 2900 rpm (N2)
- Electricity: ₹8.5/kWh, 8760 hours/year
- Cost: ₹50,000, Scrap: ₹5,000

**Expected Output:**
- Energy savings calculation based on formula
- Visual comparison chart
- Financial analysis with payback period
- Recommendation based on criteria

## Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Responsive on mobile devices
- No Internet Explorer support required

## Notes
- No backend or database required
- All data processing happens in browser
- PDF generation works offline
- No external API calls
