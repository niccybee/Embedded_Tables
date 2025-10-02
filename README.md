# E2 Embeddable Pricing Tables

This Nuxt 4 project creates embeddable pricing tables that can be customized through query parameters and embedded in any website using iframes.

## Features

- **Embeddable Design**: Can be embedded in any website using iframes
- **Query Parameter Customization**: Customize the display using URL parameters
- **Responsive Layout**: Works on desktop and mobile devices
- **Multiple Course Types**: Support for various test preparation courses
- **Dynamic Pricing**: Discount codes with configurable percentages
- **Package Filtering**: Show only specific packages based on requirements

## Query Parameters

### Course (required)
- `course`: The type of course/test preparation
- Valid values: `IELTS Academic`, `IELTS General`, `PTE Academic`, `PTE Core`, `TOEFL`, `CELPIP LS`, `CELPIP`, `OET Nurses`, `OET Doctors`

### Discount Code (optional)
- `discountCode`: Apply a discount code (examples: `INVEST25`, `SAVE20`, `STUDENT15`, `EARLY30`)
- Automatically calculates percentage discount (max 30%)

### Affiliate Code (optional)
- `affiliateCode`: Affiliate tracking ID for conversion tracking

### Displayed Packages (optional)
- `displayedPackages`: Comma-separated list of packages to display
- Valid packages: `Express`, `Express Plus`, `4-Week Intensive`, `Bronze`, `Silver`, `Gold`

## Usage Examples

### Basic Embedding
```html
<iframe 
  src="https://your-domain.com/embed?course=IELTS General"
  width="100%" 
  height="800"
  frameborder="0"
  title="E2 Pricing Table"
></iframe>
```

### With Discount Code
```html
<iframe 
  src="https://your-domain.com/embed?course=IELTS Academic&discountCode=INVEST25&affiliateCode=ABC123"
  width="100%" 
  height="800"
  frameborder="0"
  title="E2 Pricing Table"
></iframe>
```

### Filtered Packages
```html
<iframe 
  src="https://your-domain.com/embed?course=PTE Academic&displayedPackages=Bronze,Silver,Gold"
  width="100%" 
  height="800"
  frameborder="0"
  title="E2 Pricing Table"
></iframe>
```

## Available Packages

- **Express**: 1 Month Access - Basic tutorial package
- **Express Plus**: 3 Month Access - Enhanced tutorial package  
- **4-Week Intensive**: 4 Week Access - Specialized intensive courses
- **Bronze**: 3 Month Access - Interactive learning with feedback
- **Silver**: 6 Month Access - Committed learning with teacher guidance
- **Gold**: 12 Month Access - Premium package for high achievers

## Development

### Setup
```bash
# Install dependencies
bun install

# Start development server
bun dev
```

### Build for Production
```bash
# Build the application
bun build

# Preview production build
bun preview
```

## Demo

Visit the homepage at `http://localhost:3000` to see live examples and embedding code.
Visit the embed page at `http://localhost:3000/embed?course=IELTS Academic` to see the embeddable table directly.
