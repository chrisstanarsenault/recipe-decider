<template>
  <div>
    <button @click="randomMeal">Pick A Meal For Me!</button>
    <hr>
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
    <button @click="addNewRecipe = !addNewRecipe">Add A New Recipe</button>

    <div v-if="addNewRecipe">
      <form @submit.prevent="check">
        Recipe Name:<input v-model.lazy="newRecipe.recipeName">
      <br>
        Recipe Link:<input v-model.lazy="newRecipe.recipeLink">
      </form>

      <form>
        Recipe Ingredients:<input id="newIngredients"><button @click.prevent="addToNewRecipeIngredient">Add</button>
      </form>

      <form>
        Recipe Directions:<input id="newDirections"><button @click.prevent="addToNewRecipeDirection">Add</button>
      </form>
    </div>

    <div>
      <p>New Recipe</p>
      <hr>
      <p>Recipe Name: {{ newRecipe.recipeName }}</p>
      <p>Recipe Link: {{ newRecipe.recipeLink }}</p>

      <span style="vertical-align: top;">Recipe Ingredients:
        <ol style="display:inline-block; margin:0">
          <li v-for="(ingredient, index) in newRecipe.recipeIngredients">{{ingredient}}<button @click="removeIngredient(index)">Remove</button></li>
        </ol>
      </span>

      <br>

      <span style="vertical-align: top;">Recipe Directions:
        <ol style="display:inline-block; margin:0">
          <li v-for="(direction, index) in newRecipe.recipeDirections">{{direction}}<button @click="removeDirection(index)">Remove</button></li>
        </ol>
      </span>
    </div>
    <button @click="submitToRecipes">Add To Recipe List</button>
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
        addNewRecipe: false,
        newRecipe: {
          recipeName: '',
          recipeLink: '',
          recipeIngredients: [],
          recipeDirections: []
        },
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
      },
      check() {
        console.log(this.newRecipe.recipeName)
      },
      addToNewRecipeIngredient() {
        let ingredient = document.getElementById("newIngredients").value;
        this.newRecipe.recipeIngredients.push(ingredient);
        document.getElementById("newIngredients").value = "";
      },
      addToNewRecipeDirection() {
        let direction = document.getElementById("newDirections").value;
        this.newRecipe.recipeDirections.push(direction);
        document.getElementById("newDirections").value = "";
      },
      removeIngredient(index) {
        this.newRecipe.recipeIngredients.splice(index, 1);
      },
      removeDirection(index) {
        this.newRecipe.recipeDirections.splice(index, 1);
      },
      submitToRecipes() {
        this.recipes.push(this.newRecipe);

        console.log(this.recipes)
      }
    }
  }

</script>

<style scoped>
  .recipe-container {
    padding: 0;
    margin: 0;
  }
</style>