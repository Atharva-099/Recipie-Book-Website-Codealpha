#TASK1-CODEALPHA
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f2f2f2;
        }

        header {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 1em;
        }

        main {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: white;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        section {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 5px;
        }

        textarea, input {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            box-sizing: border-box;
        }

        button {
            background-color: #1616d5;
            color: white;
            padding: 10px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }

        button:hover {
            background-color: #45a049;
        }
    </style>
    <title>Recipe B00k Website</title>
</head>
<body>
    <header>
        <h1>Recipe Book Website</h1>
    </header>

    <main>
        <section id="recipe-list">
            <!-- Display recipes here -->
        </section>

        <section id="recipe-form">
            <h2>Add/Edit Recipe</h2>
            <form id="recipe-form">
                <label for="recipe-name">Recipe Name:</label>
                <input type="text" id="recipe-name" required>

                <label for="ingredients">Ingredients:</label>
                <textarea id="ingredients" required></textarea>

                <label for="instructions">Instructions:</label>
                <textarea id="instructions" required></textarea>

                <button type="button" id="submit-button" onclick="saveRecipe()">Save Recipe</button>
            </form>
        </section>
    </main>

    <script>
        // Sample recipe data
        let recipes = [
            { name: 'Chicken Korma', ingredients: 'chicken,onions,yogurt,cashews,almonds,oil or ghee,ginger-garlic paste,coconut milk ,water,cumin powder,coriander powder,red chili powder,garam masala,turmeric powder', instructions: 'grind the soaked cashews,smooth paste using a blender,oil or ghee medium heat,spices,pour in the coconut milk and water,garam masala over the chicken korma and mix gently,garnish with fresh coriander leaves' },
            // Add more recipes as needed
        ];

        // Function to display recipes
        function displayRecipes() {
            const recipeList = document.getElementById('recipe-list');
            recipeList.innerHTML = '';

            recipes.forEach((recipe, index) => {
                const recipeCard = document.createElement('div');
                recipeCard.classList.add('recipe-card');
                recipeCard.innerHTML = `
                    <h3>${recipe.name}</h3>
                    <p><strong>Ingredients:</strong> ${recipe.ingredients}</p>
                    <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                    <button onclick="editRecipe(${index})">Edit</button>
                    <button onclick="deleteRecipe(${index})">Delete</button>
                `;
                recipeList.appendChild(recipeCard);
            });
        }

        // Function to save a new or edited recipe
        function saveRecipe() {
            const nameInput = document.getElementById('recipe-name');
            const ingredientsInput = document.getElementById('ingredients');
            const instructionsInput = document.getElementById('instructions');

            const recipe = {
                name: nameInput.value,
                ingredients: ingredientsInput.value,
                instructions: instructionsInput.value
            };

            // Check if we are editing an existing recipe or adding a new one
            if (editingIndex === null) {
                recipes.push(recipe);
            } else {
                recipes[editingIndex] = recipe;
                editingIndex = null; // Reset editing index
            }

            // Clear form inputs
            nameInput.value = '';
            ingredientsInput.value = '';
            instructionsInput.value = '';

            // Refresh the displayed recipes
            displayRecipes();
        }

        // Function to edit a recipe
        function editRecipe(index) {
            const recipe = recipes[index];
            const nameInput = document.getElementById('recipe-name');
            const ingredientsInput = document.getElementById('ingredients');
            const instructionsInput = document.getElementById('instructions');

            // Populate form with selected recipe data
            nameInput.value = recipe.name;
            ingredientsInput.value = recipe.ingredients;
            instructionsInput.value = recipe.instructions;

            // Set the editing index to the selected recipe
            editingIndex = index;
        }

        // Function to delete a recipe
        function deleteRecipe(index) {
            recipes.splice(index, 1);
            displayRecipes();
        }

        // Initial display of recipes
        displayRecipes();
    </script>
</body>
</html>
