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
**1D - Vector**
 A vector lying over only one axis 
![[1D-Graph(1).png]]
in this condition the X axis.

Here there is a 1-D vector called `a` with a length of **2**
![[1D-Graph-a.png]]
**1D - Vector addition**
![[1D-vector addition-Step 1.png]]

Now there is a new vector called `b` with a length of **3**, now we can add both vector `a` and vector `b`. This will result in a new vector that is a sum of a and b (i.e) `a+b`. We can easily visualize by keeping one vector over an another like this.
![[1D-vector addition-Step 2.png]]

Now the sum of both will form a new line that will be the exact length of both the vectors combined called `c` this will be a length of **5**.
![[1D-vector addition-Step 3.png]]

You can also do it like this 
$$a = 2$$ $$b =3$$$$a+b = c$$$$2 + 3 = 5$$

Thus even in this way Vector `c` can be proven as **5**

