<template>
  <div>
    <div class="q-pa-md">
      <q-carousel
        swipeable
        animated
        autoplay
        v-model="slide"
        thumbnails
        infinite
      >
        <q-carousel-slide :name="1" img-src="~assets/1.jpg" />
        <q-carousel-slide :name="2" img-src="~assets/2.jpg" />
        <q-carousel-slide :name="3" img-src="~assets/3.jpg" />
        <q-carousel-slide :name="4" img-src="~assets/4.jpg" />
      </q-carousel>
    </div>

    <div class="q-pa-md">
      <q-card class="my-card q-pa-md">
        <q-card-section class="bg-primary text-white">
          <span class="text-center"
            ><b>UNSURE WHICH VEHICLE YOU ARE LOOKING FOR? FIND IT HERE</b></span
          >
        </q-card-section>
        <q-separator />
        <q-card-section>
          <div class="row justify-center q-pa-md">
            <div class="col-12 col-md-2 q-pa-md">
              <q-card class="my-card">
                <q-card-section>
                  <q-img src="~assets/pickUp.svg" />
                </q-card-section>
              </q-card>
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-card class="my-card">
                <q-card-section>
                  <q-img src="~assets/SUV.svg" />
                </q-card-section>
              </q-card>
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-card class="my-card">
                <q-card-section>
                  <q-img src="~assets/Coupe.svg" />
                </q-card-section>
              </q-card>
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-card class="my-card">
                <q-card-section>
                  <q-img src="~assets/convertable.svg" />
                </q-card-section>
              </q-card>
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-card class="my-card">
                <q-card-section>
                  <q-img src="~assets/sedan.svg" />
                </q-card-section>
              </q-card>
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-card class="my-card">
                <q-card-section>
                  <q-img src="~assets/miniCar.svg" />
                </q-card-section>
              </q-card>
            </div>
          </div>

          <div class="row justify-center q-pa-md">
            <div class="col-12 col-md-2 q-pa-md">
              <q-select
                rounded
                outlined
                v-model="form.make"
                :options="makeOptions"
                label="Any Make"
              />
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-select
                rounded
                outlined
                v-model="form.make"
                :options="makeOptions"
                label="Any Model"
              />
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-select
                rounded
                outlined
                v-model="form.make"
                :options="makeOptions"
                label="Vehicle Status"
              />
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-select
                rounded
                outlined
                v-model="form.make"
                :options="makeOptions"
                label="Min Year"
              />
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              <q-select
                rounded
                outlined
                v-model="form.make"
                :options="makeOptions"
                label="Max Year"
              />
            </div>
          </div>

          <div class="row justify-center q-pa-md">
            <div class="col-12 col-md-2 q-pa-md">
              Price Range
              <q-range v-model="price" :min="0" :max="10000" :step="2" label />
            </div>
            <div class="col-12 col-md-2 q-pa-md">
              Vehicle Mileage Range
              <q-range
                v-model="milage"
                :min="0"
                :max="3000"
                :step="2000"
                label
              />
            </div>
            <div class="col-12 col-md-4 q-pa-md">
              <q-btn
                class="full-width q-pa-md"
                rounded
                color="primary"
                text-color="white"
                label="SEARCH"
              />
            </div>
          </div>
        </q-card-section>
      </q-card>
    </div>

    <div class="q-pa-md">
      <div class="row q-col-gutter-x-xs q-col-gutter-y">
        <div class="col-12 col-md-4 q-pa-md" v-for="car in data" :key="car.id">
          <q-card class="my-card">
            <q-card-section>
              <div class="text-h6 q-mb-xs">
                <strong> {{ car.vehicle_name }} </strong>
              </div>
              <div class="row no-wrap items-center">
                <!-- <q-rating size="18px" v-model="stars" :max="5" color="primary" /> -->
                <span class="text-caption text-grey q-ml-sm"
                  ><b>{{ car.start_code }}</b></span
                >
              </div>
            </q-card-section>
            <q-card-section horizontal>
              <q-img
                :src="car.images[0]"
                @click="selected(car.id)"
                v-ripple
                class="cursor-pointer relative-position"
              >
                <template v-slot:loading>
                  <div class="text-yellow">
                    <q-spinner-ios />
                    <div class="q-mt-md">Loading...</div>
                  </div>
                </template>
                <div class="absolute-bottom text-subtitle2 text-center">
                  <strong
                    >Current
                    {{
                      new Intl.NumberFormat("us-US", {
                        style: "currency",
                        currency: "USD"
                      }).format(car.buy_it_now)
                    }}
                  </strong>
                </div>
              </q-img>

              <q-card-actions vertical class="justify-around">
                <q-btn flat round color="red" icon="favorite" />
                <q-btn flat round color="primary" icon="share" />
              </q-card-actions>
            </q-card-section>
          </q-card>
        </div>
      </div>
    </div>

    <div class="q-pa-md">
      <div class="row justify-center q-pa-md">
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/bmw.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/audi.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/chevrolet.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/honda.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/dodge.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/nissan.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/toyota.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/jeep.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/subaru.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/volkswagen.png" spinner-color="white" />
        </div>
        <div class="col-8 col-md-2 q-pa-md">
          <q-img src="~assets/tesla.png" spinner-color="white" />
        </div>
      </div>
    </div>

    <q-dialog v-model="view_details_modal">
      <q-card style="width: 80%">
         <q-card-section>
          <div class="q-pa-md">
            <q-carousel
                animated
                v-model="slide_1"
                navigation
                infinite
                arrows
                transition-prev="slide-right"
                transition-next="slide-left"
                @mouseenter="autoplay = false"
                @mouseleave="autoplay = true"
              >
                <q-carousel-slide
                  v-for="image in view_selected_lot.images"
                  spinner-color="white"
                  :key="image"
                  :name="image"
                  :img-src="image"
                ></q-carousel-slide>
              </q-carousel>
          </div>
        </q-card-section>
       <q-card-section>
         
       </q-card-section>
        
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      slide: 1,
      slide_1: 1,
      form: {},
      data: [],
      view_selected: [],
      autoplay: true,
      view_selected_lot: {},
      makeOptions: [],
      view_details_modal: false,
      price: {
        min: 0,
        max: 10000
      },
      milage: {
        min: 0,
        max: 3000
      }
    };
  },

  methods: {
    loading_cars() {
      axios
        .get(
          "https://www.salvagebid.com/rest-api/v1.0/lots/search?page=1&per_page=10&type=car&make=*&model=*&search_id=&search_query=&year_from=2008&year_to=2021&sort_field=&sort_order=&sales_type=*&distance=*&destination_zip=&location_state=*&location_city=*&primary_damage=normal+wear+%26+tear&loss_type=*&title_name=*&exterior_color=*&odometer_min=*&odometer_max=*"
        )
        .then(response => {
          this.data = response.data.lots;
        });
    },

    selected(id) {
      console.log(id);
      axios
        .get("https://www.salvagebid.com/rest-api/v2/lots/" + id)
        .then(response => {
          this.view_selected = response.data;
          this.view_selected_lot = response.data.lot;
          this.view_details_modal = true;
        });
    }
  },

  mounted() {
    this.loading_cars();
  }
};
</script>

<style lang="sass" scoped>
.my-content > div
  padding: 10px 15px
  background: rgba(86,61,124,.15)
  border: 1px solid rgba(86,61,124,.2)
  margin-top: 1rem

.shadow-box
  width: 90px
  height: 90px
  margin: 25px
  border-radius: 50%
  font-size: 12px
</style>
