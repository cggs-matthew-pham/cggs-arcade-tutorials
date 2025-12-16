### @title Story, Quiz and Score

### @description Tell a short story, ask a quiz question, and track the player’s score based on their answers.

### @preferredEditor blocks

### @explicitHints true

# Story, Quiz and Checking Answers
## Step 1: Add the Story extension (for choices)

We need the Story extension so we can show multiple-choice questions.

  

- Click **Extensions**

- Search for **story**

- Add the **arcade-storytelling** extension

  

## Step 2: Create a function for your story section

Now we will put the story text and quiz into its own function.

  

- Open **Advanced → Functions**

- Click **Make a Function**

- Name it `welcomeToOzHarvest`

- Click **Done**

  

The function will not run unless we call it.

  

- Drag **call welcomeToOzHarvest** into the workspace

- Place it inside **on start**

  

```blocks

function welcomeToOzHarvest () {

  

}

  

welcomeToOzHarvest()

  
  

```

  
  
  

## Step 3: Add the first story text (long text)

We will use long text blocks so the player reads one message at a time.

  

- Open **Game**

- Drag **show long text** into the `welcomeToOzHarvest` function

- Type: `Welcome to OzHarvest!`

- Set the layout to **Bottom** (or keep the default)

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

}

```

  

## Step 4: Add more story text (a short sequence)

Add a few more long text blocks to create a short intro.

  

- Duplicate the long text block a few times (right click → Duplicate)

- Update the text in each block

  

Example sequence:

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)

    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)

}

```

  

## Step 5: Add the quiz question (player choices)

Now we add a multiple-choice question.

  

- Add a new long text blocks to show the question text for the player's choices

- Open **Story**

- Drag **show player choices** into the function

- Add four answer options (you can edit these later)

  

Example:

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)

    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)

    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)

    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")

}

```

  

## Step 6: Add a score variable

We’ll keep score so correct answers increase it.

  

- Open **Info**

- Click **set score to 0** (or create score however you prefer)

- Place it near the start of your program

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)

    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)

    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)

    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")

}

  

info.setScore(0)

welcomeToOzHarvest()

```

  

## Step 7: Check the player’s answer

We will check the last choice and respond.

  

- Open **Logic**

- Drag an **if / else** block under the choices

- Open **Story**

- Use **check last answer** inside the if condition

- Put the correct answer text exactly (must match one of the options)

  

Example:

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)

    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)

    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)

    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")

    if (story.checkLastAnswer("2 million")) {

    } else {

    }

}

```

  

## Step 8: Add feedback + update score

Now we fill in the if / else actions.

  

- In the **if** block:

  - Open **Info** → **change score by 1**

  - Open **Game** → **show long text** → “That’s correct!”

- In the **else** block:

  - Open **Game** → **show long text** → “No, it’s actually 2 million!”

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)

    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)

    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)

    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")

    if (story.checkLastAnswer("2 million")) {

        info.changeScoreBy(1)

        game.showLongText("That's correct!", DialogLayout.Bottom)

    } else {

        game.showLongText("No, it's actually 2 million!", DialogLayout.Bottom)

    }

}

```

  

## Step 9: Add a “wrap-up” story text after the quiz

Add a couple more long text blocks after the if / else to extend the learning.

  

```blocks

function welcomeToOzHarvest () {

    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)

    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)

    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)

    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)

    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")

    if (story.checkLastAnswer("2 million")) {

        info.changeScoreBy(1)

        game.showLongText("That's correct!", DialogLayout.Bottom)

    } else {

        game.showLongText("No, it's actually 2 million!", DialogLayout.Bottom)

    }

    game.showLongText("In Australia we waste 7.6 million tonnes of food every year.", DialogLayout.Bottom)

    game.showLongText("This costs over $36.6 billion dollars!", DialogLayout.Bottom)

}

```

  

## Step 10: Test your story section

Run the game and check:

  

- The long text appears in the right order

- The choices appear

- Picking the correct option increases the score

- You see the correct/incorrect feedback

  
  

