<template>
  <div>
    <div class="page__top"></div>
    <section class="result" id="result">
      <div class="container">
        <div class="title" data-aos="fade-up">{{ api.result.title }}</div>

        <div class="row">
          <div
            class="col-lg-3 col-sm-6"
            v-for="(item, idx) in api.result.list"
            :key="idx"
            data-aos="flip-left"
            :data-aos-delay="200"
          >
            <div class="result__title" v-html="item.title"></div>
            <p>
              {{ item.text }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <section class="speaker">
      <div class="container">
        <div class="title" data-aos="fade-up">{{ api.speakers.title }}</div>

        <div class="row">
          <div
            class="col-lg-3 col-sm-6"
            v-for="(speaker, idx) in api.speakers.list"
            :key="idx"
            data-aos="flip-left"
            :data-aos-delay="200"
          >
            <div class="speaker__item">
              <div class="speaker__item-img" v-if="speaker.img">
                <img
                  :src="require(`@/assets/images/speakers/${speaker.img}.jpg`)"
                  alt
                />
              </div>
              <strong>{{ speaker.name }}</strong>
              <div class="speaker__info">
                <p>{{ speaker.position }}</p>
              </div>
            </div>
          </div>
        </div>
        <a
          href="#"
          v-if="showAll"
          @click.prevent="allSpeaker()"
          class="speaker__all"
        >
          {{ api.speakers.btn }}
        </a>
      </div>
    </section>
  </div>
</template>

<script>
import AOS from "aos";
import API from "../static/API";

export default {
  data() {
    return {
      showAll: true,
    };
  },
  computed: {
    api() {
      const lang = this.$store.state.curLang;
      return API[lang];
    },
  },
  methods: {
    allSpeaker() {
      this.showAll = false;
      this.api.speakers.list.push(...this.api.speakers.all);
    },
  },
  created() {
    AOS.init({
      duration: 600,
      disable: "mobile",
      // once: true,
    });
  },
  watch: {
    api() {
      this.showAll = true;
    },
  },
};
</script>

<style>
</style>