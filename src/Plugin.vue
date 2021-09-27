<template>
  <div class="integration">
    <div v-if="!modalIsOpen">
      <SfCarousel
        v-if="model.products"
        :settings="{ peek: 16, breakpoints: { 1023: { peek: 0, perView: 2 } } }"
        class="carousel"
      >
        <template #prev="{go}">
          <SfArrow
            aria-label="prev"
            class="sf-arrow--left sf-arrow--long"
            @click="go('prev')"
          />
        </template>
        <template #next="{go}">
          <SfArrow
            aria-label="next"
            class="sf-arrow--right sf-arrow--long"
            @click="go('next')"
          />
        </template>
        <!-- for some reason, it asks to register the SfCarouselItem component -->
        <!-- so it's not working -->
        <!-- <SfCarouselItem
          v-for="(product, index) in model.products"
          :key="index"  
        > -->
        <SfProductCard
          v-for="(product, index) in model.products"
          :key="index"
          :image="product.image"
          :title="product.name"
          :link="`http://product.com/${product.name}`"
          :regular-price="product.price.regular"
          :special-price="product.price.special"
          :score-rating="product.rating.score"
          :max-rating="product.rating.max"
          :is-on-wishlist="product.isOnWishlist"
          show-add-to-cart-button
          :reviews-count="reviews"
          :badge-label="badgeLabel"
          :badge-color="badgeColor"
          wishlist-icon="heart"
          @click.native="selectItem"
        />
        <!-- </SfCarouselItem> -->
      </SfCarousel>
      <button class="uk-button uk-width-1-1 uk-margin-small-top" @click.prevent="openSelection">Manage products</button>
    </div>

    <div v-if="modalIsOpen">
      <div class="integration-selection">
        <div class="uk-flex uk-flex-middle util__grow integration-selection__header">
          <div class="util__grow">
            <form class="uk-margin-right">
              <input
                v-model="search_term"
                placeholder="Search"
                class="uk-width-1-1"
              >
            </form>
          </div>
          <div class="uk-position-relative uk-text-nowrap">
            <div slot="actions">
              <a class="uk-button" @click="closeSelection">
                <i class="uk-icon-close"></i> Close
              </a>
            </div>
          </div>
        </div>
        <div class="integration-items">
          <div v-for="(product, index) in products" :key="index">
            <SfProductCard
              :image="product.image"
              :title="product.name"
              :link="`http://product.com/${product.name}`"
              :regular-price="product.price.regular"
              :special-price="product.price.special"
              :score-rating="product.rating.score"
              :max-rating="product.rating.max"
              :is-on-wishlist="product.isOnWishlist"
              show-add-to-cart-button
              :reviews-count="reviews"
              :badge-label="badgeLabel"
              :badge-color="badgeColor"
              wishlist-icon="heart"
              @click.native="selectItem(product)"
            />
          </div>
        </div>
      </div>    
    </div>
  </div>
</template>

<script>
import {
  SfCarousel,
  SfArrow,
  SfProductCard,
} from '@storefront-ui/vue';

export default {
  mixins: [window.Storyblok.plugin],
  components: {
    SfCarousel,
    SfArrow,
    SfProductCard,
  },
  data() {
    return {
      modalIsOpen: false,
      search_term: '',
      products: [
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: true,
          reviews: 8,
          badgeLabel: '',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ', special: '$ 25.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: true,
          reviews: 8,
          badgeLabel: '-50%',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: false,
          reviews: 8,
          badgeLabel: '',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: false,
          reviews: 8,
          badgeLabel: '',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ', special: '$ 45.00' },
          rating: { max: 5, score: 4 },
          isOnWishlist: false,
          reviews: 8,
          badgeLabel: '-10%',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: false,
          reviews: 8,
          badgeLabel: '',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: false,
          reviews: 8,
          badgeLabel: '',
          badgeColor: 'color-primary',
        },
        {
          name: 'Cream Beach Bag',
          image:
            'https://static.netshoes.com.br/produtos/camisa-selecao-italia-home-2021-sn-torcedor-puma-masculina/52/NWG-0394-852/NWG-0394-852_zoom1.jpg',
          price: { regular: '$ 50.00 ' },
          rating: { max: 5, score: 4 },
          isOnWishlist: false,
          reviews: 8,
          badgeLabel: '',
          badgeColor: 'color-primary',
        },
      ]
    }
  },
  watch: {
    'model': {
      handler(value) {
        this.$emit('changed-model', value);
      },
      deep: true
    }
  },
  methods: {
    initWith() {
      return {
        // needs to be equal to your storyblok plugin name
        plugin: 'carousel-storefrontui',
        products: [],
      }
    },
    openSelection() {
      this.modalIsOpen = true
      this.$emit('toggle-modal', true)
    },
    closeSelection() {
      this.modalIsOpen = false
      this.$emit('toggle-modal', false)
    },
    selectItem(product) {
      this.model.products.push(product)
    },
  },
}
</script>

<style lang="scss">
.integration-selection {
  min-height: 700px;
  overflow-x: hidden;
  overflow-y: auto;
}

.integration-selection__header {
  position: sticky;
  top: 0px;
  background: #ffffff;
  padding-bottom: 10px;
}

.integration-items {
  display: grid;
  grid-template-columns: repeat(auto-fill, 154px);
  justify-content: center;
}
</style>
