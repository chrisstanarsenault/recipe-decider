<template>
  <div>
    <button @click="randomMeal">Pick A Meal For Me!</button>
   <p v-if="wasClicked">{{ chosenRecipe.recipeName }}</p>
   <div v-if="wasClicked">
    <button @click="showLink = !showLink">Show Recipe Link</button>
    <button @click="showIngredients = !showIngredients">Show Ingredient List</button>
    <button @click="showDirections = !showDirections">Show Directions</button>
   </div>
   <p v-if="showLink">{{ chosenRecipe.recipeLink }}</p>
   <ol v-if="showIngredients">
    <li v-for="ingredient in chosenRecipe.recipeIngredients">{{ ingredient }}</li>
   </ol>
   <ol v-if="showDirections">
     <li v-for="direction in chosenRecipe.recipeDirections">{{ direction }}</li>
   </ol>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        chosenRecipe: {},
        wasClicked: false,
        showLink: false,
        showIngredients: false,
        showDirections: false,
        recipes:[
          {
            recipeName: 'Frat Boy Pasta',
            recipeLink: 'www.gamespot.com',
            recipeIngredients: ['Carrots', '2 Heads Broccoli', '1 Yellow Onion', 'Tomato Sauce', 'Cheddar Cheese', 'Garlic Powder', 'Onion Powder', 'Penne Noodles'],
            recipeDirections: ['Add shit in pot', 'eat that son bitch']
          },

          {
            recipeName: 'Kraft Dinner',
            recipeLink: 'www.ign.com',
            recipeIngredients: ['Box of KD', 'Milk', 'Butter'],
            recipeDirections: ['Just do it']
          }
        ]
      }
    },
    methods: {
      randomMeal() {
        let mealLength = this.recipes.length
        let randomMealIndex = Math.floor(Math.random() * mealLength);
        let randomMeal = this.recipes[randomMealIndex]
        this.chosenRecipe = randomMeal;
        this.wasClicked = true;
      }
    }
  }
</script>

<style scoped>

</style>