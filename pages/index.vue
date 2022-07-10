<template>
<div class="container p-4">
    <h3>Filters</h3>
  <p class="text-info">Shapes</p>
  <div class="d-flex">
    <div v-for="shape in shapes" class="mr-2">
      <button class="btn btn-xs grey rounded-pill f-10 mb-2" @click="selectShape(shape)" :class="selectedShape.includes(shape) ? 'bg-dark text-white' : ''">
          {{shape}}
      </button>
    </div>
  </div>
  <div>
    <p class="text-info mt-4">Colors</p>
    <div class="d-flex mb-4">
        <div v-for="(color, index) in colors" :key="index" class="mr-2">
          <button class="btn btn-xs rounded-circle mb-2 p-2 shadow" :class="selectedColor.includes(color) ? 'border-8 border-dark' : ''" :style="'background-color:' + color" @click="selectColor(color)">
            </button>
        </div>
    </div>
  </div>
    <div class="filter">
       <h6>{{filterTitle}}</h6>
        <div class="d-flex align-content-start flex-row flex-wrap">
        <div v-for="shape in allShapes">
          <div v-for="color in allColors">
              <div class="bg-white mb-4 shadow p-4 mr-4">
                <div class="mx-auto" :class="shape" v-if="shape === 'Triangle'" :style="'border-bottom: 50px solid ' + color"></div>
                <div class="mx-auto" :class="shape" v-else :style="'background-color:' + color"></div>
              </div>
          </div>
        </div>
      </div>
    </div>
    <!-- <div v-else>
         <div class="bg-white mb-4 shadow p-4 w-25">
            <div class="mx-auto" :class="selectedShape" v-if="selectedShape === 'Triangle'" :style="'border-bottom: 50px solid ' + selectedColor"></div>
            <div class="mx-auto" :class="selectedShape" v-else :style="'background-color:' + selectedColor"></div>
          </div>
    </div> -->
</div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
       "shapes": ["Oval", "Round", "Triangle", "Square", "Rectangle"],
       "colors": [
        "red",
        "blue",
        "green",
        "yellow",
        "lightblue",
        "grey"
       ],
       "selectedShape": [],
      "selectedColor": []

    }
  },
  computed: {
    allShapes() {

      if (this.selectedShape.length == 0) {
        return this.shapes;
      }

      return this.selectedShape
    },

    allColors() {
      console.log('ues')
      if (this.selectedColor.length == 0) {
        return this.colors;
      }
      return this.selectedColor;
    },

    filterTitle() {
        if ((this.allShapes.length === this.shapes.length) && (this.allColors.length === this.colors.length)) {
          return 'All Items: ' + (this.colors.length * this.shapes.length);
        }

        if ((this.allColors.length === this.colors.length) && (this.allShapes.length === 1)) {
          return 'All ' + this.allShapes[0] + ' items: ' + Object.keys(this.allColors).length;
        }

        if (this.allShapes.length === this.shapes.length && (this.allColors.length == 1 )) {
          return 'All ' + this.allColors[0] + ' items: ' + this.allShapes.length;
        }

        if ((this.allShapes.length === this.shapes.length && (this.allColors.length > 1 )) || (this.allColors.length === this.colors.length && (this.allShapes.length > 1 ))) {
          return 'Multiple items: ' + (this.allShapes.length * this.allColors.length);
        }

        if (this.allShapes.length > 1 && this.allColors.length == 1) {
          return 'Multiple ' +  this.allColors[0] + ' items: ' + this.allShapes.length;
        }

        if (this.allColors.length > 1 && this.allShapes.length == 1) {
          return 'Multiple ' +  this.allShapes[0] + ' items: ' + this.allColors.length;
        }

        if (this.allColors.length == 1 && this.allShapes.length == 1) {
          return this.allShapes[0] + ' ' + this.allColors[0] + ' item: ' + this.allColors.length;
        }
    },
  },
  methods: {
    selectShape(shape) {
      if (this.selectedShape.includes(shape)) {
        this.selectedShape = this.selectedShape.filter(s => s !== shape);
      } else {
        this.selectedShape.push(shape);
      }
    },

    selectColor(color) {
      if (this.selectedColor.includes(color)) {
         this.selectedColor = this.selectedColor.filter(c => c !== color);
      } else {
        this.selectedColor.push(color);
      }
    }
  }
}
</script>
<style>
  .f-10 {
    font-size: 10px;
  }

  .grey {
    background-color: #e3e3e3;
  }

  .w-30 {
    width: 40%;
  }

  .p-custom {
    padding: 25%;
  }

  .Rectangle {
    height: 50px;
    width: 100px;
  }

  .Oval {
    height: 50px;
    width: 100px;
    border-radius: 50%;
  }

  .Round {
    height: 50px;
    width: 50px;
    border-radius: 50%;
  }

  .Triangle {
    width: 0;
    height: 0;
    border-left: 25px solid transparent;
    border-right: 25px solid transparent;
  }

  .Square {
    height: 50px;
    width: 50px;
  }
</style>
