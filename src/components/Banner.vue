<template>
  <section class="parallax-container">
    <div class="parallax-bg"></div>
    
    <div v-observe-visibility="onElementObserved" :class="['content', { 'is-visible': visible }]"> <!-- scroll da pagina -->
      <h1>Monte seu Hamburguer</h1>
      <p>A experiência artesanal definitiva.</p>
    </div>
  </section>
</template>

<script>
    export default {
        name : 'Banner',
data() {
    return {
      visible: false
    }
  },
  methods: {
    // ativar a animação Intersection Observer
    onElementObserved() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            this.visible = true;
          }
        });
      }, { threshold: 0.3 }); // Dispara quando 30% do elemento estiver visível
      observer.observe(this.$el);
    }
  },
  mounted() {
    this.onElementObserved();
  }
}
</script>

<style scoped>
   .parallax-container {
  height: 450px;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.parallax-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 120%;
  background-image: url('../assets/img/burger.jpg');
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  z-index: -1;
}

.content {
  text-align: center;
  color: var(--color-p);
  opacity: 0;
  transform: translateY(50px);
  transition: all 2s ease-out;
}

.content.is-visible {
  opacity: 1;
  transform: translateY(0);
}

h1 {
  font-size: 3.5rem;
  text-shadow: 2px 2px 10px rgba(0,0,0,0.5);
}
</style>