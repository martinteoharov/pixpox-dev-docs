 ## The "Command" Design Pattern



### Explanation

The "command" pattern is a simple way to map actions to functions. 

> Somewhere in every game is a chunk of code that reads in raw user input — button presses, keyboard events, mouse clicks, whatever. It takes each input and translates it to a meaningful action in the game:
> ![[Pasted image 20220722164326.png]]

````c++
void InputHandler::handleInput()
{
  if (isPressed(BUTTON_X)) jump();
  else if (isPressed(BUTTON_Y)) fireGun();
  else if (isPressed(BUTTON_A)) swapWeapon();
  else if (isPressed(BUTTON_B)) lurchIneffectively();
}````



> To support that, we need to turn those direct calls to `jump()` and `fireGun()` into something that we can swap out. “Swapping out” sounds a lot like assigning a variable, so we need an _object_ that we can use to represent a game action. Enter: the Command pattern.



### Sources
https://gameprogrammingpatterns.com/command.html



### Pros & Cons 

| pros         | cons |
| ------------ | ---- |
|  |  |
