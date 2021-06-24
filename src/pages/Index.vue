<template>
  <div class="">
    <q-tabs inline-label class="bg-primary text-white shadow-2">
      <q-tab v-on:click="chet" name="chet" class="w-100 mx-2" label="Четная" />
      <q-tab
        v-on:click="nechet"
        name="nechet"
        class="w-100 mx-2"
        label="Нечетная"
      />
    </q-tabs>
    <div class="col w-100 mx-3">
      <q-input bottom-slots v-model="group" label="Группа" maxlength="5">
        <q-btn v-on:click="getPosts" dense flat icon="search" />
      </q-input>
    </div>
    <div class="container-fluid">
      <div class="div">
        <div class="row">
          <div
            v-for="day in week"
            :key="day.week"
            class="col-lg-2 col-md-4 col-sm-6 col-12"
            id=""
            style="padding:0 3px"
          >
            <div v-if="day[0]" class="col-lg-12 dayhead" id="nedelya">
              {{ day[0][0] }}
            </div>
            <div v-for="pair in day" :key="pair.day" class="col-lg-12 day">
              <div>
                <span class="time">{{ pair[2] }}</span>
              </div>
              <div class="less">
                <span class="lesson">{{ pair[1] }}</span>
              </div>
              <div class="text-right">
                <span class="prepod">{{ pair[3] }}</span>
              </div>
              <div class="row">
                <div class="col-lg-3">
                  <span class="aud">{{ pair[4] }}</span>
                </div>
                <div class="col-lg-9 text-right">
                  <span class="type n-type">{{ pair[5] }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PageIndex",
  data() {
    return {
      Url: "http://127.0.0.1:8081/raspisanie/?g=",
      week: [],
      chet_days: [],
      nechet_days: [],
      group: "152"
    };
  },
  methods: {
    getPosts() {
      axios
        .get(this.Url + this.group)
        .then(response => {
          this.chet_days = this.week = response.data[0];
          this.nechet_days = response.data[1];
        })
        .catch(response => {
          console.log(response);
        });
    },
    chet: function(event) {
      this.week = this.chet_days;
    },
    nechet: function(event) {
      this.week = this.nechet_days;
    }
  },
  created() {
    this.getPosts();
  }
};
</script>
