# Part 0: Why Visual Scripting?

*Contents*: [What is Visual Scripting?](#what-is-visual-scripting) | [The Benefits](#the-benefits) | [The Drawbacks](#the-drawbacks) | [TL;DR](#tldr)

## What is Visual Scripting?

**Visual scripting** is a way to represent game logic that uses visual elements instead of traditional code. It's a common tool in modern game engines, built to help non-programmers understand and modify what happens in a game.

The specifics vary a bit across engines. Programs like Scratch have users assemble lego-like blocks together, while Unity and Unreal have users draw connections between nodes. I'll be focusing on Unity's version, but the core ideas here should carry over to other systems. 

## The Benefits

### Designer Friendliness

With visual scripting, designers can manipulate the logic of a game without diving into the specifics of the code. 

This is especially useful for rapid iteration, where designers can change aspects of the game and quickly replay it. This can help designers quickly experiment with new concepts, or perfect existing ones.

### Representing Sequential/Branching Logic

For certain jobs, visual scripting stands out as the most effective approach. Here's one example.

Imagine that you're making a choose-your-own-adventure text game with lots of branching choices. You need to represent the entire game's content (dialogue / choices for each branch). What are your options?
- A single text file
  - Will need lots of skips from one line to another. Following the logic will get difficult, fast.
- Multiple text files
  - Can end in massive file structures.
  - Will likely create lots of dependencies where exact file locations are essential, and slight rearrangement will break everything. 
- (Unity-Specific) Creating Monobehaviour scripts to hold the dialogue
  - Can easily bloat the size of a scene.
  - Can be messy to navigate the Inspector, looking for the right component to change.
- (Unity-Specific) Creating ScriptableObject instances to hold the dialogue
  - Searching for a specific piece of dialogue can be very difficult.
  - Like with multiple text files, can end in massive file structures.

In comparison, Unity's visual scripting system feels like a natural fit. Its node-based system shows a clear sequence of events, so you can understand exactly what happens when. Additionally, representing branches is easy; you can just go to a different node under a certain condition. Bloat is also less of an issue, since a node can contain other, "smaller" nodes.

Of course, the choose-your-own-adventure game was just an example, but it captures an important principle:

***In general, visual scripting works best for games whose high-level logic is sequential!*** (e.g. moving from one piece of dialogue, to the next, to the next...)

As a rule of thumb:
- *Good for Visual Scripting*: This happens. Then that happens. Then that happens.
- *Less Good for Visual Scripting*: This thing is revolving around this thing, and if you press A then this thing happens, while the whole time this other thing is happening.

This isn't to say it could *never* be worthwhile to use visual scripting for the second case. In general, though, the closer your game is to a sequence of discrete events, the more neatly it will fit into the visual scripting workflow.


## The Drawbacks

### Performance

The most obvious downside of visual scripting is its speed. In Unity, [It can be hundreds of times slower than C# code!](https://www.youtube.com/watch?v=Lyw98dl5acE) If your game performance needs to be perfected down to the microsecond, that will likely be a deal-breaker.

There *are* ways to limit this problem, though. For one thing, you can break your game logic into layers--the outer layer being visual scripting, and the inner layer being C# code. Since visual scripting nodes can call C# scripts, you can treat the visual scripting nodes as an "interface" for designers to interact with, while putting the heavier underlying logic in C#.

### Inappropriate Use

When you learn visual scripting, it's tempting to use it for everything. However, remember that the key benefit of visual scripting is its intuitiveness and designer friendliness. 

Sometimes, visual scripting can make something look more complicated than it is. This is especially true for math-heavy tasks like player movement or physics.

In general, visual scripting should only be used if its inclusion makes it easier for designers to work on your game. The more you use visual scripting, the better you'll intuitively understand what are and aren't good use cases for it.

## TL;DR

Visual scripting can be valuable for projects that...
- Are heavily designer-driven, and/or would benefit from a rapidly iterative approach to design.
- Generally operate with sequential logic.
- Can take at least a mild hit in performance.

Visual scripting can pose a problem when it...
- Is used for complex math (or anything else that would be simpler with some C# code).
- Is used on highly performance-intensive projects.

## References

https://www.youtube.com/watch?v=Lyw98dl5acE

## Next Lesson

[Part 1: Setting Up Visual Scripting](1_SettingUpVisualScripting.md)

