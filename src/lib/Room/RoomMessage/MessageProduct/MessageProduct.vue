<template>
  <div class="vac-message-product-question">
    <div class="product-info">
      <img v-if="thumbnail" :src="thumbnail" class="product-image" :alt="name" />
      <div class="product-details">
        <div class="product-name">{{ name }}</div>
        <div class="product-meta">
            <span v-if="price" class="product-price">
              <span v-if="hasDiscount">قیمت با تخفیف</span>
              <span v-else>قیمت</span>
                {{ formattedPrice }}
            </span>
        </div>
        <a
          v-if="url"
          :href="url"
          target="_blank"
          rel="noopener"
          class="btn-view"
        >
          {{ buttonText }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MessageProduct',

  props: {
    message: { type: Object, required: true }
  },

  computed: {
    thumbnail() {
      return this.message.metadata.thumbnail || ''
    },
    name() {
      return this.message.metadata.name || ''
    },
    price() {
      return this.hasDiscount ? this.message.metadata.discount_price : this.message.metadata.price || 0
    },
    hasDiscount() {
      return !!this.message.metadata.discount_price
    },
    url() {
      return this.message.metadata.url || null
    },
    buttonText() {
      return this.message.metadata.button_text || 'مشاهده محصول'
    },
    formattedPrice() {
      const number = Number(this.price)
      return isNaN(number) ? this.price : number.toLocaleString('fa-IR')
    }
  }
}
</script>
