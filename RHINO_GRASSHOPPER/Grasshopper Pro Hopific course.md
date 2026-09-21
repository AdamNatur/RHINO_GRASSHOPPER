# Grasshopper Pro Hopific course

## Roadmap

![[resources/Pasted image 20251116142507.png]]

## Cheat Sheet

![[Hopific - The Ultimate Grasshopper Keyboard Shortcuts CheetSheet.pdf]]

---

## Prerequisite: Grasshopper Foundations

### The Grasshopper Interface

#### Shortcuts

| Shortcut                    | Action                   |
| --------------------------- | ------------------------ |
| `Drag+Alt` (on components)  | duplicate object         |
| `Ctrl+Q`                    | preview on/off           |
| `Ctrl+G`                    | group objects            |
| `Drag+Alt` in an area       | shift between components |
| `Ctrl+Shift` (on wires)     | move wires               |

#### Wire types

There are three main wire types:

| Wire                 | The data stream contains                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| **Thin continuous**  | a single item (for example a number or a curve)                                                   |
| **Thick continuous** | multiple items, all in the same list (more on that in the data module later in the course)        |
| **Thick, dashed**    | multiple items in multiple data branches, i.e. a list of lists                                    |

![[image.png]]

> [!tip]
> Wire types give you a quick, intuitive picture of the data structure flowing between components, without having to attach a Panel or Param Viewer to look 'inside'.
>
> In complex scripts, checking the wire type before you make a connection can save you from long computation times or crashes caused by mismatched data.

### Essential Components

> [!abstract] Used components
> `Curves` · `Panel` · `DivideCurve` · `Number slider` · `Expression component`

#### Panels

Two components to know:

- **Data Viewer** - lets you inspect the data inside a component or output before connecting it further, and see what kind of data it contains. It is part of the Diagnostic Tools.
- **Text editor and container** - lets you type data into a Panel and store it, for example several numbers to feed different components. Put each value on its own line to create multiple items.

#### Number slider

The Number slider lets you input numbers.

Ways to create one:

- from the toolbox menu at the top, like any other component
- by typing in the workspace, like any other component
- by using special typing shortcuts:
  - **Single number** - creates a slider from 0 to 10ⁿ, where n is the number of digits.
    For example, `25` creates a slider from 0 to 100, and `356` creates a slider from 0 to 1000.
    Adding a decimal point and decimals sets the slider's precision.
  - **Interval**, like `10..100` - creates a slider from 10 to 100.
    If a number has decimals, the slider gets that precision. If both do, the higher precision wins.

#### Script to divide curves into equal parts

![[resources/Pasted image 20251110135701.png]]

### The Grasshopper Design Process

![[resources/Pasted image 20251110145320.png]]

#### First Script

> [!abstract] Used components
> `Point component` · `Circle component` · `Number slider` · `Divide curve` · `NURBS Curve` · `Surface` · `Move` · `Unit Z` · `Series` · `Panel` · `Extrude` · `Rotate`

![[resources/Pasted image 20251111092046.png]]

![[resources/Pasted image 20251111092224.png]]

> [!note]
>
> - In components that use a plane to define their location (circle, point, etc.), you can plug in a point instead.
> - Grasshopper converts data between component types automatically. For example, a closed contour can be plugged straight into the Surface component to get a surface.
> - Almost all components have default values.

#### NURBS curvatures

![[resources/Pasted image 20251111093544.png]]

#### Assignment

---

## Module 1. Thinking in Data

### Introduction to Thinking Data

Data structures are the core of Grasshopper. They let you change many objects at once, for example through a list. In Rhino, by contrast, you can run only one command at a time and modify only one or two objects at a time.

### Intro to Lists

> [!abstract] Used components
> `Curve` · `Explode` · `Panel` · `Middle Point` · `Points List` · `Text3d Tag` · `Series` · `List length` · `Number slider` · `Cull Pattern` · `Length` · `Expression` · `Point In Curve`

#### Lists

![[resources/Pasted image 20251116144135.png]]

In Rhino, every object has its own index (position), and selecting an object picks that index. In the Rhino viewport we cannot work with indexes directly, but Grasshopper gives us direct access to them through lists of items (objects).

![[resources/Pasted image 20251116144754.png]]

A list has three parts: **index**, **objects** and **data path** (the list name). A list can store any type of data: numbers, geometry, true/false values, etc.

#### Script to numerate edges of rectangle and locate numbers in the middle of it

![[resources/Pasted image 20251116152632.png]]

> [!note]
> The Wrap property of List Item makes the index cycle, so a missing index never causes an error. For example, if you request index 4 but the highest index is 3, you get index 0, because wrap is enabled. I think the formula is: $\text{resultIndex} = \text{inputIndex} \bmod \text{listLength}$

#### Script for Exercise

![[resources/Pasted image 20251117180304.png]]

#### Result

![[resources/Pasted image 20251117180416.png]]

Green-highlighted lines are the lines whose middle points lie inside the curve (rectangle).

### Lists Assignment

#### Task

![[resources/Pasted image 20251117180556.png]]

#### Script

I used the script from the previous lesson. The only difference is shown in the picture below. The core component is **Shift List**, which shifts a list by a given number of steps; here the list of points was shifted by one.

![[resources/Pasted image 20251117182720.png]]

#### Result

![[resources/Pasted image 20251117183025.png]]

### Lists Design Exercise

#### Task

![[resources/Pasted image 20251121091659.png]]

> [!abstract] Used components
> `Curve` · `Explode` · `Panel` · `Middle Point` · `Points List` · `Number slider` · `Cull Pattern` · `Expression` · `Loft` · `Extrude` · `Flip matrix` · `Line` · `Weave` · `Flip curve` · `NURBS Curve` · `End Points`

#### Script

![[resources/Pasted image 20251121122009.png]]

> [!note]
> Instead of **Reverse List**, you can use **Flip Line**, which swaps the start point and the end point.

> [!note]
> **Flip Matrix** swaps rows and columns when working with a list of lists. It works only for a square matrix, where the number of columns equals the number of rows.

### Intro into Data Trees

#### Lists

![[resources/Pasted image 20251123153229.png]]

Lists are data structures. Every component performs certain operations, but it also contains a set of data, whether geometry, numbers, etc.

![[resources/Pasted image 20251123161845.png]]

Every component can be thought of as a database.

#### Types of databases

![[resources/Pasted image 20251123162243.png]]

We can access each part of a list by its name - the index. Every item has its own index.

![[resources/Pasted image 20251123162355.png]]

- **Database** - "Data Tree": a list of lists.
- **List** - "Data Branch": a subpart of the database that contains items.
- **List name** - "Data Path": technically, the list's absolute index in the database.

#### Param Viewer

![[resources/Pasted image 20251123163239.png]]

The Param Viewer component displays the structure of a list. Unlike the Panel, which shows the items inside, Param Viewer shows only the data structure: the number of branches and the number of items in each.

![[resources/Pasted image 20251123165534.png]]
![[resources/Pasted image 20251123165631.png]]
![[resources/Pasted image 20251123165607.png]]

#### Graphical representation of the lists

![[resources/Pasted image 20251123165716.png]]

#### Graphical representation of the lists

![[resources/Pasted image 20251123170712.png]]

Grasshopper uses different wire styles between components to show the type of data structure:

- **Single line** - the output holds a list with one item.
- **Double line** - the output holds a list of several items.
- **Dashed line** - the output holds a list of lists, with multiple branches.

Organizing data into lists is called **grafting**. Grasshopper does it in two ways:

- **Auto-grafting** - whenever a component produces more than one output element for each input element, Grasshopper bundles them into a list for each input element.
- **Manual grafting** - the user edits lists and data trees by hand.

![[resources/Pasted image 20251123172011.png]]

A Data Tree is just a list of lists with several levels. Each level has a number (index), and the deeper a list sits in the tree, the longer its path, as shown in the picture above.

### Modifying Data Trees

#### Trim Tree

![[resources/Pasted image 20251123173536.png]]

Trim Tree deletes the last level (data path) of the tree, which merges the lists of that level, as shown in the picture above.

#### Graft Tree

![[resources/Pasted image 20251123174134.png]]

Graft Tree creates a separate list for each item in the source data branches.

#### Flatten tree

![[resources/Pasted image 20251123174640.png]]

Flatten Tree erases the data structure and puts everything into one single list, no matter what the structure was before.

#### Simplify tree

![[resources/Pasted image 20251123174931.png]]

Simplify Tree removes redundant path levels. It doesn't change the data structure itself, only the data path, making it simpler and more readable. We also use it to make sure the data streams we want to join or match have the same path (name).

We use all these operations to control and manage data matching.

#### Data matching

![[resources/Pasted image 20251123181041.png]]

![[resources/Pasted image 20251123181103.png]]

![[resources/Pasted image 20251123181126.png]]

![[resources/Pasted image 20251123181150.png]]

![[resources/Pasted image 20251123181207.png]]

![[resources/Pasted image 20251123181227.png]]

![[resources/Pasted image 20251123181243.png]]

### Data Tree Example

![[resources/Pasted image 20251123192013.png]]

### Data Tree Assignment

### Data Trees - Design Exercise

---

## Module 2. Mastering in Geometry

### Intro to Geometry Type

In this module, I learned about different geometry types and how to work with them. The idea is to move from the basic geometry unit, curves, to surfaces, and then to volumes.

### Intro to Curves

> [!abstract] Used components
> `Evaluate curve` · `Reparameterize` (in the component options) · `Direction` · `Curve Domain`

![[resources/Pasted image 20251124120345.png]]

Rhino is NURBS modelling software. NURBS geometry lets us create mathematically precise geometry, and smooth geometry when needed.

![[resources/Pasted image 20251124121136.png]]

Control points are an essential part of any NURBS geometry: they define its shape and let you control it. Let's start with the NURBS curve.

| Curve Degree | Continuity | Description                                                              |
| ------------ | ---------- | ------------------------------------------------------------------------ |
| **1**        | positional | control points are connected to each other with straight lines           |
| **2**        | tangential | control points define straight lines, and the curve bends to be tangent to them |
| **3**        | curvature  | creates a smooth transition between the control points                   |

You can change a curve's degree at any time. In practice, we use only degrees 1 and 3, to get polylines and smooth curves respectively.

![[resources/Pasted image 20251124122108.png]]

After degree, the most important parameter is **Curve Direction**. It defines the curve's orientation, i.e. where it starts and where it ends. We need it when we want to get a point on the curve.

![[resources/Pasted image 20251124122337.png]]

To get a point on a curve, we use the curve parameter: a value within the curve domain, often thought of as relative, from 0 to 1. But the domain doesn't have to be 0 to 1. It is simply defined by its lowest (minimum) and highest (maximum) values.

![[resources/Pasted image 20251124123211.png]]

Because the domain differs from curve to curve, we **reparametrize** the curve, i.e. redefine its domain to [0, 1]. It is similar to vector normalization, but for the curve domain, and it means we no longer need to know the domain of each curve we work with.

When we evaluate a point on a curve, we get not only the point but also the tangent vector at that point. This is useful for creating geometry that responds to the shape of the curve.

![[resources/Pasted image 20251124123355.png]]

![[resources/Pasted image 20251124123649.png]]
![[resources/Pasted image 20251124123722.png]]

### Curves - Arrays

---

## Module 3. Essential Algorithms

---

## Wrapping Up
