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
