# Mini project exercises

This list offers some bigger coding projects to test how you can combine many programming skills we've covered throughout the CodeAcademy Python curriculum. If you're proud of what you create, consider sharing it on GitHub!

Prerequisites:
- CodeAcademy Python Level 1
- Python Advanced and OOP Advanced submodules from CodeAcademy Python Level 2

There are two types of challenges:
- **Clear instructions (C)**: These challenges are like following a recipe - someone tells you exactly what to do step-by-step. These types of exercises prepare you for working on a team where you'll be given detailed instructions for tasks. All you need to do is implement a described feature or project.
- **Vague instructions (V)**: These challenges are more like coming up with a recipe for a specified food. You'll need to understand the main idea, design the project, and figure out the implementation details yourself. These exercises are similar to job interview take-home coding tasks or working with a client who doesn't yet clearly know what their end product should look like. These exercises are trickier because you need to plan more beforehand and take responsibility for your plans by implementing them.

Remember that future you as well as other programmers will look at your code. Do them a favour and follow the following tips for working on new Python projects: 
- Before starting writing code we *highly* recommend to plan your program. Use pen and paper or write comments at the top of your python file. 
  - What is the desired use of your program? How will you or the user interact with it? What are the inputs, what are the outputs?
  - What functions should you create? Why? Write small documentation for functions _before_ implementing them.
  - What classes should you create? Why is it appropriate to use OOP here?
  - Should you use inheritance? Should you use encapsulation (data hiding)? Do we have multiple similar classes, would an abstract base class help, then? 
  - It's almost always a good idea to implement magic methods like `__str__`, `__repr__` for classes. Think about whether you will compare objects, then implement `__eq__`, `__ne__`, `__le__`, `__ge__`, etc.
  - Think about whether it is appropriate to use `@dataclass`, `@staticmethod`, `@classmethod`, or custom decorators.
- Write documentation for functions and classes.
- Use type hinting in function arguments.
- Use PEP8 style to make your code readable. Press `CTRL + ALT + L` often!
- Use `print()` calls or the `logging` library often for testing and debugging! If you run into problems, use Pycharm IDE debugger
- If it makes sense, separate your functions and classes into distinct files and structure your project.  
- Use `git` and GitHub to keep track of your project and show it to others. Use informative commit messages and push small changes often!
  - Write a `README.md` file briefly describing your project. Why did you create it? How can people use it? 

## Tank exercise (C)

Your task is to develop a simple [command-line interface](https://en.wikipedia.org/wiki/Command-line_interface) tank game. You will implement this exercise in stages, each stage is a bit more difficult and *builds upon* the previous stage. That is, please develop the same file iteratively or create a separate file each time where you copy from the previous stage, creating files `tank_stage1.py`, `tank_stage2.py`, etc.

Start with the given file `tank_game.py` because it has some starting code to make it easier for you.

```
# tank_game.py

class TankGame:
    def __init__(self, N: int = 7):
        """Create a tank game object.

        :param N: the size of the map (grid) NxN to generate for the game.
        """
        self.N = N
        # Hard-coded starting tank location is 2, 1
        self.tank_loc_x = 2
        self.tank_loc_y = 1
        # Starting direction: tank facing north/up
        self.direction = "up"

    def print_map(self):
        """Print the current map of the game.

        Example output for a 7x7 map:
           0  1  2  3  4  5  6
        0  .  .  .  .  .  .  .
        1  .  .  T  .  .  .  .
        2  .  .  .  .  .  .  .
        3  .  .  .  .  .  .  .
        4  .  .  .  .  .  .  .
        5  .  .  .  .  .  .  .
        6  .  .  .  .  .  .  .

        where T is the location of the tank,
        where . (the dot) is an empty space on the map,
        where the horizontal axis is the x location of the tank and,
        where the vertical axis is the y location of the tank.
        """
        # Print the numbers for the x axis
        print("   " + "  ".join([str(i) for i in range(self.N)]))

        for i in range(self.N):
            # Print the numbers for the y axis
            print(f"{i} ", end="")
            for j in range(self.N):
                if self.tank_loc_x == j and self.tank_loc_y == i:
                    print(" T ", end="")
                else:
                    print(" . ", end="")
            print()

    def steer_left(self):
        # TODO implement this
        pass

    # TODO: add more methods here


if __name__ == "__main__":
    # Initialize your game object
    tg = TankGame()
    # Start game loop
    while True:
        tg.print_map()

        command = input("Input a command: ")
        if command == "left":
            tg.steer_left()
        # TODO: add more command handling here...

```


### Stage 1

All tank and information management must be done on the console (actual graphical interface is not required). This will require you to create a menu and accept user instructions. Actions to be performed (methods called) until the user stops the program (for example, by selecting an actual menu item). You can use this management to test your TankGame class during your coding process.

Class: TankGame

Methods to implement: `print_map` (already implemented), `forward`, `backward`, `steer_left`, `steer_right`, `shoot`, `info`, ...

Store the following variables in the class:
- Tank coordinates.
- Direction of the tank.
- Number of shots in each direction.

The tank can move forward (to the North), to the right (to the East), back (to South), left (West) by one position. For example "the tank is moving left," meaning it turned 90 degrees and moved through one unit to the West.

A tank can only fire in the direction it is facing.

The `info()` method must display:
- Which direction the tank is currently facing.
- What are its coordinates.
- How many total shots did it make.
- How many shots were fired in each direction separately.

### Stage 2

Improve the program so that:
- A target is generated in the tank game grid. 
- The task of the tank is to be in the right position and in the right direction so that a hit is recorded after firing. 
- When a tank hits, we see the message "hit" on the console and a new target is generated immediately. 

### Stage 3

Improve the program further:
- Come up with a point system, e.g. start with 100 points, +50 points for hits, -10 points for each forward drive, sum up total hits.
  - Briefly describe the point system to the player at the start of the game or when `info()` is called.
- Show the points next to the game grid. 
- When the points run out, the program shows how many targets have been shot down and ends. 
- Perhaps it is possible to store high scores - after the end, the name is entered and the player with the number of downed targets is recorded in the charts. 
- The charts can perhaps be viewed with the 'top' command. 

### Stage 4

Come up with some improvements of your own! Remember to document your new features well. Provide information for the player at the start of your game of what should they expect.

## Hangman (C)

The final product should look something like [this](https://i.vimeocdn.com/video/1727623664-abc3c668b087e48ec826f30ef75a285dada9f1fc4c3a45eba37c254f3a0406cd-d?mw=700&mh=393). 

Exercise inspired by [this](https://realpython.com/python-hangman/).

### Step 1: Set Up the Hangman Project

Your hangman game will select a word, handle user input, and display all output using a text-based user interface. You need code to handle each of these tasks. However, you’ll do everything using built-in and standard-library tools. You don’t need to install anything else.

### Step 2: Select a Word to Guess

The first step in playing hangman is to select the target word. When a human player selects a word for hangman, they pick one word from their own vocabulary. For the computer to select a word, it needs to have a vocabulary from which to select. Of course, its vocabulary doesn’t need to be as large as a human’s.

### Step 3: Get and Validate the Player’s Input

Now, you need a way to get the player’s guesses at the command line. After all, a game isn’t much of a game if there isn’t some way for the player to influence the outcome.

In your hangman game, you have to get the player’s input and make sure that it’s valid. Remember when you created your list of words? All the words were in lowercase, so you should turn the player’s guesses into lowercase letters as well.

Additionally, the player shouldn’t be able to guess the same letter twice. It’d also be good to avoid numbers, special characters, and complete words as well.

### Step 4: Display the Guessed Letters and Word

Once you’ve selected the target word in a real-life game of hangman, you need to write an underscore, or blank, for each letter in the word. These blanks tell the players how many letters are in the target word. As players make guesses, you fill in the blanks with the correct letters. You should also keep track of incorrect letters, which you write to the side.

### Step 5: Draw the Hanged Man

Of course, there’s no hangman game without the actual hanged man, is there? You could simply print out the number of guesses the player has taken. But if you want to make the game look like hangman, then showing the hanged man is a good idea.
Implement a function `draw_hanged_man` that, depending on the integer passed, will show different ASCII pictures 

```
>>> draw_hanged_man(0)
  -----
  |   |
      |
      |
      |
      |
      |
      |
      |
      |
-------

>>> draw_hanged_man(6)
  -----
  |   |
  O   |
 ---  |
/ | \ |
  |   |
 ---  |
/   \ |
|   | |
      |
-------
```

### Step 6: Figure Out When the Game Is Over

Games normally end due to a condition set up by the player’s input. Perhaps the player has finally reached the goal, or they failed some task and lost the game.

Your hangman game ends when one of two events happens:

- The player makes six incorrect guesses.
- The player guesses the word correctly.

Both of these outcomes stem from the player’s input. So, it makes sense to check for them in the game loop, which is where you gather, validate, and process all player input. Encapsulating these checks into a function is a good idea as well.

### Step 7: Run the Game Loop

Up to this point, you’ve assembled the functions and code that cover most of the important parts of your hangman game. Those parts include the following:

1. Selecting a random word to guess
2. Gathering and processing the player’s input
3. Showing the word with unguessed letters hidden
4. Showing the hanged man drawing
5. Tracking the letters guessed and guesses taken
6. Checking if the game is over

## Bank simulation (C)

Your task is to build a system that can parse bank records and put them into a "database" correctly. 
We will not work with actual databases, but will represent them as classes and files.

Consider the following text file (copy and save it as `bank-records.txt`) consisting of these bank records:
```
CREATE_ACC "John Smith" 0 EUR
DEPOSIT 1 200
WITHDRAW 1 100
CREATE_ACC "Louise Johnson" 500 USD
WITHDRAW 1 50
WITHDRAW 2 25
TRANSFER 2 1 100
DELETE_ACC 2
CREATE_ACC "John Smith" 1000 USD
CREATE_ACC "Peter W Higgs" 123 GBP
TRANSFER 3 4 100
```

Explanation:
-  `CREATE_ACC "John Smith" 0 EUR`. Creates an account for "John Smith" with an initial balance of 0 for EUR currency. 
  - Upon creation, an automatic ID starting (from 1 and incrementing by 1 for each new account) should be assigned to each account which will be referred to in the next commands.
- `DEPOSIT 1 200`. Add 200 money (whichever currency the account has) to the account with ID 1 (the only one that has been created so far)
- `WITHDRAW 1 100`. Subtract 100 money from account with ID 1. Subtract an extra 0.5% from the withdrawal amount (in this case, 0.5 EUR) because the bank charges for withdrawal.   
- `CREATE_ACC "Louise Johnson" 500 USD`. Create a new account for holder "Louis Johnson" with an initial balance of 500 USD
- `WITHDRAW 1 50`. Subtract 50 money from account with ID 1. Subtract an extra 0.5% from the withdrawal amount because the bank charges for withdrawal. 
- `WITHDRAW 2 25`. Subtract 25 money from account 25. Subtract an extra 0.5% from the withdrawal amount because the bank charges for withdrawal. 
- `TRANSFER 2 1 100`. Transfer 100 money from account 2 to account 1. 
  - Since account 2 has currency USD, we will transfer 100 USD to account 1. 
  - Proper currency conversion should take place when transferring between accounts with different currencies. 
  - Transfers cost 0.7% of (in this case, 0.7 USD) the transferred amount for the account sending money (in this case, account ID 2).
- `DELETE_ACC 2`. The account with ID 2 should be deleted from the bank system. New account ids continue to increment UP.
- `CREATE_ACC "John Smith" 1000 USD`. Creates an account for "John Smith" with an initial balance of 1000 for USD currency. 
- `CREATE_ACC "Peter W Higgs" 123 GBP`. Creates an account for "Peter Higgs" with an initial balance of 123 CHF currency. 
- `TRANSFER 3 4 100`. Transfer 100 money (of corresponding currency) from account 3 to account 4.  
  
In a nutshell, your task is to:
- Create a way to read the file, parse the bank records and handle them accordingly
- You should use classes to handle storage of data for accounts and processing the transactions
- At the end of reading the whole file and handling its operations, you should print the final states of all _existing_ accounts to a CSV file

### Stage 1

- Create a file `main.py` which will be the starting file to our application
- As always, add `if __name__ == "__main__":` in it which is where we will trigger the necessary functions to process the bank records file
- Create a file `bank_records.py` where we will store all bank record file reading functions  
- Implement a function to read the file `bank-records.txt` line by line and return the processed text
- Process each word of the input by splitting it up by spaces. Hint: take a look at the `csv` library and its `delimeter` parameter, it could save you a lot of trouble.
- For debugging, use the `logging` library to log how the bank record was parsed. For example:
```
2024-02-27 20:41:52 DEBUG. Command: CREATE_ACC, Parameters: ['John Smith', '0', 'EUR']
2024-02-27 20:41:52 DEBUG. Command: DEPOSIT, Parameters: ['1', '200']
2024-02-27 20:41:52 DEBUG. Command: WITHDRAW, Parameters: ['1', '100']
```

### Stage 2

- Create an `accounts.py` file and keep all functionality related to bank accounts here
- Create a `BankAccount` dataclass that has all the needed properties
- Create a `BankAccountManager` class. It is the main "puppeteer" part of this project. This class should:
  - Have a list (or dictionary) of all `BankAccount` instances created
  - For now, skip handling the `TRANSFER` operation
  - Implement a `process_command(self, command, parameters)` method that calls other appropriate methods (read next point) based on the command 
  - Implement each bank operation via methods. For example, `CREATE_ACC` should be a method `create_account(self, parameters)`
- For debugging, log the string representation of each account before and after the bank command action was taken. For example:
```
2024-02-27 20:55:36,070 DEBUG. BankAccount(id=1, holder='John Smith', balance=0, currency='EUR')
2024-02-27 20:55:36,070 DEBUG. Performing deposit on account id 1 with amount 200
2024-02-27 20:55:36,070 DEBUG. BankAccount(id=1, holder='John Smith', balance=200, currency='EUR')
```

### Stage 3

- Create a `conversion.py` file and keep the currency conversion-related things here
- Create a `CurrencyConversion` class which 
  - Has a dictionary with currencies (in our example it's enough to have EUR, USD, GBP) and their conversion rates. Use the following conversion rates:
    - USD to EUR: 0.91
    - EUR to USD: 1.09
    - USD to GBP: 0.78
    - GBP to USD: 1.28
    - EUR to GBP: 0.85
    - GBP to EUR: 1.17
  - Has a method `convert_currency` that converts a given amount of one currency to a different currency
- Implement the `TRANSFER` command handling using the `CurrencyConversion` class instance

### Stage 4

- Implement a method `dump_accounts_to_csv` as part of `BankAccountManager` which writes the state of each _still existing_ account to a csv file. For example, after processing the file above, our output CSV file should look like this:
```csv
account_id,holder,balance,currency
1,"John Smith",140.25,EUR
3,"John Smith",899.3,USD
4,"Peter W Higgs",201.00,GBP
```
- Add another debug logging when writing to file, for example
```
2024-02-27 20:59:56,080 DEBUG. Writing to file: BankAccount(id=1, holder='John Smith', balance=200, currency='EUR')
```

### (Advanced) Stage 5 

- Extend the bank record format so that now there's two types of accounts: standard and premium.
  - For example, the command `CREATE_ACC_STD "ABC" 100 USD` will create a standard account for account holder ABC with 100 USD initial funds.
  - The command `CREATE_ACC_PRM` would create a premium account
- Reflect these changes by changing `BankAccount` to an abstract base class.
  - Extend `BankAccount` class to implement with additional `account_type` property.
  - Implement `StandardBankAccount` and `PremiumBankAccount`, both inherit from `BankAccount`
  - Change the withdrawal and transfer methods in `BankAccount` to be abstract methods, concrete implementations of these methods should reside in `PremiumBankAccount` and `StandardBankAccount` instead
    - Standard accounts, as before, pay 0.5% for money withdrawal and 0.7% for money transfers
    - Premium accounts pay 0.3% for money withdrawal and 0.45% for money transfers
    - When created, standard accounts pay 0.1% of their initial funds for the account creation (if the initial funds are 0, then they don't pay anything)
    - When created, premium accounts pay 0.3% of their initial funds for the account creation (if the initial funds are 0, then they don't pay anything)
- Update the logging messages to reflect these changes
- When writing the final result to CSV file, also include the account type

So, after incorporating these changes and processing the following bank records:
```
CREATE_ACC_STD "John Smith" 0 EUR
DEPOSIT 1 200
WITHDRAW 1 100
CREATE_ACC_PRM "Louise Johnson" 500 USD
WITHDRAW 1 50
WITHDRAW 2 25
TRANSFER 2 1 100
DELETE_ACC 2
CREATE_ACC_PRM "John Smith" 1000 USD
CREATE_ACC_STD "Peter W Higgs" 123 GBP
TRANSFER 3 4 100
```

the final CSV output file should look like:
```csv
account_id,holder,balance,currency
1,"John Smith",140.25,EUR
3,"John Smith",896.55,USD
4,"Peter W Higgs",200.88,GBP
```

## Task app (V)

Create a program where you can track a list of your tasks. With each task, you should be able to specify its name, priority, and deadline.
- You can keep track of your tasks inside a `tasks.txt` file which your program would constantly modify. You can use a simple text format but we recommend using JSON or CSV because it should be easier to work with it.
- You can implement your program that, once you run it, you can input your desired arguments using a CLI-like commands (similar to [Tank](#tank-exercise-d) exercise above)
- Alternatively, your application could benefit from [parsing arguments](https://docs.python.org/3/howto/argparse.html#argparse-tutorial). 
For example, you could run it as 
```bash
python todo.py --add "Do dishes" --priority 2 --deadline "2024-02-24 12:00"
```
where the words with `--` such as `--add` are called python program options and the words 
following those, such as `"Do dishes"` are the arguments. In this case, you would indicate 
that you like to _add_ the task "Do dishes" as a task.

For example, interaction with your application could look like this (this is using arguments, but similar idea would work for CLI applications):
```bash
>>> python todo.py --add "Do dishes" --priority 2 --deadline "2024-02-24 12:00"
Task added successfully! Here is the current list:
2. Do dishes. Due date: 2024-02-24 12:00
>>> python todo.py --add "Do laundry" --priority 1 --deadline "2024-02-24 11:00"
Task added successfully! Here is the current list:
1. Do laundry. Due date: 2024-02-24 11:00
2. Do dishes. Due date: 2024-02-24 12:00
>>> python todo.py --add "Call grandma" --priority 2 --deadline "2024-02-24 15:00"
Task added successfully! Here is the current list:
1. Do laundry. Due date: 2024-02-24 11:00
2. Do dishes. Due date: 2024-02-24 12:00
2. Call grandma. Due date: 2024-02-24 15:00
>>> python todo.py --del "Do laundry"
Task deleted successfully! Here is the current list:
2. Do dishes. Due date: 2024-02-24 12:00
2. Call grandma. Due date: 2024-02-24 15:00
>>> python todo.py --del
Latest task deleted successfully! Here is the current list:
2. Call grandma. Due date: 2024-02-24 15:00
>>> python todo.py --edit "Call ganma" --name "Call mom" --priority 3 --deadline "2024-02-25 17:00"  
Unfortunately, "Call ganma" task currently does not exist. Try again!
Here is the current list of tasks:
2. Call grandma. Due date: 2024-02-24 15:00
>>> python todo.py --edit "Call grandma" --name "Call mom" --priority 3 --deadline "2024-02-25 17:00"  
Task edited successfully! Here is the current list:
3. Call mom. Due date: 2024-02-25 17:00
```

## Wordle (V)

Create a [Wordle](https://en.wikipedia.org/wiki/Wordle) clone in python. You can use [colorama](https://pypi.org/project/colorama/) to set colors to printed outputs, check its documentation to understand how to use it.

## Rolling dice (V)

Demo of the app [here](https://files.realpython.com/media/python-dice-roll-demo.93e6fe0d714a.gif).

## Flashcard app (V)

Build a [flashcard](https://en.wikipedia.org/wiki/Flashcard) app. 

- Your flashcards can be stored in a TXT, JSON, CSV or other format in some file. 
- Implement some logic which retrieves the cards using [spaced repetition](https://www.khanacademy.org/science/learn-to-learn/x141050afa14cfed3:learn-to-learn/x141050afa14cfed3:spaced-repetition/a/l2l-spaced-repetition).
- Example usage could look similar to [this](https://github.com/bttger/markdown-flashcards) but feel free to create your own!
