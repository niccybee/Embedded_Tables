<template>
  <PricingTable
    :course="course"
    :discount-code="discountCode"
    :affiliate-code="affiliateCode"
    :displayed-packages="displayedPackages"
  />
</template>

<script setup lang="ts">
// Get query parameters from the route
const route = useRoute()

// Extract query parameters with defaults
const course = computed(() => {
  const courseParam = route.query.course as string
  const validCourses = [
    'IELTS Academic',
    'IELTS General', 
    'PTE Academic',
    'PTE Core',
    'TOEFL',
    'CELPIP LS',
    'CELPIP',
    'OET Nurses',
    'OET Doctors'
  ]
  
  return validCourses.includes(courseParam) ? courseParam : 'IELTS General'
})

const discountCode = computed(() => {
  return (route.query.discountCode as string) || ''
})

const affiliateCode = computed(() => {
  return (route.query.affiliateCode as string) || ''
})

const displayedPackages = computed(() => {
  const packages = route.query.displayedPackages as string
  if (!packages) return ''
  
  const validPackages = [
    'Express',
    'Express Plus', 
    '4-Week Intensive',
    'Bronze',
    'Silver',
    'Gold'
  ]
  
  // Filter and validate packages
  const requestedPackages = packages.split(',').map(pkg => pkg.trim())
  const validRequestedPackages = requestedPackages.filter(pkg => validPackages.includes(pkg))
  
  return validRequestedPackages.join(',')
})

// Set page meta for embedding
useHead({
  title: `${course.value} Pricing Packages`,
  meta: [
    {
      name: 'description',
      content: `Choose the best ${course.value} preparation package for your needs. Discount codes available.`
    },
    {
      name: 'viewport',
      content: 'width=device-width, initial-scale=1'
    }
  ]
})
</script>

<style>
/* Global styles for embedded context */
body.embedded-pricing {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
}

/* Remove any default margins/padding that might interfere with embedding */
.embedded-pricing * {
  box-sizing: border-box;
}
</style>