<template>
  <main class="w-100 min-vh-100 bg-gray9 white sans-serif pa6 flex flex-column justify-center items-center ba bw4 b--gray8">
  <div class="mw8 center w-100 overflow-hidden">

    <h1 class="mt0 mb4 tc fw6 f6 black-10">
      <a href="https://fontawesome.com" class="link gray2 hover-white">
        <i class="fab fa-font-awesome-flag"></i>
        <span> Using SVG Symbols</span>
      </a>
    </h1>

    <!-- Define the symbols, these are invisible on the page -->
    <i data-fa-symbol="delete" class="fas fa-trash fa-fw"></i>
    <i data-fa-symbol="edit" class="fas fa-pencil fa-fw"></i>
    <i data-fa-symbol="favorite" class="fas fa-star fa-fw"></i>
    <svg class="icon pa2 br2 pointer bg-gray"><use xlink:href="#edit"></use></svg>
    <!-- <div class="flex justify-center">
      <div id="app" class="w-50">
        <div v-for="row of rows" class="flex items-center bb ph2 bw2 mb2 b--black-10">
          <div class="w-80 pv2">
             {{ row.label }}
          </div>
          <div class="w-20 tr pv2">
            Leverage the SVG Sprite technique and the <use> tag
            <svg class="icon pa2 br2 pointer bg-gray"><use xlink:href="#edit"></use></svg>
            <svg class="icon pa2 br2 pointer bg-gray"><use xlink:href="#delete"></use></svg>
            <svg class="icon pa2 br2 pointer bg-gray"><use xlink:href="#favorite"></use></svg>
          </div>
        </div>
      </div>
    </div> -->
  </div>
</main>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.icon {
  width: 2em;
  height: 2em;
  color:brown;
}
</style>
