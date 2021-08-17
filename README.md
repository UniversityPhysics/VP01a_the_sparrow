# The sparrow and the hawk, part 1
Introduction to VPython. The sparrow, fleeing a hawk, just wants to get home. It is traveling at it's maximum speed. 

## Our development environment: Glowscript.org

You don't need to install anything! Just use http://GlowScript.com. Southern students can log in with their southern email. To submit your assignment this time, you will simply paste in a URL to your glowscript code. Make sure you choose a PUBLIC folder and not PRIVATE, to be sure that it is not hidden from me in a private folder. 

We will use the visual package for Python, referred to as VPython. There is a lot of helpful reference material and tutorial videos available at http://VPython.org. 

## "All I ever did was copy and paste code, I don't know how to do this next assignment"
Each of these computational assignments is a stepping stone, building toward more challenging projects later in the semester. Be advised that students are sometimes surprised when they are expected to use what they learn on one assignment in the next assignment. 

Advice:
*Think as you type, don't copy and paste.
*If something doesn't make sense in this class, ask for help right away.



Yes, understanding how to code physics will be on the test, so that won't be a surprise.


## Draw 3D shapes in VPython

Let's build a birdhouse! VPython makes it easy to make a box shape: if you click help and select box, this is the syntax:

```
birdhouse = box(pos=vector(x0,y0,z0),
       length=L, height=H, width=W)
```

Let's make it a cube with side length `0.1` and place it at a position `vec(5, 1, 0)`. You can also specify the color to be `color=color.red`.

Checkpoint 1 ("Run this program", check for errors)

I'm also going to add a flattened cylinder to be the ground. Your code could look like this.
```
birdhouse = box(pos=vec(5,1.0,0), length=0.3, height=0.3, width=0.3, color=color.red)
ground = cylinder(pos=vec(0,0,0), axis=vec(5,0,0),height=0.1)
```
Add a pole, the position is at the ground, and the axis is pointing from the ground pointing up. Adjust the axis property so that the pole connects to the birdhouse
```
pole = cylinder(pos=vec(5,0,0), axis = vec(?,?,?),radius=0.03,color=color.red)
```
Use control-mouse to pan and zoom. 
 
Checkpoint 2 ("Run this program", check for errors)

Let's represent the sparrow as a sphere. For help on objects such as a sphere, click on help in Glowscript.org. Here is a link to the documentation. https://www.glowscript.org/docs/VPythonDocs/sphere.html
```
sparrow = sphere( radius=0.1, pos=vec(x,y,z))
```

## Making motion diagrams by leaving a trail

VPython has an easy way to let the sphere make a "trail", which will allow us to make a motion diagram. Just paste in this line o

```
sparrow = sphere(radius = 0.1, make_trail=True, trail_type="points",
              interval=1, retain=50)
```

Now, in computer programming, the sphere is an object and you have so far created box, sphere, and cylinder objects. Objects have properties, and so far you have set those properties as arguments. Another way to do that is after creating the object. You created the sparrow but you didn't set the position. In the next line, set the position like this.
```
sparrow.pos = vec(0,1,0)
```
Checkpoint 3

Run the code to see your scene and verify that the dart position is at the top of the person.


## Position update form of average velocity equation
It will probably help to read Matter & Interactions chapter 1 section 11 before doing this activity. The first chapter is [freely available online here](https://matterandinteractions.org/wp-content/uploads/2016/07/Chapter1-InteractionsandMotion.pdf). Read their excellent explanation of how the definition of average velocity can be written in "update form". Instead of defining a new position vector at each update, a computer program can simply store the updated postion `r+v*delta_t` in the old position using the assignment statement `r=r+v*delta_t`. As the authors explain, this is not a mathematical statement! This is an instruction to calculate `r+v*delta_t` and store the result in the memory address for `r`. This statement works just as well if `r` and `v` are vector objects.

Apply what you have learned to update the position of a sphere representing the sparrow, such as in the code sample below.

```

delta_t=0.1
t=0
sparrow.velocity=vec(3.0,0,0)

while t<2:
  rate(1.0/delta_t) #slow the execution of the loop down so it runs every delta_t seconds
  sparrow.pos=sparrow.pos + sparrow.velocity * delta_t
  t=t+delta_t
  print(t,sparrow.pos)
```

Get the sparrow to the birdhouse: experiment with the loop to stop the animation when the sparrow is closest to the birdhouse.

Checkpoint 4

## The hawk!

Create a hawk like this
```
hawk = sphere(radius = 0.2, color = color.yellow, make_trail=True, trail_type="points",
              interval=1, retain=50)
hawk.pos = vec(-5,1.5,0)
hawk.velocity = vec(4,0,0)
```
Does each line make sense to you? If not, raise your hand.

Modify your animation loop to update `hawk.position` using `hawk.velocity`, similar to the way you updated `sparrow.pos`. This is a one-liner.

Experiment with the velocity of the hawk so that it runs into the birdhouse just when the sparrow has safely made it home.




