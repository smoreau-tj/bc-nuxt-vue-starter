<template>
  <div id="category">
    <SfHeader
      title="Tommy John"
    >
      <template #navigation>
        <SfHeaderNavigationItem>
          <a
            href="/"
            :style="{ display: 'flex', alignItems: 'center', height: '100%' }"
          >
            Home
          </a>
        </SfHeaderNavigationItem>
        <SfHeaderNavigationItem>
          <a
            href="/products"
            :style="{ display: 'flex', alignItems: 'center', height: '100%' }"
          >
            Shop All
          </a>
        </SfHeaderNavigationItem>
      </template>
    </SfHeader>
    <div class="navbar section">
      <div class="navbar__aside desktop-only">
        <h1 class="navbar__title">
          Shop All
        </h1>
      </div>
      <div class="navbar__main">
        <div class="navbar__counter">
          <span class="navbar__label desktop-only">Products found: </span>
          <strong class="desktop-only">{{ category.products.edges.length }}</strong>
          <span class="navbar__label mobile-only">{{ category.products.edges.length }}</span>
        </div>
      </div>
    </div>
    <div class="main section">
      <div class="products">
        <div class="products__list">
          <SfProductCard
            v-for="(product, i) in category.products.edges"
            :key="i"
            :title="product.node.name"
            :image="product.node.defaultImage.url"
            :link="'/products' + product.node.path"
            :regular-price="'$' + product.node.prices.price.value.toFixed(2)"
            class="products__product-card"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import '@storefront-ui/vue/styles.scss'
import {
  SfProductCard,
  SfHeader
} from '@storefront-ui/vue'
export default {
  components: {
    SfProductCard,
    SfHeader
  },
  async asyncData ({ params }) {
    const result = await axios({
      method: 'POST',
      url: 'https://tommyjohn-poc.mybigcommerce.com/graphql',
      headers: {
        Authorization: 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzI1NiJ9.eyJlYXQiOjE2NDA4MzQ5NTEsInN1Yl90eXBlIjoyLCJ0b2tlbl90eXBlIjoxLCJjb3JzIjpbImh0dHA6Ly9sb2NhbGhvc3Q6MzAwMCJdLCJjaWQiOjEsImlhdCI6MTYwOTM1OTc0Miwic3ViIjoiam16czV6cXRvbHh3Y28wNWM0MXBoMjNsc3JyeWVhZCIsInNpZCI6MTAwMDg2MTQyOSwiaXNzIjoiQkMifQ.ytbw9pVzObiPz1hatlgXc8mrxew6d-R7cdlJUiDCV1rirDZI1gQ-h4wSryJQjHLZDtniYp_UtCij62XpgGYUuw'
      },
      data: {
        query: `
          query CategoryByUrl {
            site {
              route(path: "/shop-all/") {
                node {
                  id
                  ... on Category {
                    name
                    entityId
                    products {
                      edges {
                        node {
                          name
                          path
                          defaultImage {
                            url(width: 216, height: 326)
                            altText
                          }
                          prices {
                            price {
                              value
                              currencyCode
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        `
      }
    })
    const productsData = result.data.data.site.route.node
    // debugger
    // console.log(productsData)

    return { category: productsData }
  },
  data () {
    return {
      category: {}
    }
  },
  methods: {
  }
}
</script>
<style lang="scss" scoped>

</style>
