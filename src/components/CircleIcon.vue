<template>
  <div class="ellipse">
        <BaseIcon
          @click="addData(2)"
          @mouseover="addHovering(3)"
          @mouseleave="addHovering(0)"
          :class="{'ellipseHover' : hoveringItem === 3}"
          class="ellipse__pulsar ellipse__color"
          href="#pulsar"
        />
        <BaseIcon
          @click="addData(4)"
          @mouseover="addHovering(4)"
          @mouseleave="addHovering(0)"
          :class="{'ellipseHover' : hoveringItem === 4}"
          class="ellipse__waveForm ellipse__color"
          href="#waves"
        />
        <BaseIcon
          @click="addData(5)"
          @mouseover="addHovering(6)"
          @mouseleave="addHovering(0)"
          :class="{'ellipseHover' : hoveringItem === 6}"
          class="ellipse__hydrogen ellipse__color"
          href="#hydrogen"
        />
        <BaseIcon
          @click="addData(3)"
          @mouseover="addHovering(5)"
          @mouseleave="addHovering(0)"
          :class="{'ellipseHover' : hoveringItem === 5}"
          class="ellipse__frames ellipse__color"
          href="#frames"
        />
        <BaseIcon
          @click="addData(1)"
          @mouseover="addHovering(2)"
          @mouseleave="addHovering(0)"
          :class="{'ellipseHover' : hoveringItem === 2}"
          class="ellipse__elevation ellipse__color"
          href="#elevation"
        />
        <BaseIcon
          @click="addData(0)"
          @mouseover="addHovering(1)"
          @mouseleave="addHovering(0)"
          :class="{'ellipseHover' : hoveringItem === 1}"
          class="ellipse__record ellipse__color"
          href="#record"
        />
  </div>
</template>

<script>
import EventBus from '@/EventBus';
import BaseIcon from '@/components/BaseIcon.vue';
import { url } from "@/constants.js";

export default {
  props:{
    hoveringItem:{
      type:Number,
      required: false,
    }
  },
  components:{
    BaseIcon
  },
  methods: {
    addData(i){
      fetch(`${url}/query/how_use`, {
      method: "GET",
    })
    .then(Response => Response.json())
    .then(data => {
      EventBus.$emit("open", {
        component: "BaseModal",
        content:{
            text1 : data[i].text_1,
            text2 : data[i].text_2,
            title : data[i].title,
            symbol: data[i].symbol
        }
      })
    })
    .catch(error => console.log(error))
    },
    addHovering(hoverTest){
      this.$emit('hover', hoverTest)
    }
  },
}
</script>

<style lang="scss">
  .ellipse{ 

    position: relative;
    height: 350px;
    width: 350px;
    border-radius: 50%;
    background: linear-gradient(#d7c37f, #a67a3b);

    @include media_tablet {
      width: 32%;
      height: 40%;
    }

  &__color {
    &:hover {
      stroke: $primary-white;
      filter: drop-shadow(0px 6px 2px rgba($primary-darkblue, 0.7));
    }
  }

  &__pulsar {
    position: absolute;
    top: 50%;
    left: 15%;
    width: 150px;
    height: 150px;
    stroke: $primary-darkblue;
    fill: none;

    @include media_tablet {
      width: 120px;
      height: 120px;
    }
  }

  &__waveForm {
    position: absolute;
    top: 15%;
    right: 20%;
    width: 120px;
    height: 80px;
    stroke: $primary-darkblue;
    fill: none;

    @include media_tablet {
      width: 80px;
      height: 70px;
    }
  }

  &__hydrogen {
    position: absolute;
    top: 70%;
    right: 20%;
    width: 80px;
    height: 80px;
    stroke: $primary-darkblue;
    fill: none;

    @include media_tablet {
      width: 50px;
      height: 50px;
    }
  }

  &__frames {
    position: absolute;
    top: 40%;
    right: 20%;
    width: 80px;
    height: 80px;
    stroke: $primary-darkblue;
    fill: none;

    @include media_tablet {
      width: 60px;
      height: 60px;
    }
  }

  &__elevation {
    position: absolute;
    top: 35%;
    left: 15%;
    width: 80px;
    height: 80px;
    stroke: $primary-darkblue;
    fill: none;

    @include media_tablet {
      width: 60px;
      height: 60px;
    }
  }

  &__record {
    position: absolute;
    top: 15%;
    left: 15%;
    width: 80px;
    height: 80px;
    stroke: $primary-darkblue;
    fill: none;

    @include media_tablet {
      width: 60px;
      height: 60px;
    }
  }

  .ellipseHover{
    stroke: $primary-white;
    filter: drop-shadow(0px 6px 2px rgba($primary-darkblue, 0.7));
    cursor: pointer;
  }
} 
</style>