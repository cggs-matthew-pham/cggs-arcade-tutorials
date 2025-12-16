### @title Numbers and Math

### @description Use ask for number, calculate an answer using division and rounding down, then check the player’s answer and update score.

### @preferredEditor blocks

### @explicitHints true

# Numbers and Math

## Step 1: Set up score (on start)

We will use score so correct answers can earn a point.

  

- Open Info

- Drag set score to 0 into the workspace

- Leave this outside any function

  

```blocks

info.setScore(0)

```

  

## Step 2: Create a function for the maths section

We will keep all the maths and checking logic inside a function.

  

- Open Advanced → Functions

- Click Make a Function

- Name it calculateNumberOfHungryStudents

The function will not run unless we call it.

  

- Drag **call calculateNumberOfHungryStudents** into the workspace

- Place it inside **on start**

```blocks

function calculateNumberOfHungryStudents () {

  

}

calculateNumberOfHungryStudents()

```

  

## Step 3: Show an intro message

Explain the idea before asking questions.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

}

```

  

## Step 4: Explain the maths

Tell the player what calculation they need to do.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

}

```

  

## Step 5: Ask for the number of students

Collect a number from the player.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

    let numStudents = game.askForNumber("How many students are there in this class?", 2)

}

```

  

## Step 6: Ask the player for their answer

Ask the player to enter their calculated result.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

    let numStudents = game.askForNumber("How many students are there in this class?", 2)

    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)

}

```

  

## Step 7: Calculate the correct answer

The program now calculates the real answer.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

    let numStudents = game.askForNumber("How many students are there in this class?", 2)

    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)

    let numHungryStudents = Math.floor(numStudents / 9)

}

```

  

## Step 8: Check if the answer is correct

Use an if / else block to compare the numbers.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

    let numStudents = game.askForNumber("How many students are there in this class?", 2)

    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)

    let numHungryStudents = Math.floor(numStudents / 9)

  

    if (playerAnswer == numHungryStudents) {

  

    } else {

  

    }

}

```

  

## Step 9: Add feedback and update score

Fill in the if / else blocks.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

    let numStudents = game.askForNumber("How many students are there in this class?", 2)

    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)

    let numHungryStudents = Math.floor(numStudents / 9)

  

    if (playerAnswer == numHungryStudents) {

        info.changeScoreBy(1)

        game.showLongText("Correct! There would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)

    } else {

        game.showLongText("No, actually there would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)

    }

}

```

  

## Step 10: Wrap-up message (optional)

End with a reflective question.

  

```blocks

function calculateNumberOfHungryStudents () {

    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)

    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)

    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)

    let numStudents = game.askForNumber("How many students are there in this class?", 2)

    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)

    let numHungryStudents = Math.floor(numStudents / 9)

  

    if (playerAnswer == numHungryStudents) {

        info.changeScoreBy(1)

        game.showLongText("Correct! There would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)

    } else {

        game.showLongText("No, actually there would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)

    }

  

    game.showLongText("What can we do to make sure EVERYONE has enough to eat?", DialogLayout.Bottom)

}

```

  

## Step 11: Call the function

The function will not run unless we call it.

  

```blocks

info.setScore(0)

calculateNumberOfHungryStudents()

```

  

## Step 12: Test your program

Run the game and check that everything works.