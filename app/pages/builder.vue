<template>
    <div class="builder-container">
        <div class="builder-header">
            <h1 class="builder-title">Pricing Table Builder</h1>
            <p class="builder-subtitle">
                Build and customize your embeddable pricing table with live preview
            </p>
        </div>

        <div class="builder-layout">
            <!-- Configuration Panel -->
            <div class="config-panel">
                <div class="config-section">
                    <h2 class="config-title">Configuration</h2>

                    <!-- Course Selection -->
                    <div class="form-group">
                        <label class="form-label">Course Type</label>
                        <select v-model="selectedCourse" class="form-select">
                            <option v-for="course in courseOptions" :key="course" :value="course">
                                {{ course }}
                            </option>
                        </select>
                    </div>

                    <!-- Discount Code -->
                    <div class="form-group">
                        <label class="form-label">Discount Code (Optional)</label>
                        <select v-model="selectedDiscountCode" class="form-select">
                            <option value="">No Discount</option>
                            <option v-for="(percent, code) in discountCodes" :key="code" :value="code">
                                {{ code }} ({{ percent }}% off)
                            </option>
                        </select>
                        <small class="form-hint">Or enter custom code below:</small>
                        <input v-model="customDiscountCode" type="text" placeholder="Custom discount code"
                            class="form-input" />
                    </div>

                    <!-- Affiliate Code -->
                    <div class="form-group">
                        <label class="form-label">Affiliate Code (Optional)</label>
                        <input v-model="affiliateCode" type="text" placeholder="Enter affiliate code"
                            class="form-input" />
                    </div>

                    <!-- Package Selection -->
                    <div class="form-group">
                        <label class="form-label">Display Packages</label>
                        <div class="checkbox-group">
                            <label v-for="pkg in packageOptions" :key="pkg" class="checkbox-label">
                                <input type="checkbox" :value="pkg" v-model="selectedPackages" class="checkbox-input" />
                                <span class="checkbox-text">{{ pkg }}</span>
                            </label>
                        </div>
                        <small class="form-hint">Leave all unchecked to show all packages</small>
                    </div>

                    <!-- Generated URLs -->
                    <div class="form-group">
                        <label class="form-label">Generated URLs</label>

                        <div class="url-section">
                            <h4 class="url-title">Embed URL</h4>
                            <div class="url-container">
                                <input :value="embedUrl" readonly class="url-input" ref="embedUrlInput" />
                                <button @click="copyUrl('embed')" class="copy-btn">
                                    {{ copiedEmbed ? 'Copied!' : 'Copy' }}
                                </button>
                            </div>
                        </div>

                        <div class="url-section">
                            <h4 class="url-title">Direct Link</h4>
                            <div class="url-container">
                                <input :value="directUrl" readonly class="url-input" ref="directUrlInput" />
                                <button @click="copyUrl('direct')" class="copy-btn">
                                    {{ copiedDirect ? 'Copied!' : 'Copy' }}
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Embed Code -->
                    <div class="form-group">
                        <label class="form-label">Embed Code</label>
                        <textarea :value="embedCode" readonly class="embed-textarea" ref="embedCodeTextarea"></textarea>
                        <button @click="copyEmbedCode" class="copy-btn-full">
                            {{ copiedEmbedCode ? 'Copied!' : 'Copy Embed Code' }}
                        </button>
                    </div>
                </div>
            </div>

            <!-- Preview Panel -->
            <div class="preview-panel">
                <div class="preview-header">
                    <h3 class="preview-title">Live Preview</h3>
                    <div class="preview-controls">
                        <button @click="refreshPreview" class="refresh-btn" :disabled="isRefreshing">
                            {{ isRefreshing ? 'Refreshing...' : 'Refresh' }}
                        </button>
                    </div>
                </div>

                <div class="preview-container">
                    <iframe :src="embedUrl" class="preview-iframe" :key="previewKey" @load="onPreviewLoad"
                        title="Pricing Table Preview"></iframe>

                    <!-- Loading overlay -->
                    <div v-if="isLoading" class="loading-overlay">
                        <div class="loading-spinner"></div>
                        <p>Loading preview...</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, computed, watch, nextTick } from 'vue'

// Page metadata
useHead({
    title: 'Pricing Table Builder - E2 Embeddable Tables',
    meta: [
        { name: 'description', content: 'Build and customize your embeddable pricing table with live preview' }
    ]
})

// Reactive data
const selectedCourse = ref('IELTS General')
const selectedDiscountCode = ref('')
const customDiscountCode = ref('')
const affiliateCode = ref('')
const selectedPackages = ref<string[]>([])
const previewKey = ref(0)
const isLoading = ref(true)
const isRefreshing = ref(false)

// Copy states
const copiedEmbed = ref(false)
const copiedDirect = ref(false)
const copiedEmbedCode = ref(false)

// Template refs
const embedUrlInput = ref<HTMLInputElement>()
const directUrlInput = ref<HTMLInputElement>()
const embedCodeTextarea = ref<HTMLTextAreaElement>()

// Configuration options
const courseOptions = [
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

const packageOptions = [
    'Express',
    'Express Plus',
    '4-Week Intensive',
    'Bronze',
    'Silver',
    'Gold'
]

const discountCodes = {
    'INVEST25': 25,
    'SAVE20': 20,
    'STUDENT15': 15,
    'EARLY30': 30,
    'SPECIAL10': 10
}

// Computed URLs
const baseUrl = computed(() => {
    if (typeof window !== 'undefined') {
        return window.location.origin
    }
    return 'https://your-domain.com' // Replace with your actual domain
})

const queryParams = computed(() => {
    const params = new URLSearchParams()

    params.set('course', selectedCourse.value)

    const discountCode = customDiscountCode.value || selectedDiscountCode.value
    if (discountCode) {
        params.set('discountCode', discountCode)
    }

    if (affiliateCode.value) {
        params.set('affiliateCode', affiliateCode.value)
    }

    if (selectedPackages.value.length > 0) {
        params.set('displayedPackages', selectedPackages.value.join(','))
    }

    return params.toString()
})

const embedUrl = computed(() => {
    return `${baseUrl.value}/embed?${queryParams.value}`
})

const directUrl = computed(() => {
    return `${baseUrl.value}/embed?${queryParams.value}`
})

const embedCode = computed(() => {
    return `<iframe
  src="${embedUrl.value}"
  width="100%"
  height="800"
  frameborder="0"
  style="border: none; border-radius: 8px;"
  title="E2 Pricing Table">
</iframe>`
})

// Methods
const refreshPreview = async () => {
    isRefreshing.value = true
    isLoading.value = true
    previewKey.value++

    await nextTick()

    setTimeout(() => {
        isRefreshing.value = false
    }, 500)
}

const onPreviewLoad = () => {
    isLoading.value = false
}

const copyUrl = async (type: 'embed' | 'direct') => {
    try {
        const url = type === 'embed' ? embedUrl.value : directUrl.value
        await navigator.clipboard.writeText(url)

        if (type === 'embed') {
            copiedEmbed.value = true
            setTimeout(() => { copiedEmbed.value = false }, 2000)
        } else {
            copiedDirect.value = true
            setTimeout(() => { copiedDirect.value = false }, 2000)
        }
    } catch (err) {
        console.error('Failed to copy URL:', err)
    }
}

const copyEmbedCode = async () => {
    try {
        await navigator.clipboard.writeText(embedCode.value)
        copiedEmbedCode.value = true
        setTimeout(() => { copiedEmbedCode.value = false }, 2000)
    } catch (err) {
        console.error('Failed to copy embed code:', err)
    }
}

// Watch for changes to refresh preview automatically
watch([selectedCourse, selectedDiscountCode, customDiscountCode, affiliateCode, selectedPackages], () => {
    refreshPreview()
}, { deep: true })
</script>

<style scoped>
.builder-container {
    min-height: 100vh;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 2rem 1rem;
}

.builder-header {
    text-align: center;
    margin-bottom: 3rem;
}

.builder-title {
    font-size: 2.5rem;
    font-weight: 700;
    color: white;
    margin-bottom: 0.5rem;
}

.builder-subtitle {
    font-size: 1.1rem;
    color: rgba(255, 255, 255, 0.9);
    max-width: 600px;
    margin: 0 auto;
}

.builder-layout {
    display: grid;
    grid-template-columns: 400px 1fr;
    gap: 2rem;
    max-width: 1400px;
    margin: 0 auto;
}

@media (max-width: 1024px) {
    .builder-layout {
        grid-template-columns: 1fr;
        gap: 1.5rem;
    }
}

.config-panel {
    background: white;
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

.config-section {
    padding: 2rem;
}

.config-title {
    font-size: 1.5rem;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 1.5rem;
}

.form-group {
    margin-bottom: 1.5rem;
}

.form-label {
    display: block;
    font-weight: 500;
    color: #374151;
    margin-bottom: 0.5rem;
}

.form-select,
.form-input {
    width: 100%;
    padding: 0.75rem;
    border: 1px solid #d1d5db;
    border-radius: 6px;
    font-size: 0.875rem;
    transition: border-color 0.2s;
}

.form-select:focus,
.form-input:focus {
    outline: none;
    border-color: #3b82f6;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.form-hint {
    display: block;
    font-size: 0.75rem;
    color: #6b7280;
    margin-top: 0.25rem;
}

.checkbox-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.checkbox-label {
    display: flex;
    align-items: center;
    font-size: 0.875rem;
    cursor: pointer;
}

.checkbox-input {
    margin-right: 0.5rem;
}

.checkbox-text {
    color: #374151;
}

.url-section {
    margin-bottom: 1rem;
}

.url-title {
    font-size: 0.875rem;
    font-weight: 500;
    color: #374151;
    margin-bottom: 0.5rem;
}

.url-container {
    display: flex;
    gap: 0.5rem;
}

.url-input {
    flex: 1;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
    font-size: 0.75rem;
    padding: 0.5rem;
    background: #f9fafb;
    border: 1px solid #e5e7eb;
    border-radius: 4px;
}

.copy-btn {
    padding: 0.5rem 1rem;
    background: #3b82f6;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 0.75rem;
    cursor: pointer;
    transition: background-color 0.2s;
}

.copy-btn:hover {
    background: #2563eb;
}

.embed-textarea {
    width: 100%;
    height: 120px;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
    font-size: 0.75rem;
    padding: 0.75rem;
    border: 1px solid #d1d5db;
    border-radius: 6px;
    background: #f9fafb;
    resize: vertical;
}

.copy-btn-full {
    width: 100%;
    padding: 0.75rem;
    background: #10b981;
    color: white;
    border: none;
    border-radius: 6px;
    font-weight: 500;
    cursor: pointer;
    transition: background-color 0.2s;
    margin-top: 0.5rem;
}

.copy-btn-full:hover {
    background: #059669;
}

.preview-panel {
    background: white;
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

.preview-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 2rem;
    border-bottom: 1px solid #e5e7eb;
    background: #f9fafb;
}

.preview-title {
    font-size: 1.25rem;
    font-weight: 600;
    color: #1f2937;
}

.refresh-btn {
    padding: 0.5rem 1rem;
    background: #6366f1;
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 0.875rem;
    cursor: pointer;
    transition: background-color 0.2s;
}

.refresh-btn:hover:not(:disabled) {
    background: #5855eb;
}

.refresh-btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

.preview-container {
    position: relative;
    height: 800px;
}

.preview-iframe {
    width: 100%;
    height: 100%;
    border: none;
}

.loading-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255, 255, 255, 0.9);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
}

.loading-spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #e5e7eb;
    border-left-color: #3b82f6;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    to {
        transform: rotate(360deg);
    }
}
</style>