<template>
  <div class="pricing-card" :class="[color, { popular: isPopular }]">
    <!-- Popular Badge -->
    <div v-if="isPopular" class="popular-badge">
      Special Summer Discount
    </div>

    <!-- Header -->
    <div class="card-header">
      <h3 class="card-title">{{ title }}</h3>
      <p class="card-subtitle">{{ subtitle }}</p>
      <p class="card-description">{{ description }}</p>
      <p class="card-student-text">{{ studentText }}</p>
    </div>

    <!-- Pricing -->
    <div class="card-pricing">
      <div class="pricing-row">
        <span class="original-price">${{ originalPrice }}</span>
        <span class="discounted-price">${{ discountedPrice }} USD</span>
      </div>
      <div class="discount-info">{{ discountPercent }}% DISCOUNT APPLIED</div>
      <div class="gst-info">incl 10.00% GST ⓘ</div>
    </div>

    <!-- Upgrade Button -->
    <div class="card-button">
      <button 
        class="upgrade-btn"
        @click="handleUpgrade"
      >
        UPGRADE
      </button>
    </div>

    <!-- Features List -->
    <div class="card-features">
      <div class="features-title">{{ featuresTitle }}</div>
      <ul class="features-list">
        <li v-for="(feature, index) in features" :key="index">
          {{ feature }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  title: string
  subtitle: string
  description: string
  studentText: string
  originalPrice: number
  discountedPrice: string
  discountPercent: number
  affiliateCode: string
  color: 'orange' | 'blue' | 'yellow' | 'purple' | 'indigo' | 'green' | 'pink'
  features: string[]
  isPopular?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  isPopular: false
})

const emit = defineEmits<{
  upgrade: [packageData: any]
}>()

const featuresTitle = computed(() => {
  if (props.title.includes('Express')) return 'Expert Teacher Tutorials'
  return 'Assessment with Expert Feedback'
})

const handleUpgrade = () => {
  const packageData = {
    title: props.title,
    price: props.discountedPrice,
    originalPrice: props.originalPrice,
    affiliateCode: props.affiliateCode,
    features: props.features
  }
  
  emit('upgrade', packageData)
  
  // Here you would typically redirect to payment gateway
  // For now, we'll just log the data
  console.log('Upgrade clicked:', packageData)
}
</script>

<style scoped>
.card-title {
  font-size: 1.25rem;
  font-weight: bold;
  color: #1f2937;
  margin-bottom: 0.25rem;
}

.card-subtitle {
  font-size: 0.875rem;
  color: #4b5563;
  margin-bottom: 0.25rem;
}

.card-description {
  font-size: 0.875rem;
  color: #4b5563;
  margin-bottom: 0.75rem;
}

.card-student-text {
  font-size: 0.875rem;
  color: #374151;
  font-style: italic;
}

.pricing-row {
  margin-bottom: 0.5rem;
}

.original-price {
  font-size: 1.125rem;
  color: #6b7280;
  text-decoration: line-through;
}

.discounted-price {
  font-size: 1.5rem;
  font-weight: bold;
  color: #dc2626;
  margin-left: 0.5rem;
}

.discount-info {
  font-size: 0.875rem;
  color: #4b5563;
  margin-bottom: 0.25rem;
}

.gst-info {
  font-size: 0.75rem;
  color: #6b7280;
}

.features-title {
  font-size: 0.875rem;
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 0.75rem;
}
</style>