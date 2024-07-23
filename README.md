---------------------------------------------

This Python script creates a simple snake game using the Turtle graphics library and the freegames module. The player controls a snake that moves around the screen, eats food to grow, and tries to avoid running into the walls or itself.

---------------------------------------------

Importing Required Modules

---------------------------------------------

from turtle import *
from random import randrange
from freegames import square, vector
turtle: Provides functions to create graphics and animations.
randrange: Generates random numbers, used to place food randomly on the screen.
freegames: A module that provides additional functions like square for drawing shapes and vector for handling coordinates.

---------------------------------------------

Initializing Game Variables

---------------------------------------------

food = vector(0, 0)
snake = [vector(10, 0)]
aim = vector(0, -10)
food: A vector representing the position of the food.
snake: A list of vectors representing the segments of the snake, starting with one segment at position (10, 0).
aim: A vector representing the direction the snake is moving, initially set to move down.

---------------------------------------------

Defining Helper Functions

---------------------------------------------

def change(x, y):
    "Change snake direction."
    aim.x = x
    aim.y = y
change(x, y): Updates the direction of the snake based on key presses.

---------------------------------------------

def inside(head):
    "Return True if head inside boundaries."
    return -200 < head.x < 190 and -200 < head.y < 190
inside(head): Checks if the snake's head is within the game boundaries. Returns True if inside, False otherwise.

---------------------------------------------

def move():
    "Move snake forward one segment."
    head = snake[-1].copy()
    head.move(aim)

    if not inside(head) or head in snake:
        square(head.x, head.y, 9, 'red')
        update()
        return

    snake.append(head)

    if head == food:
        print('Snake:', len(snake))
        food.x = randrange(-15, 15) * 10
        food.y = randrange(-15, 15) * 10
    else:
        snake.pop(0)

    clear()

    for body in snake:
        square(body.x, body.y, 9, 'black')

    square(food.x, food.y, 9, 'green')
    update()
    ontimer(move, 100)
move(): Advances the snake forward by one segment:
Copies the position of the snake's head and moves it in the direction of aim.
Checks if the new head position is inside the boundaries and not overlapping the snake itself.
Draws the snake's head in red and stops the game if the move is invalid.
Adds the new head position to the snake.
If the head reaches the food, the food is repositioned randomly, and the snake grows.
If the head does not reach the food, the snake moves forward without growing.
Clears the screen and redraws the snake and food.
Sets a timer to call move() again after 100 milliseconds.

---------------------------------------------

Setting Up the Game

---------------------------------------------

setup(420, 420, 370, 0)
hideturtle()
tracer(False)
listen()
onkey(lambda: change(10, 0), 'Right')
onkey(lambda: change(-10, 0), 'Left')
onkey(lambda: change(0, 10), 'Up')
onkey(lambda: change(0, -10), 'Down')
move()
done()
setup(420, 420, 370, 0): Sets up the game window with dimensions 420x420 pixels and positions it on the screen.
hideturtle(): Hides the turtle cursor.
tracer(False): Turns off automatic animation to improve performance.
listen(): Sets up the window to listen for key presses.
onkey(lambda: change(10, 0), 'Right'): Changes the snake's direction to the right when the 'Right' key is pressed.
onkey(lambda: change(-10, 0), 'Left'): Changes the snake's direction to the left when the 'Left' key is pressed.
onkey(lambda: change(0, 10), 'Up'): Changes the snake's direction to up when the 'Up' key is pressed.
onkey(lambda: change(0, -10), 'Down'): Changes the snake's direction to down when the 'Down' key is pressed.
move(): Starts the snake's movement.
done(): Keeps the window open until it is closed by the user.

---------------------------------------------

Usage

---------------------------------------------

Run the script.
Use the arrow keys to control the direction of the snake.
Eat the green food to grow the snake.
Avoid running into the walls or the snake itself to keep playing.
