# Critter-World-Simulation

## Overview

This is the final project for CS 2112: Objected Oriented Programming and Data Structure - Honors offered at Cornell University. In this project, we discussed, designed, and implemented a Critter World Simulation program, which involves 

- customizable species / creatures that are known as "Critters", 
- a hexagonal world set up with evolving time steps, 
- as well as a Graphical User Interface to demonstrate the flow of time and world behaviors. 

As an overview, we have designed and implemented: 

- A Parser, Abstract Syntax Tree, and an Interpreter for a Context Free grammar supporting various different features in the critter "genome" 
- A modeling world simulator that documents the world state
- A Graphical User Interface using using JavaFX  
- Shortest Path search for food using Dijkstra's Algorithm





### Critters

#### Supported Behavior

Each critter is able to 

- **wait**: The critter waits until the next turn without doing anything except absorbing solar energy.
- **move forward / backward** : A critter uses some energy to move forward to the hex in front of it or backward to the hex behind it. If it attempts to move and there is a critter, food, or a rock in the destination hex, the move fails but still takes energy
- **turn left / right:** rotate 60 degrees right or left.
- **eat**: The critter may eat some of the food that might be available on the hex ahead of it, gaining the same amount of energy as the food it consumes. It eats as much as it can; when the hex has more food than the critter can absorb, the excess food is left on the hex
- **attack**: It may attack a critter directly in front of it. The attack removes an amount of energy from the attacked critter that is determined by the size and offensive ability of the attacker and the defensive ability of the victim.
- **grow**: A critter may use energy to increase its size by one unit.
- **bud**: A critter may use a large amount of its energy to produce a new, smaller critter behind it with the same genome (possibly with some random mutations).
- **mate:** A critter may attempt to mate with another critter in front of it. For this to be successful, the critter in front must also be facing toward it and attempting to mate in the same time step. If mating is successful, both critters use energy to create a new critter of size 1 whose genome is the result of merging the genomes of its parents. Unsuccessful mating uses little energy
- **serve**: A critter may convert some of its own energy into food added to the hex in front of it, if that hex is either empty or already contains some food.

and sense the surroundings with built in sensors. 

#### Behavior Definition

Each Critter "species" is defined by a set of instructions that direct their behavior. This program is formed by a simple set of context free grammar, where a *command* is executed if and only if the *condition* is satisfied. 

<img src="/Users/angelachao/Library/Application Support/typora-user-images/image-20221011154746316.png" alt="image-20221011154746316" style="zoom:50%;" /> 



#### Language Parsing

This instruction language is supported by a Tokenizer, a Parser, an Abstract Syntax Tree, and an Interpreter. 

__Tokenizer: __ The tokenizer is improved so that it supports Java-style comments. This was made possible by the BacktrackScanner in the package easyIO because the reader is allowed to go back to a previous mark.

__Parser: __ The parser parses the input program into our design of the Abstract Syntax Tree, then creates the underlying genome that dictates each Critter's Behavior

__Abstract Syntax Tree: __ An underlying representation of the critter genome, determines the appropriate action at appropriate times

__Interpreter: __ Interprets the said critter genome each time step, and executes the appropriate actions dictated by the AST 



### World Model: 

The world in which critter behavior is simulated is represented by a hexagonal grid

