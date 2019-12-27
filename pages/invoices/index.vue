<template>
  <div>
    <div class="logo columns">
      <div class="column is-2">
        <logo />
      </div>
      <h2 class="subtitle column is-10">Vue Invoice</h2>
    </div>
    <div class="container">
      <div class="invoice-list">
        <div class="columns">
          <div class="column">
            <h3>Item Name</h3>
          </div>
          <div class="column">
            <h3>Quantity</h3>
          </div>
          <div class="column">
            <h3>Unit Price</h3>
          </div>
          <div class="column">
            <h3>Sub Total</h3>
          </div>
        </div>
        <hr />
        <div
          v-for="(item, index) in cartItems"
          v-bind:key="index"
          class="columns"
        >
          <div class="column">
            <label for="index">
              {{ item.Name ? item.Name : 'Item Name ' + index }}
            </label>
          </div>
          <div class="column">
            <input v-model="item.Quantity" type="number" min="1" />
          </div>
          <div class="column">
            <input v-model="item.UnitPrice" type="number" min="0" />
          </div>
          <div class="column">
            <div class="columns">
              <div class="column">
                <label for="index">{{ item.Quantity * item.UnitPrice }}</label>
              </div>
              <div class="column">
                <span>
                  <a @click="removeRowFromCartItems(index)" class="button">
                    X
                  </a>
                </span>
              </div>
            </div>
          </div>
        </div>
        <hr />
        <div class="columns">
          <div class="column">
            <span></span>
          </div>
          <div class="column text-r">
            <span>Total Price:&nbsp;</span>
          </div>
          <div class="column">
            <span>
              {{ TotalPrice }}
            </span>
          </div>
          <div class="column add-button">
            <span>
              <a @click="addRowInCartItems" class="button is-primary">+</a>
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data() {
    return {
      cartItems: [
        {
          Name: '',
          Quantity: 1,
          UnitPrice: 0,
          SubTotal: 0
        }
      ]
    }
  },
  computed: {
    TotalPrice() {
      return this.cartItems.reduce((total, item) => {
        return total + Number(item.Quantity * item.UnitPrice)
      }, 0)
    }
  },
  methods: {
    addRowInCartItems() {
      const row = {
        Name: '',
        Quantity: 1,
        UnitPrice: 0,
        SubTotal: 0
      }
      this.cartItems.push(row)
    },
    removeRowFromCartItems(index) {
      this.cartItems.splice(index, 1)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.logo svg {
  max-width: 100px;
  margin: 0 10px;
  max-height: 100px;
}

.logo h2 {
  text-align: center;
  padding-top: 30px;
}

.invoice-list {
  width: 100%;
}

.invoice-list * {
  text-align: left;
}

.invoice-list div.add-button {
  text-align: right;
}

.text-r {
  text-align: right;
}
</style>
