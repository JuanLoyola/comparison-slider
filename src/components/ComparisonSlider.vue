<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template>
  <div id="app">
    <div class="compare-img-slider" ref="slider">
      <img class="before" src="@/assets/before.jpg" tag="before"/>

      <div class="resizer" :style="`width: ${dragLeft}%;`">
        <img class="after" src="@/assets/after.jpg" tag="after"/>
      </div>

      <div
        class="handler"
        :style="`left: ${dragLeft}%;`"
        @mousedown.stop="onDragStart"
        @mousemove.prevent.stop="onMove"
        @mouseup="onDragStop"
        @mouseleave="onDragStop"
        @touchstart.stop="onDragStart"
        @touchmove.prevent.stop="onMove"
        @touchend="onDragStop"
      >
        <i class="cursor fas fa-arrows-alt-h"></i>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'ComparisonSlider',
  data() {
    return {
      isDragging: false,
      dragLeft: 0,
    };
  },
  methods: {
    getClient(e) {
      if (e.clientX) {
        return { x: e.clientX, y: e.clientY };
      }
      const touch = e.touches?.[0] || {};
      return {
        x: touch.clientX,
        y: touch.clientY
      };
    },

    onDragStart(e) {
      const parentStyle = getComputedStyle(e.target.parentNode);
      this.sliderWidth = this.$refs.slider.offsetWidth;
      this.offsetX = parseInt(parentStyle.left) - this.getClient(e).x;
      this.isDragging = true;
    },

    onMove(e) {
      if (!this.isDragging) return;
      const leftPercent = (this.getClient(e).x + this.offsetX) * 100 / this.sliderWidth;
      if (leftPercent <= 0 || leftPercent >= 100) {
        this.isDragging = false;
        return;
      }
      this.dragLeft = leftPercent;
    },
    onDragStop() {
      this.isDragging = false;
    },
  },
};
</script>

<style lang="scss" scoped>
body {
  margin: 0;
  img {
    display: block;
  }
}

.compare-img-slider {
  position: relative;
  width: 100%;
  user-select: none;
  -webkit-box-shadow: 0px 10px 5px 0px #c0b9c0;
  -moz-box-shadow: 0px 10px 5px 0px #c0b9c0;
  box-shadow: 0px 10px 5px 0px #c0b9c0;
  border-radius: 10px;
  .before {
    width: 100%;
    border-radius: 10px;
  }

  .resizer {
    position: absolute;
    top: 0;
    left: 0;
    width: 50%;
    height: 100%;
    overflow: hidden;

    .after {
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      border-radius: 10px;
    }
  }

  .handler {
    position: absolute;
    top: 0;
    left: 0;
    width: 1px;
    height: 100%;

    .cursor {
      position: absolute;
      display: block;
      top: 50%;
      left: 50%;
      font-size: 3em;
      background: #4e83c9;
      color: #f1f1f1;
      padding: 8px;
      border-radius: 50%;
      transform: translate(-50%, -50%) rotate(360deg);
      transition: transform 0.5s;
      cursor: pointer;

      &:active {
        transform: translate(-50%, -50%) rotate(0deg) scale(0.9);
        color: #afdefa;
        opacity: 0.7;
      }
    }
  }
}

@media screen and (max-width: 1024px) {
  .compare-img-slider {

    .handler {

      .cursor {
        font-size: 2em;

        &:active {
          transform: translate(-50%, -50%) rotate(0deg) scale(1);
        }
      }
    }
  }
}
</style>