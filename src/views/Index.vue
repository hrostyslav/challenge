<template>
  <div>
    <h1 id="hello">Hello AMPHTML World!</h1>

    <amp-base-carousel width="600" height="400" layout="responsive">
      <amp-img
        src="https://source.unsplash.com/Ji_G7Bu1MoM/600x400"
        width="600"
        height="400"
        layout="responsive"
      ></amp-img>
      <amp-img
        src="https://source.unsplash.com/4yCXNMLP9g8/600x400"
        width="600"
        height="400"
        layout="responsive"
      ></amp-img>
      <amp-img
        src="https://source.unsplash.com/QrgRXH81DXk/600x400"
        width="600"
        height="400"
        layout="responsive"
      ></amp-img>
      <amp-img
        src="https://source.unsplash.com/8QJSi37vhms/600x400"
        width="600"
        height="400"
        layout="responsive"
      ></amp-img>
    </amp-base-carousel>
    <button on="tap:hello.hide">Goodbye AMPHTML World!</button>
    <button on="tap:hello.show">hello AMPHTML World!</button>
    <!-- <ul id="example-1">
      <li v-for="item in this.countries" :key="item.name">
        {{ item.name }}
      </li>
    </ul> -->
  <!-- <amp-state id="countries">
    <script type="application/json">
       {{this.countries}}
    </script>
  </amp-state>
  <amp-list
  width="auto"
  height="100"
  layout="fixed-height"
  src="amp-state:countries">
  <template type="amp-mustache">
  <div>
    <div class="item">{{item}}</div>
    <div class="name">{{name}}</div>
  </div>
</template>
</amp-list> -->
</div>
</template>
<script>
const axios = require("axios");
export default {
  data() {
    return {
      countries: [],
    };
  },
  metaInfo: {
    title: "Vue SSR Boilerplate",
    meta: [{ name: "description", content: "Vue SSR Boilerplate" }],
  },
  methods: {
    getCountries: function () {
      axios({
        method: "post",
        url: "https://countries.trevorblades.com/",
        data: {
          query: 'query{continent(code: "EU"){countries{name emoji emojiU languages{name}}}}',
        },
      })
        .then((res) => {
          this.countries = res.data.data.continent.countries
          /*this.countries.forEach(c => {
            console.log(c['name'])
          }); */
          /*   console.log(this.countries) */
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },

  created() {
    this.getCountries();
  },
};
</script>
<style scoped>
h1 {
  margin: 1rem;
}
</style>