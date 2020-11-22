# Why are we studying this ?
We assume this will teach us basic how to's on basic math principles such as
- Scaling and Ratios 
- Vectors and Dot Products
- Trigonometry
- Degrees and Radians
- Cross Product
- Local vs World Space and Transformations
- Lerp
- Derivatives 
- Frame rate independence 

---


### Scaling and Ratios  
Let's say there is a **Health Bar** 
![[healthbar.png]]
And let's say there's a player who has 40 percent of that health left, how much portion of the health be occupied over the health bar.
For that we first need to know the width of the health bar
![[PixWidthBar.png]]
Let's consider `PixelWidthBar` as the width of Health Bar in **Pixels**
And find the current health value in percentage `pctHealth`, we just divide the current health `healthCurrent` value by the total health value, Let's assume the total health value as 100 `healthMax`.
$$pctHealth = healthCurrent/healthMax$$

If you multiply `pctHealth` with the `PixelWidthBar` you'll get the area covered by the `healthCurrent` over `healthMax`

$$PixelWidthBar * pctHealth$$

![[healthCurrentVsMax.png]]

Now it'd be even better if we make a **Sprite** cover over the part of the **Health Bar** that represents the current health of the player.

So we download a sprite from a random website, this sprite has a total of **4 pixel width** (We ignore height for now, since our goal only depends on the width).
![[Spritewith4width.png]]
Thus
$$Pixel/Sprite$$$$= 4/1$$$$= 4$$
But the problem here is, inorder for us to use resize this sprite we need to change the width of the sprite from pixel per sprite into sprite per pixel because we cannot directly multiply 4 with the overlaying value for the current health we just found. We need to see how much sprite is there in a single pixel and multiply that with the value. 

$$Pixel/Sprite  Sprite/Pixel $$$$4/1 = 1/4$$$$ SpritePerPixel = 0.25    Sprite/Pixel$$

If you apply this value to the sprite then the sprite will accurately occupy the amont of **Current Health** over the **Health Bar**

![[CurrHealthWithSprite.png]]

---
### Vectors and Dot Products 
#### Vectors : 
**What is a Vector ?**
A vector has both magnitude and direction.
![[Defenition of a vector.png]]
#### 1D - Vector
 A vector lying over only one axis 
![[1D-Graph(1).png]]
in this condition the X axis.

Here there is a 1-D vector called `a` with a length of **2**
![[1D-Graph-a.png]]
#### 1D - Vector addition
![[1D-vector addition-Step 1.png]]

Now there is a new vector called `b` with a length of **3**, now we can add both vector `a` and vector `b`. This will result in a new vector that is a sum of a and b (i.e) `a+b`. We can easily visualize by keeping one vector over an another like this.
![[1D-vector addition-Step 2.png]]

Now the sum of both will form a new line that will be the exact length of both the vectors combined called `c` this will be a length of **5**.
![[1D-vector addition-Step 3.png]]

You can also do it like this 
$$a = 2$$ $$b =3$$$$a+b = c$$$$2 + 3 = 5$$

Thus even in this way Vector `c` can be proven as **5**

####  2d-Vector
A vector that has 2 Dimensions one over the X and one over the Y

![[2D Vector.png]]

Vector A is a 2D vector
![[A-2D Vector.png]]
Same as earlier you can observe the coordinates of the vector by understanding the distance covered by the vector in both axis.
![[A-2D Vector-Measured.png]]
THus as you can see the vector coordinates of A is (4,2)

####  2D Vector Addition

Same as 1D vectors, Vector addition can be performed over two vectors to attain a new vector of combined size.
Here lies 2 Vectors called A and B.
![[AB-2D VectorsV2.png]]
Where A is ``(4,2)``
and B is `(1,2)`
You can visualize adding two vectors same as a 1D Vector.
Just plcae one vector over an another and you will get the distance of how much the resultant vector will cover.	
![[ABResultant-2D VectorsV2.png]]
So you can see the resultant vector being the cumulative quantity of both A and B vectors.
We shall call this the Vector C which is ``(5,4)``
![[C-2D Vector.png]]
You can also solve this like you did Vector 1 
$$A = (4,2)$$
$$B = (1,2)$$
$$A+B = (A.x+B.x,A.y+B.y)$$
$$ = (4+1,2+2)$$
$$C = (5,4)$$
Which is same as what we visualized in the graph.

####  2D Vector Subtraction
This uses the same strategy as the vector addition

Here we use the same example 
![[AB-2D VectorsV2.png]]
But instead of doing A+B we will perform A-B.

**Before Visualization lets first try to solve it:- **
Since it is -B we need to multiply all of B by -1 `(1,2)*-1` resulting in ``(-1,-2)``
If you then put it up against A `(4-1,2-2)` you will get `(3,0)` which will be the new resultant vector 

We can visualize it the same way, Since the B is negated it will be pointing to the opposite direction which will be `(-1,-2)`
![[Negated B Vector-Measured.png]]
Now put this over A and visualize like we did earlier for the addition	
![[A-BResultant Vector-Measured.png]]
You can see it points to the same  `(3,0)` like we calculated before .

####  Finding Distance between Two Vectors

Finding the distance between two points will actually help you find the [Euclidean  distance](https://en.wikipedia.org/wiki/Euclidean_distance) between the two points. 
To get the distance between two vectors, you need to first do vector subtraction. Like we have learned earlier vector subtraction helps us to find a new vector that is actually a  result of one vector negated from another vector but this vector also represents distance between the two vectors!!!
We would require a formula to procure the actual distance from the two vectors besides just negating one vector from another vector

**The formula is $\sqrt{X^2+Y^2}$**

**Where is the subtraction in here ?**
To acquire the `X` and `Y` you'd need to do the subtraction operation between the vector points you'd like to determine the distance for and on their appropriate axes.
$\sqrt{(A.x-B.x)^2+(A.y-B.y)^2}$

Let's take the subtraction graph that we solved in the previous topic
![[Distance between A and B.png]]

To find the distance between A and B as proposed earlier we subtract A - B.
![[A-BResultant Vector-Measured.png]]

**PRO TIP** : You can also do `B-A` if you'd like, the formula can be changed to $\sqrt{(B.x -A.x)^2+(B.y-A.y)^2}$ and it'd get you the same result as `A-B`

**How ?**
If you could look ta the graph even with inverted subtraction the distance of C still remains to be the same.
![[B-A Resultant Vector-Measured.png]]

Thus If you could fill the A.x, B.x, A.y and B.y in the distance formula, you'll get a single number that is not a vector which represents the [Euclidean  distance](https://en.wikipedia.org/wiki/Euclidean_distance) between two points.

#### Finding Direction between two vectors
 Target-source for direction
 you can change the length or a vector by not changing it's direction by multiplying the value that you want your vector's length to be by the normalised vector of the vector you wanna change the direction of.
 Dot product - helps you to easily find opposite direction or perpendicular or direction facing vectors, 80 % of the time I use dot product to find similarity between vectors is what freya holmer says
 
 dot product being called as a scalar projection- find dot for a  normalised and non normalised vector 
 