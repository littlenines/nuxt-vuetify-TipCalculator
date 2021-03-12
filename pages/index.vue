<template>
  <v-app>
    <v-card class='centered mt-auto mb-auto' max-width='336'>
      <v-img
        dark
        height='50'
        src='https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg'
      >
        <v-row align='center' justify='center'>
          <v-col cols='12'>
            <h1 class='font-weight-thin tekst'>Tip Calculator</h1>
          </v-col>
        </v-row>
      </v-img>
      <v-form ref='form' v-model='valid' class='px-5 py-5' lazy-validation>
        <v-text-field
          v-model='bill'
          :rules='billRules'
          color='purple darken-2'
          label='How much was your bill?'
          placeholder='$'
          required
        ></v-text-field>

        <v-text-field
          v-model='sharing'
          :rules='shareRules'
          label='How many people are sharing the bill?'
          required
        ></v-text-field>

        <v-select
          v-model='select'
          :items='items'
          :rules="[(v) => !!v || 'Service is required']"
          item-text='itemtext'
          item-value='value'
          label='How was your service?'
          required
        ></v-select>

        <v-btn
          :disabled='!valid'
          color='success'
          class='mr-4'
          @click='validate'
        >
          Validate
        </v-btn>

        <v-btn color='error' class='mr-4' @click='reset'> Reset Form </v-btn>
      </v-form>
    </v-card>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    bill: '',
    billRules: [(v) => !!v || 'Bill is required'],
    sharing: '',
    shareRules: [(v) => !!v || 'Sharing is required'],
    items: [
      { value: 0.3, itemtext: '30% - Outstanding' },
      { value: 0.2, itemtext: '20% - Good' },
      { value: 0.15, itemtext: '15% - It was Ok' },
      { value: 0.1, itemtext: '10% - Bad' },
      { value: 0.05, itemtext: '5% - Terrible' },
    ],
    select: null,
  }),

  methods: {
    validate() {
      let total = (this.bill * this.select) / this.sharing
      total = Math.round(total * 100) / 100
      total = total.toFixed(2)
      alert(total + '$')
    },
    reset() {
      this.$refs.form.reset()
    },
  },
}
</script>

<style>
.centered {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.tekst {
  text-align: center;
}
</style>
