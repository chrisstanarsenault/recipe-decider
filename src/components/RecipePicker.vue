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
      <form>
        Recipe Name:<input id="newRecipeName"><button @click.prevent="addRecipeName">Add</button>
      </form>
      <form>
        Recipe Link:<input id="newRecipeLink"><button @click.prevent="addRecipeLink">Add</button>
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
      <p>Recipe Name: {{ recipeName }}</p>
      <p>Recipe Link:<a :href=recipeLink value="https://">{{ recipeLink }}</a></p>

      <span style="vertical-align: top;">Recipe Ingredients:
        <ol style="display:inline-block; margin:0">
          <li v-for="(ingredient, index) in recipeIngredients">{{ingredient}}<button @click="removeIngredient(index)">Remove</button></li>
        </ol>
      </span>

      <br>

      <span style="vertical-align: top;">Recipe Directions:
        <ol style="display:inline-block; margin:0">
          <li v-for="(direction, index) in recipeDirections">{{direction}}<button @click="removeDirection(index)">Remove</button></li>
        </ol>
      </span>
    </div>
    <button @click.prevent="submitToRecipes">Add To Recipe List</button>
    <button @click.prevent="clearField">Clear Field</button>
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
        recipeName: "",
        recipeLink: "",
        recipeIngredients: [],
        recipeDirections: [],
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
      addToNewRecipeIngredient() {
        let ingredient = document.getElementById("newIngredients").value;
        this.recipeIngredients.push(ingredient);
        document.getElementById("newIngredients").value = "";
      },
      addToNewRecipeDirection() {
        let direction = document.getElementById("newDirections").value;
        this.recipeDirections.push(direction);
        document.getElementById("newDirections").value = "";
      },
      removeIngredient(index) {
        this.recipeIngredients.splice(index, 1);
      },
      removeDirection(index) {
        this.recipeDirections.splice(index, 1);
      },
      addRecipeName() {
        let newRecipeName = document.getElementById("newRecipeName").value;
        this.recipeName = newRecipeName;
        document.getElementById('newRecipeName').value = "";
      },
      addRecipeLink() {
        let newRecipeLink = document.getElementById("newRecipeLink").value;
        if (newRecipeLink.includes('https://') || newRecipeLink.includes('http://')) {
          this.recipeLink = newRecipeLink;
        } else {
          this.recipeLink = 'https://' + newRecipeLink;
        }
        document.getElementById('newRecipeLink').value = "";
      },
      submitToRecipes() {
        this.recipes.push(
          {
            recipeName: this.recipeName,
            recipeLink: this.recipeLink,
            recipeIngredients: this.recipeIngredients,
            recipeDirections: this.recipeDirections
          }
        );
      },
      clearField(e) {
        this.recipeName = "";
        this.recipeLink = "";
        this.recipeIngredients = [];
        this.recipeDirections = [];
        e.preventDefault();
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