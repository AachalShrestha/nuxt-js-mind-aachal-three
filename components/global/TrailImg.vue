<template>
    <div class="content">
      <img
        v-for="(image, index) in images"
        :key="index"
        class="content__img"
        :src="image"
      />
    </div>
  </template>
  
  
  <script setup>
  import { ref, onMounted } from "vue";
  import gsap from "gsap";
  
  // Helper functions
  const MathUtils = {
    lerp: (a, b, n) => (1 - n) * a + n * b,
    distance: (x1, y1, x2, y2) => Math.hypot(x2 - x1, y2 - y1),
  };
  
  // Mouse position tracking
  const mousePos = ref({ x: 0, y: 0 });
  let lastMousePos = { x: 0, y: 0 };
  let cacheMousePos = { x: 0, y: 0 };
  
  const updateMousePos = (event) => {
    mousePos.value.x = event.clientX;
    mousePos.value.y = event.clientY;
  };
  

  //IMAGES ARRAY
  const images = ref([]);

  // Dynamically populate the array with image paths
  for (let i = 1; i <= 12; i++) {
    images.value.push(`/img/trail-img/trail-img${i}.png`);
  }
  // GSAP Animations
  class ImageTrail {
    constructor(images) {
        this.images = Array.from(images).map((img) => ({
        el: img,
        rect: img.getBoundingClientRect(),
    }));
      this.zIndexVal = -1;
      this.threshold = 100;
      this.imgPosition = 0;
      this.render();
    }
  
    render() {
      const distance = MathUtils.distance(
        mousePos.value.x,
        mousePos.value.y,
        lastMousePos.x,
        lastMousePos.y
      );
  
      cacheMousePos.x = MathUtils.lerp(cacheMousePos.x, mousePos.value.x, 0.1);
      cacheMousePos.y = MathUtils.lerp(cacheMousePos.y, mousePos.value.y, 0.1);
  
      if (distance > this.threshold) {
        this.showNextImage();
        this.zIndexVal++;
        this.imgPosition =
          this.imgPosition < this.images.length - 1 ? this.imgPosition + 1 : 0;
        lastMousePos = { ...mousePos.value };
      }
  
      requestAnimationFrame(() => this.render());
    }
  
    showNextImage() {
      const img = this.images[this.imgPosition];
      gsap.killTweensOf(img.el);
  
      gsap.timeline()
        .set(img.el, {
          opacity: 1,
          scale: 1,
          zIndex: this.zIndexVal,
          x: cacheMousePos.x - img.rect.width / 2,
          y: cacheMousePos.y - img.rect.height / 2,
        })
        .to(img.el, {
          duration: 0.9,
          ease: "expo.out",
          x: mousePos.value.x - img.rect.width / 2,
          y: mousePos.value.y - img.rect.height / 2,
        })
        .to(
          img.el,
          {
            duration: 1,
            ease: "power1.out",
            opacity: 0,
          },
          0.4
        )
        .to(
          img.el,
          {
            duration: 1,
            ease: "quint.out",
            scale: 0.2,
          },
          0.4
        );
    }
  }
  
  // Lifecycle
  onMounted(() => {
    window.addEventListener("mousemove", updateMousePos);
  
    const imgElements = document.querySelectorAll(".content__img");
    const trail = new ImageTrail(imgElements);
  });
  </script>
  
  
  
  <style>
.content {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: -100;
}

.content__title {
  font-family: "Arial", sans-serif;
  text-transform: uppercase;
  z-index: 10000;
  font-size: 4vw;
}

.content__img {
  max-height: 150px;
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
}

@media (min-width: 768) {
  body {
    overflow: hidden;
  }
  .content {
    overflow: hidden;
  }
  .content__img {
  max-height: 200px;
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
}
}

@media (min-width: 1024) {
  body {
    overflow: hidden;
  }
  .content {
    overflow: hidden;
  }
  .content__img {
  max-height: 150px;
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
}
}

  </style>
  