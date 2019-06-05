<template>
  <div class="stars-container" :style="{height: options.size + 'px', width: 'fit-content'}">
    <div v-if="options.readOnly" class="conditional-stars-container" style="cursor: auto">
      <div
        v-for="(val, index) in available_values"
        :key="index"
        class="star-container"
        :style="{width: options.size + 'px', height: options.size + 'px', marginRight: options.marginRight + 'px'}"
      >
        <svg
          class="star-svg full-star"
          xmlns="http://www.w3.org/2000/svg"
          :viewBox="options.viewBox"
          :style="{width: options.size + 'px', height: options.height + 'px'}"
        >
          <path
            :data-rating="val[1]"
            class="widget-rating-star"
            :stroke="options.stroke"
            :fill="options.fill"
            :stroke-width="options.strokeWidth + 'px'"
            :d="options.d"
          ></path>
        </svg>
        <div
          :style="{width: halfStarWidth + 'px', height: options.size + 'px'}"
          class="half-star-container"
        >
          <svg
            class="star-svg full-star"
            xmlns="http://www.w3.org/2000/svg"
            :viewBox="options.viewBox"
            :style="{width: options.size + 'px', height: options.height + 'px'}"
          >
            <path
              :data-rating="val[0]"
              class="widget-rating-star"
              :stroke="options.stroke"
              :fill="options.fill"
              :stroke-width="options.strokeWidth + 'px'"
              :d="options.d"
            ></path>
          </svg>
        </div>
      </div>
    </div>

    <div v-else class="conditional-stars-container" style="cursor: pointer">
      <div
        v-for="(val, index) in available_values"
        :key="index"
        @mouseleave="removeHoverEffect"
        class="star-container"
        :style="{width: options.size + 'px', height: options.size + 'px', marginRight: options.marginRight + 'px'}"
      >
        <svg
          @click="setRating(val[1])"
          @mouseenter="hoverEffect(val[1])"
          class="star-svg full-star"
          xmlns="http://www.w3.org/2000/svg"
          :viewBox="options.viewBox"
          :style="{width: options.size + 'px', height: options.height + 'px'}"
        >
          <path
            :data-rating="val[1]"
            class="widget-rating-star"
            :stroke="options.stroke"
            :fill="options.fill"
            :stroke-width="options.strokeWidth + 'px'"
            :d="options.d"
          ></path>
          <title>{{ val[1] }}</title>
        </svg>
        <div
          :style="{width: halfStarWidth + 'px', height: options.size + 'px'}"
          class="half-star-container"
        >
          <svg
            @click="setRating(val[0])"
            @mouseenter="hoverEffect(val[0])"
            class="star-svg full-star"
            xmlns="http://www.w3.org/2000/svg"
            :viewBox="options.viewBox"
            :style="{width: options.size + 'px', height: options.height + 'px'}"
          >
            <path
              :data-rating="val[0]"
              class="widget-rating-star"
              :stroke="options.stroke"
              :fill="options.fill"
              :stroke-width="options.strokeWidth + 'px'"
              :d="options.d"
            ></path>
          </svg>
        </div>
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
          if (typeof options.fill != "string") {
            console.error(
              "[Star Rating Widget]: Type of 'fill' property must be 'sring'"
            );
          }
        } else {
          options.fill = "#DDD";
        }

        if ("stroke" in options) {
          if (typeof options.stroke !== "string") {
            console.error(
              "[Star Rating Widget]: Type of 'stroke' property must be 'sring'"
            );
          }
        } else {
          options.stroke = "none";
        }

        if ("strokeWidth" in options) {
          if (typeof options.strokeWidth !== "number") {
            console.error(
              "[Star Rating Widget]: Type of 'strokeWidth' property must be 'number'"
            );
          }
        } else {
          options.strokeWidth = 2;
        }

        if ("highlighted" in options) {
          if (typeof options.highlighted !== "string") {
            console.error(
              "[Star Rating Widget]: Type of 'highlighted' property must be 'string'"
            );
          }
        } else {
          options.highlighted = "#FFDF12";
        }

        if ("hover" in options) {
          if (typeof options.hover !== "string") {
            console.error(
              "[Star Rating Widget]: Type of 'hover' property must be 'sring'"
            );
          }
        } else {
          options.hover = "#FFED84";
        }

        if ("size" in options) {
          if (typeof options.size !== "number") {
            console.error(
              "[Star Rating Widget]: Type of 'size' property must be 'number'"
            );
          }
        } else {
          options.size = 25;
        }

        if ("marginRight" in options) {
          if (typeof options.marginRight !== "number") {
            console.error(
              "[Star Rating Widget]: Type of 'marginRight' property must be 'number'"
            );
          }
        } else {
          options.marginRight = 3;
        }

        if ("readOnly" in options) {
          if (typeof options.readOnly !== "boolean") {
            console.error(
              "[Star Rating Widget]: Type of 'readOnly' property must be 'boolean'"
            );
          }
        } else {
          options.readOnly = false;
        }

        if ("rating" in options) {
          if (typeof options.rating !== "number") {
            console.error(
              "[Star Rating Widget]: Type of 'rating' property must be 'number'"
            );
          }
        } else {
          options.rating = 0;
        }

        if ("starsQuantity" in options) {
          if (typeof options.starsQuantity != "number") {
            console.error(
              "[Star Rating Widget]: Type of 'starsQuantity' property must be 'number'"
            );
          }
        } else {
          options.starsQuantity = 10;
        }

        if ("d" in options) {
          if (typeof options.d != "string") {
            console.error(
              "[Star Rating Widget]: Type of 'd' property must be 'sring'"
            );
          }
        } else {
          options.d =
            "M50 0 l-15 35 -35 5 25 24 -6 35 31 -18 31 18 -6 -35 25 -24 -35 -5 -15 -35 z";
        }

        if ("viewBox" in options) {
          if (typeof options.viewBox != "string") {
            console.error(
              "[Star Rating Widget]: Type of 'viewBox' property must be 'sring'"
            );
          }
        } else {
          options.viewBox = "0 0 100 100";
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
          size: 100,
          readOnly: false,
          rating: 0,
          marginRight: 5,
          d:
            "M50 0 l-15 35 -35 5 25 24 -6 35 31 -18 31 18 -6 -35 25 -24 -35 -5 -15 -35 z",
          viewBox: "0 0 100 100"
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
  computed: {
    halfStarWidth() {
      if (this.options.readOnly && parseFloat(this.options.rating) > 0) {
        let rating = parseFloat(this.options.rating);
        let decimal = rating % 1;
        return this.options.size * decimal;
      } else {
        return this.options.size / 2;
      }
    }
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
    for (let i = 1; i <= parseInt(this.options.starsQuantity); i++) {
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
        let starRating = parseFloat(this.stars[i].getAttribute("data-rating"));

        if (starRating <= parseFloat(this.options.rating)) {
          this.stars[i].setAttribute("fill", this.options.highlighted);
        } else if (starRating % 1 !== 0) {
          if (
            starRating - 0.5 <= parseFloat(this.options.rating) &&
            parseFloat(this.options.rating) !== 0
          ) {
            this.stars[i].setAttribute("fill", this.options.highlighted);
          }
        }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.stars-container {
  .half-star-container {
    overflow: hidden;
    margin: 0;
    padding: 0;
    position: absolute;
    top: 0;
  }

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