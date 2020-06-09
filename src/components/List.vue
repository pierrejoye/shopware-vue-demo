<template>
  <v-app id="inspire">
    <v-card class="mx-auto" max-width="1200">
      <v-container>
        <v-row dense>
          <v-col cols="12">
            <v-card>
              <v-img
                src="https://cdn.vuetifyjs.com/images/cards/house.jpg"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title>Food & Lifestyle</v-card-title>
              </v-img>

              <v-card-actions>
                <v-spacer></v-spacer>

                <v-btn icon>
                  <v-icon>mdi-heart</v-icon>
                </v-btn>

                <v-btn icon>
                  <v-icon>mdi-bookmark</v-icon>
                </v-btn>

                <v-btn icon>
                  <v-icon>mdi-share-variant</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
          <v-col v-for="card in cards" :key="card.title" cols="12" xs="12" md="6" lg="6" xl="6">
            <v-card>
              <v-img
                :src="card.src"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title v-text="card.title"></v-card-title>
              </v-img>

              <v-card-actions>
                <v-spacer></v-spacer>

                <v-btn icon>
                  <v-icon>mdi-heart</v-icon>
                </v-btn>

                <v-btn icon>
                  <v-icon>mdi-bookmark</v-icon>
                </v-btn>

                <v-btn icon>
                  <v-icon>mdi-share-variant</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col
            v-for="product in productsList"
            :key="product.id"
            cols="12"
            xs="12"
            md="6"
            lg="6"
            xl="6"
          >
            <p>{{ product.name }} - {{ getPrice(product) }}</p> - <p>{{ getImage(product) }}</p>
            <span v-html="product.description "></span>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-app>
</template>
<script>
import Vue from "vue";
import axios from "axios";

export default Vue.extend({
  data: () => ({
    productsList: null,
    cards: [
      {
        title: "Favorite road trips",
        src: "/assets/images/road.jpg",
        flex: 6
      },
      {
        title: "Sunshine rocks",
        src: "/assets/images/sunshine.jpg",
        flex: 6
      },
      {
        title: "Favorite road trips 2",
        src: "/assets/images/road.jpg",
        flex: 6
      },
      {
        title: "Some Random image",
        src: "/assets/images/300.jpg",
        flex: 6
      },
      {
        title: "Some other random images",
        src: "/assets/images/300_1.jpg",
        flex: 6
      },
      {
        title: "Yet another one",
        src: "/assets/images/300_2.jpg",
        flex: 6
      },
      {
        title: "And the last one ;)",
        src: "/assets/images/300_3.jpg",
        flex: 6
      }
    ]
  }),
  mounted() {
    const headers = {
      "Content-Type": "application/json",
      "sw-access-key": "SWSCVHRITKJEU0ZJUXDXCFZBTW"
    };
    const data = {
      filter: [
        {
          type: "equals",
          field: "categories.id",
          value: "8d7e63f5793f494d818ea433c7d2dfba"
        }
      ]
    };
    const ApiUrl =
      "https://pierre.demo.enterprise.shopware.com/sales-channel-api/v1/product";

    axios
      .post(ApiUrl, data, { headers: headers })
      .then(res => {
        this.productsList = res.data.data;
        console.log(this.productsList);
      })
      .catch(error => {
        console.log(error);
        // Manage errors if found any
      });
  },
  methods: {
    getImage: function(product) {
      return product.cover.media.url;
    },
    getPrice: function(product) {
        return product.price[0].net;
    }
  }
});
</script>