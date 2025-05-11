---
title: Game Loop
draft: false
publish: false
tags:
  - 📬
  - game-development
date: 2025-04-27
---
The game loop makes interactive programs possible. Instead of just running a program and just wait for it output and then it ends, the program can interact with the user. The very first interactive programs were text based role playing games. Modern UI applications are actually really similar to these games. Instead of waiting for text input, these programs are waiting for user input in form of key presses or mouse movements. At the same time the animations, effects and game logic are running. 

A basic game loop looks like this:
```C
while (true)
{
	processInput()
	update()
	render()
}
```

The game loop also has the job to run the game in a constant speed even if the hardware on which it is run is different for every user. If you use the basic game loop above the game will run in different speeds on different machines. One way to solve this is to just give the game a static frame rate. This approach requires that you can handle all your game logic in the time the frame gives you. On 60FPS this is 16ms.

```C
while (true)
{
  double start = getCurrentTime();
  processInput();
  update();
  render();

  sleep(start + MS_PER_FRAME - getCurrentTime());
}
```

The problem with this approach is, when your logic needs longer than 16ms to compute, your game slows down.

We can make our time steps variable or fluid: We could measure how much real time it takes to process the game logic and then continue the game state that much forward. In the following example you see that we put the elapsed time into the update function:

```C
double lastTime = getCurrentTime();
while (true)
{
  double current = getCurrentTime();
  double elapsed = current - lastTime;
  processInput();
  update(elapsed);
  render();
  lastTime = current;
}
```

Problem with this approach is, that the game gets non-deterministic. On different machines a different amount of calculations the game engines processes in a second. Game engines use floating point mathematics, therefore those calculations have rounding errors. On a slower machine the rounding errors occur less than on a faster machine. So two players could get out of sync.

The solution is to differentiate the update and render loop. The render loop can be constant while the update loop should play catch up to the real time passing.

```C
double previous = getCurrentTime();
double lag = 0.0;
while (true)
{
  double current = getCurrentTime();
  double elapsed = current - previous;
  previous = current;
  lag += elapsed;

  processInput();

  while (lag >= MS_PER_UPDATE)
  {
    update();
    lag -= MS_PER_UPDATE;
  }

  render();
}
```

The update loop runs on a fixed time loop to catch up to the real time passing. Yo need to make sure that your update logic fits into the `MS_PER_UPDATE` time frame. 
See: (https://gameprogrammingpatterns.com/game-loop.html)[Game Loop]

