<template>
  <div class="demo-container">
    <h1 class="main-heading">E2 Pricing Tables Demo</h1>
    
    <div class="demo-content">
      <h2 class="section-heading">Embeddable Pricing Table</h2>
      <p class="section-description">
        This pricing table can be embedded in any website using query parameters to customize the display.
      </p>

      <div class="params-section">
        <h3 class="subsection-heading">Available Query Parameters:</h3>
        <ul class="params-list">
          <li><strong>course:</strong> IELTS Academic, IELTS General, PTE Academic, PTE Core, TOEFL, CELPIP LS, CELPIP, OET Nurses, OET Doctors</li>
          <li><strong>discountCode:</strong> Any discount code (e.g., INVEST25, SAVE20, STUDENT15, EARLY30)</li>
          <li><strong>affiliateCode:</strong> Affiliate ID for tracking</li>
          <li><strong>displayedPackages:</strong> Comma-separated list: Express, Express Plus, 4-Week Intensive, Bronze, Silver, Gold</li>
        </ul>
      </div>

      <div class="examples-section">
        <h3 class="subsection-heading">Example URLs:</h3>
        <div class="examples-list">
          <div>
            <a href="/embed?course=IELTS Academic&discountCode=INVEST25&affiliateCode=ABC123" 
               class="example-link" target="_blank">
              Full IELTS Academic with 25% discount
            </a>
          </div>
          <div>
            <a href="/embed?course=PTE Academic&displayedPackages=Bronze,Silver,Gold" 
               class="example-link" target="_blank">
              PTE Academic - Only Bronze, Silver, Gold packages
            </a>
          </div>
          <div>
            <a href="/embed?course=TOEFL&discountCode=SAVE20&displayedPackages=Express,Express Plus" 
               class="example-link" target="_blank">
              TOEFL - Express packages only with 20% discount
            </a>
          </div>
        </div>
      </div>

      <div class="preview-section">
        <h3 class="subsection-heading">Live Preview:</h3>
        <iframe 
          src="/embed?course=IELTS General&discountCode=INVEST25&affiliateCode=DEMO123"
          class="preview-iframe"
          title="Pricing Table Preview"
        ></iframe>
      </div>

      <div class="embed-code-section">
        <h3 class="subsection-heading">Embedding Code:</h3>
        <div class="code-block">
          <code>
&lt;iframe 
  src="https://your-domain.com/embed?course=IELTS General&amp;discountCode=INVEST25&amp;affiliateCode=YOUR_ID"
  width="100%" 
  height="800"
  frameborder="0"
  title="E2 Pricing Table"
&gt;&lt;/iframe&gt;
          </code>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
useHead({
  title: 'E2 Embeddable Pricing Tables',
  meta: [
    {
      name: 'description',
      content: 'Customizable and embeddable pricing tables for E2 test preparation courses'
    }
  ]
})
</script>

<style scoped>
.demo-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.main-heading {
  font-size: 1.875rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 2rem;
}

.demo-content {
  max-width: 64rem;
  margin: 0 auto;
}

.section-heading {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.section-description {
  margin-bottom: 1.5rem;
  color: #4b5563;
}

.params-section {
  background-color: #f3f4f6;
  padding: 1rem;
  border-radius: 0.5rem;
  margin-bottom: 1.5rem;
}

.subsection-heading {
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.params-list {
  font-size: 0.875rem;
  line-height: 1.5;
}

.params-list li {
  margin-bottom: 0.25rem;
}

.examples-section {
  margin-bottom: 1.5rem;
}

.examples-list {
  font-size: 0.875rem;
}

.examples-list > div {
  margin-bottom: 0.5rem;
}

.example-link {
  color: #2563eb;
  text-decoration: none;
}

.example-link:hover {
  text-decoration: underline;
}

.preview-section {
  border: 1px solid #e5e7eb;
  border-radius: 0.5rem;
  padding: 1rem;
  margin-bottom: 1.5rem;
}

.preview-iframe {
  width: 100%;
  height: 24rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.25rem;
}

.embed-code-section {
  margin-top: 1.5rem;
}

.code-block {
  background-color: #1f2937;
  color: #f3f4f6;
  padding: 1rem;
  border-radius: 0.25rem;
  font-size: 0.875rem;
  overflow-x: auto;
}

.code-block code {
  white-space: pre;
}
</style>