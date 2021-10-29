<template>
  <div class="icon-editor">
    <p class="pt-5 px-5">Palette</p>
    <div class="color-palette px-5 pb-5 d-flex">
      <div
        v-for="color in palette"
        :key="color"
        class="tile w-5 h-5"
        :style="{
          'background-color': color,
        }"
      ></div>
    </div>
    <p class="px-5">Input Colors</p>
    <div class="icon-palette px-5 pb-5 d-flex">
      <div
        v-for="color in iconHex"
        :key="color"
        class="tile w-5 h-5"
        :style="{
          'background-color': color,
        }"
      ></div>
    </div>
    <p class="px-5">Output Colors</p>
    <div class="result-palette px-5 pb-5 d-flex">
      <div
        v-for="(color, index) in resultColors"
        :key="`color_${index}_${color}`"
        class="tile w-5 h-5"
        :style="{
          'background-color': `#${color}`,
        }"
      >
        {{ color.h }}
      </div>
    </div>
  </div>
</template>

<script>
const convert = require('color-convert')
export default {
  data() {
    return {
      palette: ['#f4fa9c', '#f369a9', '#ba53de', '#88bef5'],
      iconHex: ['#ff5670', '#aaaaaa', '#11bca2', '#fdb400', '#3c50e0'],
      paletteHSL: [],
      iconHSL: [],
      resultColors: [],
    }
  },

  mounted() {
    this.generatePalette(this.palette, this.iconHex)
  },

  methods: {
    //   To generate colours from Palette
    // paletteColors is an array of colors in hexadecimal format
    // iconColors is an array colors in the icon
    generatePalette(paletteColors, iconColors) {
      // convert paletteColors to {h,s,l}
      paletteColors.forEach((color) => {
        this.paletteHSL.push(this.generateHSLObject(color))
      })

      // convert iconColors to {h,s,l}
      iconColors.forEach((color) => {
        this.iconHSL.push(this.generateHSLObject(color))
      })

      // go through each of the colors from the icon and map the colors from the palette based on the nearest HUE
      // once the number of colors have exceeded more than the palette,
      //  use the nearest HUE and the icon color's and light
      this.iconHSL.forEach((hsl, i) => {
        const minH = this.findHueDifferenceColor(this.paletteHSL, hsl)
        if (i + 1 <= paletteColors.length)
          this.resultColors.push(convert.hsl.hex(minH.h, minH.s, minH.l))
        else this.resultColors.push(convert.hsl.hex(minH.h, hsl.s, hsl.l))
      })

      return this.resultColors
    },

    // convert HEXCODE into H S L object
    // input: (hex<String>)
    // returns: object { h:<Number>, s:<Number>, l:<Number> }
    generateHSLObject(hex) {
      const HSLArray = convert.hex.hsl(hex)
      return {
        h: HSLArray[0],
        s: HSLArray[1],
        l: HSLArray[2],
      }
    },

    // compare the HUE value between EACH COLOR FROM THE PALETTE and ONE COLOR FROM THE ICON
    // to find the nearest HUE from the palette to apply
    // input:(paletteHSL<{h,s,l}[]>, {h,s,l} )
    // returns: {h,s,l} ==> Nearest Palette color to the icon color based on the HUE
    findHueDifferenceColor(paletteHSL, iconColorHSL) {
      let minHue = paletteHSL[0]
      let min = Math.abs(minHue.h - iconColorHSL.h)
      for (let i = 1; i < paletteHSL.length; i++) {
        const diff = Math.abs(paletteHSL[i].h - iconColorHSL.h)
        if (diff < min) {
          min = diff
          minHue = paletteHSL[i]
        }
      }

      return minHue
    },
  },
}
</script>

<style scoped>
.tile {
  width: 40px;
  height: 40px;
}
</style>
