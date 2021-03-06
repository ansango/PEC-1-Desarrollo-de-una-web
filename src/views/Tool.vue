<template>
  <div id="tool">
    <section id="hero" class="section hero has-text-centered">
      <div class="hero-body">
        <div class="container head-subsection">
          <img id="tool" :src="tool.image" :alt="tool.name" />
          <h2 class="title is-2 text-secondary is-size-4-mobile">{{tool.name}}</h2>
        </div>
      </div>
    </section>
    <section class="section" v-for="content in tool.text" :key="content.id">
      <div class="container sub-section">
        <h3 class="title is-spaced is-4 text-secondary content-title">{{content.title}}</h3>
        <p class="subtitle is-5 text-secondary">{{content.paragraph1}}</p>
        <p class="subtitle is-5 text-secondary">{{content.paragraph2}}</p>
        <p class="subtitle is-5 text-secondary">{{content.paragraph3}}</p>
      </div>
    </section>

    <section class="section" v-if="tool.options !== undefined">
      <div class="container sub-section-tool" v-for="option in tool.options" :key="option.name">
        <h4 class="title is-spaced is-5 text-secondary content-title">{{option.name}}</h4>
        <p class="subtitle is-5 text-secondary content-paragraph">{{option.description}}</p>
        <a
          :href="option.link"
          target="_blank"
          class="btn violet-bg-primary link subtitle is-6 text-primary"
        >link</a>
      </div>
    </section>

    <section class="section">
      <div class="container sub-section">
        <div class="wrapper-video has-text-centered">
          <button class="btn violet-bg-primary" @click="isOpen = true">Curso de {{tool.name}}</button>
        </div>
      </div>
    </section>

    <div class="modal" :class="{'is-active' : isOpen}">
      <div class="modal-background" @click="isOpen = false"></div>
      <div class="modal-content">
        <figure class="image is-16by9">
          <iframe
            v-if="isOpen === true"
            class="has-ratio"
            :src="tool.video"
            frameborder="0"
            allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </figure>
      </div>
      <button class="modal-close is-large" @click="isOpen = false"></button>
    </div>
  </div>
</template>

<script>
import store from "../store/index.js";
export default {
  name: "Tool",
  data() {
    return {
      isOpen: false
    };
  },
  props: {
    slug: {
      type: String,
      required: true
    },
    toolSlug: {
      type: String,
      required: true
    }
  },
  computed: {
    road() {
      return store.roadmap.find(road => road.slug === this.slug);
    },
    tool() {
      return this.road.tools.find(tool => tool.slug === this.toolSlug);
    }
  }
};
</script>

<style scoped>
.hero .hero-body {
  max-width: 100%;
  margin: 0 auto;
  width: 1200px;
}
.section .container {
  width: 1200px;
  max-width: 100%;
  margin: 0 auto;
}

.sub-section {
  width: 768px !important;
}

.head-subsection {
  display: flex;
  align-items: center;
  justify-content: center;
}

.head-subsection img {
  width: 250px;
}

@media (max-width: 568px) {
  .head-subsection img {
    width: 150px;
  }
}

@media (max-width: 360px) {
  .head-subsection img {
    width: 100px;
  }
}

.head-subsection img,
h2 {
  padding: 20px;
}

.sub-section-tool {
  width: 768px !important;
  padding: 30px 0;
}

.title-hero {
  padding-bottom: 20px;
}

.content-title {
  font-weight: bold;
}

.content-paragraph {
  padding: 20px 0;
}

.wrapper-video {
  padding: 50px;
}

.link {
  width: 100px;
  text-align: center;
  text-transform: capitalize;
  color: white;
}

@media (min-width: 768px) {
  .hero .hero-body .container {
    width: 70%;
  }
}
</style>