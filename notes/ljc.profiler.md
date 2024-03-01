---
id: wi6q59zkivy4h3n4aq88r0o
title: Spark Profiler
desc: ''
updated: 1709273702798
created: 1682131570817
---
If you're experiencing lag in this modpack, this is a guide on how to pinpoint the lag (or at the very least help me help you.)

If it isn't already. Close your game and install [Spark](https://spark.lucko.me). You can test to see if it's installed by running `/sparkc` in-game, if it returns command not found, you need to install it.

## Finding Lag
After installing Spark we need to determine a few things. Firstly, how long our lag spikes last, and then we can profile our game to actually find the source of the problem.

### 1. Monitoring Ticks
First up we need to start our Tick monitor. Achieve this by running `/sparkc tickmonitor`

![](./assets/images/2023-04-21-23-29-28.png)

![](./assets/images/2023-04-21-23-30-30.png)
After the Initial analysis completes you may find some issues about GC, you can ignore this for now. Java's Garbage collector is... Garbage... We are looking for a HUGE spike in ticks.

![](./assets/images/2023-04-21-23-33-13.png)
This is a pretty Sizeable spike! so much so it kicked me from the server! (hence the dimmed screenshot)

Now we can run our profiler to try and find the actual source of the lag!

### 2. Profiling the Game
Now that we have some numbers we'll try and only capture the major spikes! First we need to take the lowest large spike, round it down to the nearest 50 and then start profiling it!

In the case above, our lowest significant spike was 106.76ms, so we'll round it down to 100

![](./assets/images/2023-04-21-23-38-24.png)
![](./assets/images/2023-04-21-23-38-51.png)

Now our profiler is running, When any spike happens over 100ms it will be captured in our profiler! We want to try and recreate the lag as best we can (while avoiding a crash!).

After we re-produce our spike, we can run `/sparkc profiler stop`
![](./assets/images/2023-04-21-23-42-05.png)

And our report will be generated!
![](./assets/images/2023-04-21-23-42-25.png)

While we're at it let's also disable the tickmonitor
![](./assets/images/2023-04-21-23-43-14.png)

Now we just click the link, and either open in browser to view it or copy to clipboard to throw at Java.
![](./assets/images/2023-04-21-23-44-11.png)

Examining the Profiler report is out of scope for this guide! You can instead follow the documentation from the [Spark page!](https://spark.lucko.me/docs/Using-the-viewer)

This guide was mostly derived from the Spark documentation anyway. Just in a more verbose manner.