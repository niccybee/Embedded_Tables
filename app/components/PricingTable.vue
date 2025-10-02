<template>
  <div class="pricing-container">
    <!-- Header Section -->
    <div class="text-center mb-8">
      <div class="promo-banner">
        Promo code {{ discountCode || 'INVEST25' }} has been applied! Get {{ discountPercent }}% off selected packages!
      </div>
      
      <h1 class="main-title">
        Choose Your Package - {{ course }}
      </h1>
      
      <button class="cta-button">
        CHOOSE THE BEST PACKAGE FOR YOU
      </button>
      
      <p class="upgrade-info">
        What happens when I upgrade my package?
      </p>
    </div>

    <!-- Pricing Cards Grid -->
    <div class="pricing-grid">
      <!-- Bronze Package -->
      <PricingCard
        v-if="shouldShowPackage('Bronze')"
        title="Bronze"
        subtitle="3 Months Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You thrive on interactive learning and personalised feedback from a teacher."
        :originalPrice="174.99"
        :discountedPrice="calculatePrice(131.18)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="orange"
        :features="bronzeFeatures"
      />

      <!-- Silver Package -->
      <PricingCard
        v-if="shouldShowPackage('Silver')"
        title="Silver"
        subtitle="6 Months Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You're a committed learner who requires teacher guidance to achieve your goals."
        :originalPrice="262.99"
        :discountedPrice="calculatePrice(197.18)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="blue"
        :features="silverFeatures"
      />

      <!-- Gold Package -->
      <PricingCard
        v-if="shouldShowPackage('Gold')"
        title="Gold"
        subtitle="12 Months Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You're a high achiever and want the confidence to get a top score!"
        :originalPrice="372.99"
        :discountedPrice="calculatePrice(279.68)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="yellow"
        :features="goldFeatures"
        :isPopular="true"
      />

      <!-- Express Package -->
      <PricingCard
        v-if="shouldShowPackage('Express')"
        title="Express"
        subtitle="1 Month Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You're a motivated self-learner"
        :originalPrice="64.99"
        :discountedPrice="calculatePrice(48.68)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="purple"
        :features="expressFeatures"
      />

      <!-- Express Plus Package -->
      <PricingCard
        v-if="shouldShowPackage('Express Plus')"
        title="Express+"
        subtitle="3 Month Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You're confident with your skills and want to practice with a mock test."
        :originalPrice="86.99"
        :discountedPrice="calculatePrice(65.18)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="indigo"
        :features="expressPlusFeatures"
      />

      <!-- Speaking Intensive Package -->
      <PricingCard
        v-if="shouldShowPackage('4-Week Intensive')"
        title="Speaking Intensive"
        subtitle="4 Week Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You're seeking detailed feedback on how to improve your speaking."
        :originalPrice="97.99"
        :discountedPrice="calculatePrice(73.43)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="green"
        :features="speakingIntensiveFeatures"
      />

      <!-- Writing Intensive Package -->
      <PricingCard
        v-if="shouldShowPackage('Writing Intensive')"
        title="Writing Intensive"
        subtitle="4 Week Access from Date of Upgrade"
        description="Plus your account at any time"
        studentText="You're seeking detailed feedback on how to improve your writing."
        :originalPrice="97.99"
        :discountedPrice="calculatePrice(73.43)"
        :discountPercent="discountPercent"
        :affiliateCode="affiliateCode"
        color="pink"
        :features="writingIntensiveFeatures"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  course?: string
  discountCode?: string
  affiliateCode?: string
  displayedPackages?: string
}

const props = withDefaults(defineProps<Props>(), {
  course: 'IELTS General',
  discountCode: '',
  affiliateCode: '',
  displayedPackages: ''
})

// Calculate discount percentage from discount code
const discountPercent = computed(() => {
  if (!props.discountCode) return 25 // Default 25% as shown in image
  
  // You can implement your own logic for different discount codes
  const discountMap: Record<string, number> = {
    'INVEST25': 25,
    'SAVE20': 20,
    'STUDENT15': 15,
    'EARLY30': 30
  }
  
  return discountMap[props.discountCode] || 25
})

// Calculate discounted price
const calculatePrice = (basePrice: number) => {
  const discount = discountPercent.value / 100
  return (basePrice * (1 - discount)).toFixed(2)
}

// Parse displayed packages
const displayedPackagesArray = computed(() => {
  if (!props.displayedPackages) return []
  return props.displayedPackages.split(',').map(pkg => pkg.trim())
})

// Check if package should be shown
const shouldShowPackage = (packageName: string) => {
  if (displayedPackagesArray.value.length === 0) return true
  return displayedPackagesArray.value.includes(packageName)
}

// Package features
const bronzeFeatures = [
  'Expert Teacher Tutorials',
  'Assessment with Expert Feedback',
  'Mock Test',
  'Writing Task 1',
  'Writing Task 2',
  'Part 2 Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]

const silverFeatures = [
  'Expert Teacher Tutorials',
  'One-on-one Expert Teacher Tutorials (45 mins)',
  'Pre-test Strategy Session',
  'Assessment with Expert Feedback',
  'Mock Test',
  'Writing Task 1',
  'Writing Task 2',
  'Part 2 Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]

const goldFeatures = [
  'Expert Teacher Tutorials',
  'One-on-one Expert Teacher Tutorials (45 mins)',
  'Pre-test Strategy Session',
  'Post-test Strategy Session',
  'Assessment with Expert Feedback',
  'Mock Test',
  'Writing Task 1',
  'Writing Task 2',
  'Part 2 Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]

const expressFeatures = [
  'Expert Teacher Tutorials (45 mins)',
  'One-on-one Expert Teacher Tutorial (45 mins)',
  'Assessment with Expert Feedback',
  'Mock Test',
  'Writing Task 1',
  'Writing Task 2',
  'Part 2 Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]

const expressPlusFeatures = [
  'Expert Teacher Tutorials (45 mins)',
  'One-on-one Expert Teacher Tutorials (45 mins)',
  'Pre-test Strategy Session',
  'Assessment with Expert Feedback',
  'Mock Test',
  'Writing Task 1',
  'Writing Task 2',
  'Part 2 Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]

const speakingIntensiveFeatures = [
  'Expert Teacher Tutorials',
  'One-on-one Expert Teacher Tutorials (45 mins)',
  'Pre-test Strategy Session',
  'Post-test Strategy Session',
  'Assessment with Expert Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]

const writingIntensiveFeatures = [
  'Expert Teacher Tutorials',
  'One-on-one Expert Teacher Tutorials (45 mins)',
  'Pre-test Strategy Session',
  'Post-test Strategy Session',
  'Assessment with Expert Feedback',
  'Practice Questions',
  'Overview Lessons',
  'Methods Lessons',
  'Live Class Recordings'
]
</script>

<style scoped>
.pricing-container {
  background-color: #f9fafb;
  min-height: 100vh;
  padding: 2rem 1rem;
}

.promo-banner {
  background-color: #fde047;
  color: #000;
  padding: 0.75rem 1rem;
  font-size: 0.875rem;
  font-weight: 500;
  margin-bottom: 1.5rem;
  border-radius: 0.25rem;
}

.main-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 0.5rem;
}

.cta-button {
  background-color: #2563eb;
  color: white;
  padding: 0.5rem 1.5rem;
  border: none;
  border-radius: 0.25rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  cursor: pointer;
}

.upgrade-info {
  color: #2563eb;
  font-size: 0.875rem;
  cursor: pointer;
}

.upgrade-info:hover {
  text-decoration: underline;
}
</style>