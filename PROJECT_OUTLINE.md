# Embeddable Pricing Tables - Development Project Outline

## Project Overview

**Project Name:** E2 Embeddable Pricing Tables  
**Project Type:** Frontend Web Component Development  
**Framework:** Nuxt 4 + Vue 3 + TypeScript  
**Status:** Prototype Complete - Ready for Production Implementation

## Business Requirements

### Primary Objective

Create embeddable pricing tables that can be integrated into any website via iframe embedding, with dynamic customization through URL query parameters.

### Key Business Goals

- Enable third-party websites to embed E2 pricing tables seamlessly
- Provide flexible pricing display options based on course type and promotional campaigns
- Support affiliate tracking and conversion attribution
- Maintain brand consistency across all embedded instances
- Ensure mobile-responsive design for all embedding scenarios

## Technical Specification

### Architecture Overview

- **Frontend Framework:** Nuxt 4.1.2 with Vue 3 Composition API
- **Language:** TypeScript for type safety and developer experience
- **Styling:** Custom CSS utility system (Tailwind-like approach)
- **Build Tool:** Bun package manager and runtime
- **Deployment:** Static site generation with SSR capabilities

### Core Components

#### 1. PricingTable Component (`components/PricingTable.vue`)

**Purpose:** Main container orchestrating pricing display logic

**Key Features:**

- Query parameter processing and validation
- Discount code calculation (up to 30% off)
- Package filtering based on business rules
- Course-specific content rendering
- Affiliate tracking integration

**Props Interface:**

```typescript
interface QueryParams {
  course: CourseType;
  discountCode?: string;
  affiliateCode?: string;
  displayedPackages?: string[];
}
```

#### 2. PricingCard Component (`components/PricingCard.vue`)

**Purpose:** Individual package display with color theming

**Key Features:**

- 7 distinct color schemes for package differentiation
- Responsive card layout with feature lists
- Upgrade button with payment integration hooks
- Price display with discount calculations
- Feature highlighting and CTAs

**Color Schemes:**

- Orange (Bronze packages)
- Blue (Silver packages)
- Yellow (Gold packages)
- Purple (Express packages)
- Indigo (Express Plus)
- Green (Speaking Intensive)
- Pink (Writing Intensive)

### API Endpoints

#### 3. Embed Route (`pages/embed.vue`)

**Purpose:** Main embeddable endpoint for iframe integration

**Query Parameters:**

- `course` (required): Course type selection
- `discountCode` (optional): Promotional discount application
- `affiliateCode` (optional): Partner tracking identifier
- `displayedPackages` (optional): Package filtering

#### 4. Demo Route (`pages/index.vue`)

**Purpose:** Documentation and testing interface

**Features:**

- Live iframe preview
- Embedding code generation
- Parameter testing interface
- Usage documentation

## Functional Requirements

### Course Type Support

System must support all E2 course offerings:

1. IELTS Academic
2. IELTS General
3. PTE Academic
4. PTE Core
5. TOEFL
6. CELPIP LS
7. CELPIP (General)
8. OET Nurses
9. OET Doctors

### Package Types

System must display the following package options:

1. **Express** - 1 Month Access, Basic tutorials
2. **Express Plus** - 3 Month Access, Enhanced tutorials
3. **4-Week Intensive** - 4 Week Access, Speaking/Writing specialization
4. **Bronze** - 3 Month Access, Interactive learning
5. **Silver** - 6 Month Access, Teacher guidance
6. **Gold** - 12 Month Access, Premium features

### Discount Code System

- Automatic percentage calculation from code name
- Maximum 30% discount enforcement
- Support for promotional campaigns
- Integration with affiliate tracking

### Package Filtering

- Comma-separated package selection
- Dynamic visibility control
- Maintains responsive layout
- Preserves color theming

## Technical Requirements

### Performance

- **Load Time:** < 2 seconds initial render
- **Bundle Size:** < 500KB total JavaScript
- **Mobile Performance:** 90+ Lighthouse score
- **SEO Optimization:** Server-side rendering support

### Browser Compatibility

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile Safari iOS 14+
- Chrome Mobile Android 10+

### Responsive Design

- **Desktop:** 1200px+ (grid layout)
- **Tablet:** 768px-1199px (2-column grid)
- **Mobile:** < 768px (single column stack)
- **Iframe Constraints:** Minimum 300px width support

### Security & Integration

- **CSP Compatibility:** Works within Content Security Policy restrictions
- **CORS Configuration:** Proper cross-origin embedding support
- **XSS Prevention:** Input sanitization for all query parameters
- **Privacy Compliance:** No cookies or tracking without consent

## Implementation Tasks

### Phase 1: Core Development (Estimated: 5-8 days)

1. **Component Architecture** (2 days)

   - Create PricingTable and PricingCard components
   - Implement TypeScript interfaces and props validation
   - Set up Vue 3 composition API structure

2. **Query Parameter System** (2 days)

   - Implement route parameter parsing
   - Add validation for course types and package names
   - Create discount code calculation logic

3. **Responsive Design Implementation** (2-3 days)

   - Develop CSS utility system
   - Implement responsive grid layouts
   - Create color theming system for packages
   - Mobile optimization and testing

4. **Integration Points** (1 day)
   - Payment gateway preparation (Stripe/PayPal hooks)
   - Analytics tracking setup
   - Affiliate code handling

### Phase 2: Testing & Optimization (Estimated: 3-5 days)

1. **Cross-Browser Testing** (2 days)

   - Test iframe embedding across different browsers
   - Validate responsive behavior
   - Performance optimization

2. **Integration Testing** (2 days)

   - Test query parameter combinations
   - Validate discount calculations
   - Verify affiliate tracking
   - Package filtering functionality

3. **Performance Optimization** (1 day)
   - Bundle size optimization
   - Lazy loading implementation
   - SEO meta tag configuration

### Phase 3: Documentation & Deployment (Estimated: 2-3 days)

1. **Documentation** (1 day)

   - API documentation for embedding
   - Integration guide for partners
   - Troubleshooting guide

2. **Deployment Setup** (1-2 days)
   - Production build configuration
   - CDN setup for iframe embedding
   - Monitoring and analytics implementation

## Acceptance Criteria

### Functional Criteria

- [ ] All 9 course types display correctly with appropriate content
- [ ] Discount codes calculate percentages accurately (max 30%)
- [ ] Package filtering works with comma-separated values
- [ ] Affiliate codes are preserved and trackable
- [ ] Responsive design works on all target devices
- [ ] Iframe embedding functions across different websites

### Technical Criteria

- [ ] Bundle size under 500KB
- [ ] Load time under 2 seconds
- [ ] 90+ Lighthouse performance score on mobile
- [ ] Cross-browser compatibility verified
- [ ] No console errors in any supported browser
- [ ] CSP and CORS compatibility confirmed

### Business Criteria

- [ ] Brand consistency maintained across all variations
- [ ] Payment integration hooks ready for implementation
- [ ] Analytics tracking capabilities implemented
- [ ] Partner embedding documentation complete
- [ ] Mobile user experience optimized

## Risks & Mitigation

### Technical Risks

1. **Browser Compatibility Issues**
   - Mitigation: Comprehensive testing matrix, polyfill implementation
2. **Performance on Mobile**
   - Mitigation: Bundle optimization, lazy loading, performance monitoring
3. **Iframe Security Restrictions**
   - Mitigation: CSP testing, sandbox attribute configuration

### Business Risks

1. **Integration Complexity for Partners**
   - Mitigation: Comprehensive documentation, code examples, support process
2. **Discount Code Abuse**
   - Mitigation: Server-side validation, usage limits, expiration dates

## Success Metrics

### Performance Metrics

- Page load time < 2 seconds
- Mobile performance score > 90
- Zero critical accessibility issues
- Cross-browser compatibility 100%

### Business Metrics

- Partner adoption rate
- Conversion rate through embedded tables
- Mobile vs desktop engagement
- Affiliate attribution accuracy

## Dependencies

### External Dependencies

- Payment gateway integration (Stripe/PayPal)
- Analytics platform (Google Analytics/Mixpanel)
- CDN for static asset delivery
- Monitoring and error tracking (Sentry)

### Internal Dependencies

- Brand guidelines and color palette
- Current pricing structure and packages
- Affiliate tracking system
- Customer support documentation

## Timeline Estimate

**Total Development Time:** 10-16 days  
**Testing & QA:** 3-5 days  
**Documentation:** 2-3 days  
**Deployment & Launch:** 1-2 days

**Total Project Timeline:** 16-26 business days (3.5-5 weeks)

## React Implementation Alternative

### Overview

While the current prototype is built with Nuxt 4 + Vue 3, the embeddable pricing tables can also be implemented using React for teams preferring React ecosystem. This section outlines the React-specific implementation approach.

### React Architecture

#### Framework Options

1. **Next.js 14+ (Recommended)**

   - App Router with Server Components
   - Built-in optimization and SEO
   - Easy deployment with Vercel

2. **Create React App + TypeScript**

   - Simpler setup for smaller teams
   - Ejectable for custom configurations

3. **Vite + React**
   - Faster development experience
   - Modern build tooling
   - Smaller bundle sizes

### React Component Structure

#### 1. PricingTable Component (`components/PricingTable.tsx`)

```typescript
import React, { useMemo } from "react";
import { useSearchParams } from "react-router-dom";
import PricingCard from "./PricingCard";

interface Package {
  name: string;
  duration: string;
  originalPrice: number;
  colorScheme:
    | "orange"
    | "blue"
    | "yellow"
    | "purple"
    | "indigo"
    | "green"
    | "pink";
  features: string[];
}

interface PricingTableProps {
  course?: string;
  discountCode?: string;
  affiliateCode?: string;
  displayedPackages?: string[];
}

const PricingTable: React.FC<PricingTableProps> = ({
  course,
  discountCode,
  affiliateCode,
  displayedPackages,
}) => {
  const packages = useMemo(() => {
    // Package generation logic similar to Vue implementation
    return generatePackagesForCourse(course);
  }, [course]);

  const discountPercentage = useMemo(() => {
    return calculateDiscount(discountCode);
  }, [discountCode]);

  const filteredPackages = useMemo(() => {
    if (!displayedPackages?.length) return packages;
    return packages.filter((pkg) => displayedPackages.includes(pkg.name));
  }, [packages, displayedPackages]);

  const handleUpgrade = (packageName: string, price: number) => {
    // Payment integration logic
    console.log("Upgrade clicked", { packageName, price, affiliateCode });
  };

  return (
    <div className="pricing-table">
      <div className="container">
        <h1 className="heading">{course} Pricing Plans</h1>
        {discountCode && (
          <div className="discount-banner">
            Save {discountPercentage}% with code {discountCode}
          </div>
        )}
        <div className="grid">
          {filteredPackages.map((pkg) => (
            <PricingCard
              key={pkg.name}
              package={pkg}
              discountPercentage={discountPercentage}
              onUpgrade={handleUpgrade}
            />
          ))}
        </div>
      </div>
    </div>
  );
};

export default PricingTable;
```

#### 2. PricingCard Component (`components/PricingCard.tsx`)

```typescript
import React from "react";

interface PricingCardProps {
  package: Package;
  discountPercentage: number;
  onUpgrade: (name: string, price: number) => void;
}

const PricingCard: React.FC<PricingCardProps> = ({
  package: pkg,
  discountPercentage,
  onUpgrade,
}) => {
  const discountedPrice = Math.round(
    pkg.originalPrice * (1 - discountPercentage / 100)
  );
  const savings = pkg.originalPrice - discountedPrice;

  return (
    <div className={`pricing-card pricing-card-${pkg.colorScheme}`}>
      <div className="card-header">
        <h3 className="package-name">{pkg.name}</h3>
        <p className="duration">{pkg.duration}</p>
      </div>

      <div className="pricing">
        {discountPercentage > 0 && (
          <p className="original-price">${pkg.originalPrice}</p>
        )}
        <p className="current-price">${discountedPrice}</p>
        {savings > 0 && <p className="savings">Save ${savings}</p>}
      </div>

      <ul className="features">
        {pkg.features.map((feature, index) => (
          <li key={index} className="feature-item">
            <span className="checkmark">✓</span>
            {feature}
          </li>
        ))}
      </ul>

      <button
        className="upgrade-button"
        onClick={() => onUpgrade(pkg.name, discountedPrice)}
      >
        Upgrade Now
      </button>
    </div>
  );
};

export default PricingCard;
```

### React Routing Implementation

#### Next.js App Router Structure

```
app/
├── embed/
│   └── page.tsx          # Main embed route
├── page.tsx              # Demo/documentation page
├── components/
│   ├── PricingTable.tsx
│   └── PricingCard.tsx
└── globals.css           # Global styles
```

#### Embed Route (`app/embed/page.tsx`)

```typescript
"use client";

import React, { Suspense } from "react";
import { useSearchParams } from "next/navigation";
import PricingTable from "@/components/PricingTable";

function EmbedContent() {
  const searchParams = useSearchParams();

  const course = searchParams.get("course");
  const discountCode = searchParams.get("discountCode");
  const affiliateCode = searchParams.get("affiliateCode");
  const displayedPackages = searchParams.get("displayedPackages")?.split(",");

  if (!course) {
    return <div>Error: Course parameter is required</div>;
  }

  return (
    <PricingTable
      course={course}
      discountCode={discountCode || undefined}
      affiliateCode={affiliateCode || undefined}
      displayedPackages={displayedPackages}
    />
  );
}

export default function EmbedPage() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <EmbedContent />
    </Suspense>
  );
}
```

### State Management Options

#### 1. React Context (Simple State)

```typescript
interface PricingContextType {
  course: string | null;
  discountCode: string | null;
  affiliateCode: string | null;
  packages: Package[];
}

const PricingContext = React.createContext<PricingContextType | undefined>(
  undefined
);

export const PricingProvider: React.FC<{ children: React.ReactNode }> = ({
  children,
}) => {
  // Context implementation
};
```

#### 2. Zustand (Recommended for Complex State)

```typescript
import { create } from "zustand";

interface PricingStore {
  course: string | null;
  discountCode: string | null;
  affiliateCode: string | null;
  packages: Package[];
  setCourse: (course: string) => void;
  setDiscountCode: (code: string) => void;
  // Other actions
}

export const usePricingStore = create<PricingStore>((set) => ({
  course: null,
  discountCode: null,
  affiliateCode: null,
  packages: [],
  setCourse: (course) => set({ course }),
  setDiscountCode: (discountCode) => set({ discountCode }),
}));
```

### Styling Solutions

#### 1. Tailwind CSS (Recommended)

```bash
npm install tailwindcss @tailwindcss/typography
npx tailwindcss init -p
```

#### 2. Styled Components

```typescript
import styled from "styled-components";

const PricingGrid = styled.div`
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  padding: 2rem;

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
`;
```

#### 3. CSS Modules

```typescript
import styles from "./PricingTable.module.css";

const PricingTable = () => (
  <div className={styles.pricingTable}>{/* Component content */}</div>
);
```

### React-Specific Implementation Timeline

#### Phase 1: React Setup & Core Components (6-10 days)

1. **Project Setup** (1-2 days)

   - Next.js/CRA setup with TypeScript
   - ESLint, Prettier configuration
   - Styling solution implementation

2. **Component Development** (3-4 days)

   - PricingTable and PricingCard components
   - TypeScript interfaces and prop types
   - React hooks for state management

3. **Routing & Query Parameters** (2-3 days)

   - Next.js App Router or React Router setup
   - Query parameter parsing with useSearchParams
   - URL state management

4. **Responsive Design** (1 day)
   - CSS Grid/Flexbox implementation
   - Mobile-first responsive design
   - Cross-browser testing

#### Phase 2: React-Specific Features (3-4 days)

1. **State Management** (1-2 days)

   - Context API or Zustand implementation
   - Global state for pricing data
   - Persistent state handling

2. **Performance Optimization** (1-2 days)
   - React.memo for component optimization
   - useMemo and useCallback for expensive operations
   - Lazy loading and code splitting

### React Dependencies

#### Core Dependencies

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "next": "^14.0.0",
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "typescript": "^5.0.0"
  },
  "devDependencies": {
    "eslint": "^8.0.0",
    "eslint-config-next": "^14.0.0",
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "prettier": "^3.0.0"
  }
}
```

#### Optional Dependencies

```json
{
  "optionalDependencies": {
    "tailwindcss": "^3.4.0",
    "zustand": "^4.4.0",
    "framer-motion": "^10.16.0",
    "react-query": "^3.39.0"
  }
}
```

### React Testing Strategy

#### Unit Testing with Jest & React Testing Library

```typescript
import { render, screen, fireEvent } from "@testing-library/react";
import PricingCard from "../PricingCard";

describe("PricingCard", () => {
  const mockPackage = {
    name: "Bronze",
    duration: "3 months",
    originalPrice: 299,
    colorScheme: "orange" as const,
    features: ["Feature 1", "Feature 2"],
  };

  test("displays package information correctly", () => {
    render(
      <PricingCard
        package={mockPackage}
        discountPercentage={0}
        onUpgrade={jest.fn()}
      />
    );

    expect(screen.getByText("Bronze")).toBeInTheDocument();
    expect(screen.getByText("$299")).toBeInTheDocument();
  });

  test("handles upgrade button click", () => {
    const mockOnUpgrade = jest.fn();
    render(
      <PricingCard
        package={mockPackage}
        discountPercentage={0}
        onUpgrade={mockOnUpgrade}
      />
    );

    fireEvent.click(screen.getByText("Upgrade Now"));
    expect(mockOnUpgrade).toHaveBeenCalledWith("Bronze", 299);
  });
});
```

### React Deployment Options

#### 1. Vercel (Next.js Recommended)

```bash
npm install -g vercel
vercel --prod
```

#### 2. Netlify

```bash
npm run build
netlify deploy --prod --dir=build
```

#### 3. AWS Amplify

- GitHub integration
- Automatic deployments
- Built-in CDN

### React vs Vue Comparison

| Aspect              | Vue 3 (Current)           | React Alternative            |
| ------------------- | ------------------------- | ---------------------------- |
| **Learning Curve**  | Gentle, template-based    | Steeper, JSX-based           |
| **Performance**     | Excellent with reactivity | Excellent with optimizations |
| **Ecosystem**       | Smaller but mature        | Large and comprehensive      |
| **TypeScript**      | Great integration         | Excellent native support     |
| **Bundle Size**     | Smaller base              | Larger but optimizable       |
| **Developer Tools** | Vue DevTools              | React DevTools               |
| **Team Preference** | Vue specialists           | React specialists            |

### Migration Strategy (Vue to React)

If migrating from the current Vue prototype:

1. **Direct Translation** (Recommended)

   - Convert Vue components to React functional components
   - Replace Vue Composition API with React hooks
   - Maintain same prop interfaces and logic

2. **Gradual Migration**

   - Use Vue components in React via vue-in-react wrapper
   - Migrate components incrementally
   - Maintain parallel codebases temporarily

3. **Complete Rewrite**
   - Start fresh with React best practices
   - Opportunity to improve architecture
   - Longer timeline but cleaner result

## Post-Launch Considerations

### Maintenance

- Regular browser compatibility testing
- Performance monitoring and optimization
- Security updates and vulnerability patches
- Feature enhancements based on partner feedback

### Analytics & Monitoring

- Conversion tracking through embedded tables
- Performance monitoring across different embedding contexts
- Error tracking and user experience analytics
- A/B testing capabilities for pricing strategies

---

**Document Version:** 1.0  
**Last Updated:** October 2, 2025  
**Author:** Development Team  
**Review Status:** Ready for Implementation
