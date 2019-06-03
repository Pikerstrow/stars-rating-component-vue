<template>
  <div class="stars-container" :style="{height: options.size + 'px', width: 'fit-content'}">
    <div v-if="options.readOnly" class="conditional-stars-container" style="cursor: auto">
      <div
        v-for="(val, index) in available_values"
        :key="index"
        class="star-container"
        :style="{width: options.size + 'px', height: options.height + 'px', marginRight: options.marginRight + 'px'}"
      >
        <svg
          class="star-svg full-star"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 100 100"
          :style="{width: options.size + 'px', height: options.height + 'px'}"
        >
          <path
            :rating="val[1]"
            class="widget-rating-star"
            :stroke="options.stroke"
            :fill="options.fill"
            :stroke-width="options.strokeWidth + 'px'"
            d="M50 0 l-15 35 -35 5 25 24 -6 35 31 -18 31 18 -6 -35 25 -24 -35 -5 -15 -35 z"
          ></path>
        </svg>
        <svg
          class="star-svg half-star"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 50 100"
          :style="{width: (options.size / 2) + 'px', height: options.height + 'px'}"
        >
          <path
            :rating="val[0]"
            class="widget-rating-star"
            :stroke="options.stroke"
            :fill="options.fill"
            :stroke-width="options.strokeWidth + 'px'"
            d="M50 0 l-15 35 -35 5 25 24 -6 35 31 -18"
          ></path>
        </svg>
      </div>
    </div>

    <div v-else class="conditional-stars-container" style="cursor: pointer">
      <div
        v-for="(val, index) in available_values"
        :key="index"
        @mouseleave="removeHoverEffect"
        class="star-container"
        :style="{width: options.size + 'px', height: options.height + 'px', marginRight: options.marginRight + 'px'}"
      >
        <svg
          @click="setRating(val[1])"
          @mouseenter="hoverEffect(val[1])"
          class="star-svg full-star"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 100 100"
          :style="{width: options.size + 'px', height: options.height + 'px'}"
        >
          <path
            :rating="val[1]"
            class="widget-rating-star"
            :stroke="options.stroke"
            :fill="options.fill"
            :stroke-width="options.strokeWidth + 'px'"
            d="M50 0 l-15 35 -35 5 25 24 -6 35 31 -18 31 18 -6 -35 25 -24 -35 -5 -15 -35 z"
          ></path>
          <title>{{ val[1] }}</title>
        </svg>
        <svg
          @click="setRating(val[0])"
          @mouseenter="hoverEffect(val[0])"
          class="star-svg half-star"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 50 100"
          :style="{width: (options.size / 2) + 'px', height: options.height + 'px'}"
        >
          <path
            :rating="val[0]"
            class="widget-rating-star"
            :stroke="options.stroke"
            :fill="options.fill"
            :stroke-width="options.strokeWidth + 'px'"
            d="M50 0 l-15 35 -35 5 25 24 -6 35 31 -18"
          ></path>
          <title>{{ val[0] }}</title>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StarsReviews",
  props: {
    value: {
      default: null
    },
    options: {
      type: Object,
      required: false,
      validator: function(options) {
        if ("fill" in options) {
          if (typeof options.fill !== "string") {
            console.error(
              "[Stars widget warn]: 'fill' property expected as a string with valid CSS-color. " +
                typeof options.fill +
                " given."
            );
          }
          options.fill = options.fill;
        } else {
          options.fill = "#DDD";
        }

        if ("stroke" in options) {
          if (typeof options.stroke !== "string") {
            console.error(
              "[Stars widget warn]: 'stroke' property expected as a string with valid CSS-color. " +
                typeof options.stroke +
                " given."
            );
          }
          options.stroke = options.stroke;
        } else {
          options.stroke = "none";
        }

        if ("strokeWidth" in options) {
          if (typeof options.strokeWidth !== "number") {
            console.error(
              "[Stars widget warn]: 'strokeWidth' property expected as an integer. " +
                typeof options.strokeWidth +
                " given."
            );
          }
          options.strokeWidth = options.strokeWidth;
        } else {
          options.strokeWidth = 0;
        }

        if ("highlighted" in options) {
          if (typeof options.highlighted !== "string") {
            console.error(
              "[Stars widget warn]: 'highlighted' property expected as a string with valid CSS-color. " +
                typeof options.highlighted +
                " given."
            );
          }
          options.highlighted = options.highlighted;
        } else {
          options.highlighted = "#FFDF12";
        }

        if ("hover" in options) {
          if (typeof options.hover !== "string") {
            console.error(
              "[Stars widget warn]: 'hover' property expected as a string with valid CSS-color. " +
                typeof options.hover +
                " given."
            );
          }
          options.hover = options.hover;
        } else {
          options.hover = "#FFED84";
        }

        if ("size" in options) {
          if (typeof options.size !== "number") {
            console.error(
              "[Stars widget warn]: 'size' property expected as an integer (number). " +
                typeof options.size +
                " given."
            );
          }
          options.size = options.size;
        } else {
          options.size = 25;
        }

        if ("marginRight" in options) {
          if (typeof options.marginRight !== "number") {
            console.error(
              "[Stars widget warn]: 'marginRight' property expected as an integer (number). " +
                typeof options.marginRight +
                " given."
            );
          }
          options.marginRight = options.marginRight;
        } else {
          options.marginRight = 3;
        }

        if ("readOnly" in options) {
          if (typeof options.readOnly !== "boolean") {
            console.error(
              "[Stars widget warn]: 'readOnly' property expected as a boolean. " +
                typeof options.readOnly +
                " given."
            );
          }
          options.readOnly = options.readOnly;
        } else {
          options.readOnly = false;
        }

        if ("rating" in options) {
          if (typeof options.rating !== "number") {
            console.error(
              "[Stars widget warn]: 'rating' property expected as a number. " +
                typeof options.rating +
                " given."
            );
          }
          options.rating = options.rating;
        } else {
          options.rating = 0;
        }

        if ("starsQuantity" in options) {
          if (typeof options.starsQuantity !== "number") {
            console.error(
              "[Stars widget warn]: 'v' property expected as a number. " +
                typeof options.starsQuantity +
                " given."
            );
          }
          options.starsQuantity = options.starsQuantity;
        } else {
          options.starsQuantity = 5;
        }

        return options;
      },
      default: function() {
        return {
          starsQuantity: 5,
          stroke: "none",
          strokeWidth: 0,
          fill: "#DDD",
          highlighted: "#FFDF12",
          hover: "#FFED84",
          size: 25,
          readOnly: false,
          rating: 0,
          marginRight: 5
        };
      }
    }
  },
  data() {
    return {
      selectedRating: null,
      stars: null,
      ratingSet: false,
      available_values: []
    };
  },
  methods: {
    setRating(value) {
      /*Set colored background for stars before selected one*/
      for (let i = 0; i < this.stars.length; i++) {
        if (value >= parseFloat(this.stars[i].getAttribute("data-rating"))) {
          this.stars[i].setAttribute("fill", this.options.highlighted);
        } else {
          this.stars[i].setAttribute("fill", this.options.fill);
        }
      }
      this.ratingSet = true;
      this.selectedRating = value;
      this.$emit("input", value);
    },
    hoverEffect(value) {
      for (let i = 0; i < this.stars.length; i++) {
        if (parseFloat(this.stars[i].getAttribute("data-rating")) <= value) {
          this.stars[i].setAttribute("fill", this.options.hover);
        } else {
          /*Check if rating was set, and if it was - we need to highlight stars according to proper color*/
          if (
            this.ratingSet &&
            parseFloat(this.stars[i].getAttribute("data-rating")) <=
              this.selectedRating
          ) {
            this.stars[i].setAttribute("fill", this.options.highlighted);
          } else {
            this.stars[i].setAttribute("fill", this.options.fill);
          }
        }
      }
    },
    removeHoverEffect() {
      for (let i = 0; i < this.stars.length; i++) {
        /*If rating is set we need to left proper color for selected stars*/
        if (
          this.ratingSet &&
          parseFloat(this.stars[i].getAttribute("data-rating")) <=
            this.selectedRating
        ) {
          this.stars[i].setAttribute("fill", this.options.highlighted);
        } else {
          this.stars[i].setAttribute("fill", this.options.fill);
        }
      }
    }
  },
  beforeMount() {
    /*Defining available values according to stars quantity from options.*/
    for (let i = 1; i <= this.options.starsQuantity; i++) {
      let starValues = [];
      starValues.push(i - 0.5);
      starValues.push(i);
      this.available_values.push(starValues);
    }
  },
  mounted() {
    this.rating = this.value;

    /*Gathering all stars*/
    let stars = document.getElementsByClassName("widget-rating-star");
    this.stars = stars;

    /*If is set readOnly property - we need to highlight stars with rating*/
    if (this.options.readOnly) {
      for (let i = 0; i < this.stars.length; i++) {
        if (
          parseFloat(this.stars[i].getAttribute("data-rating")) <=
          this.options.rating
        ) {
          this.stars[i].setAttribute("fill", this.options.highlighted);
        }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.stars-container {
  .conditional-stars-container {
    display: flex;
  }
  .star-container {
    position: relative;

    .full-star {
      position: absolute;
      top: 0;
    }
    .half-star {
      position: absolute;
      top: 0;
    }
    path {
      -webkit-transition-duration: 2s;
      -moz-transition-duration: 2s;
      -o-transition-duration: 2s;
      transition-duration: 0.2s;
    }
  }
}
</style>