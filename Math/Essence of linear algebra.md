#  Essence of linear algebra


## Ep:1 Vectors, what even are they?

Vectors can be defined using three different perspectives, where each type is a description of their approach into understanding the vectors.

#### Different aproaches that define what vectors are
- **Physicist's approach (Geometric representation)** Where a vector is seen as an arrow that determines both direction and length(magnitude) and it's origing doesn't have be in the actual origin and this vector can lie anywhere in space.
 ![[Direction and Mag.png|200]]
- **Programmer's approach (Numerical representation)** Where a vector is a 2 dimensional array capable of representing a vector in terms of numerical value.
	 This idea has been further extended by the programmer's to actualize data sets too. Where x axis stores a value of particular intention and y of an another. Here x could be age of an employee and y could be his daily wage.

$\begin{bmatrix}x\\y\end{bmatrix}$ $\begin{bmatrix}26\\1000\end{bmatrix}$  


- **Mathematician's approach** This is the most interesting approach and the approach we have been using as gamedeveloper, where we accept both of these views and use them interchangeably.

*Even in the [[Math for GameDev]] series you can witness us explaining things in both **Physicist's approach** and **Programmer's approach**, you can view it under  [[Math for GameDev# |Vectors and Dot Products]]*

#### The way we do coordinates in vector algebra
In linear algebra we almost always will have the vectors connected to the origin in an $x,y$ coordinate system unlike the Physicist's approach where the vectors can be anywhere. Like we have explained in the  [[Math for GameDev#2d-Vector|2D Vectors]] topic the $x,y$ of the vector will determine how a vector has travelled in $x-axis$ and  $y-axis$   

**For example :**
![[A-2D Vector-Measured.png|300]]
Here $\vec A$ represents a vector that has covered $4$ units in $x-axis$  and $2$ units in $y-axis$, you can represent in the numerical format as 
![[(4,2) 1.png]]

#### Most of linear algebra
Most of the linear algebra will comprise of **Vector addition** and **Scalar multiplication**.

**Vector addition** :  See how Vector addition is done in Freya Holmer Math for game dev* [[Math for GameDev#2D Vector Addition|Vector Addition -2D]]

**Scalar multiplication:** Multiplying a vector with a variable like 2,0.12,-2.... would get us the vector being **scaled** to the propotion we are multiplying the vector with.

**For example : ** Multiplying a vector `(2,2)` with a variable like `2`  would produce a vector called `(4,4)`

$= 2 * (2,2)$
$= (4,4)$

and thus this `2` that we are multiplying the vector with is called as a **scalar** value, cause you know it helps you "Scale" the vector and that is why most of the variables in linear algebra is considered scalar cause vector addition and multiplication is what we will do mostly, also the reason why we are talking about this under the most of linear algebra.

#### An extended look it vector addition

So if you had seen the [[Math for GameDev#2D Vector Addition|Vector Addition - 2D]]  you would have know how [Freya](https://twitter.com/FreyaHolmer)
approaches Vector Addition. Why does she add two vectors like that, even though the explanation is logical and makes absolute sense there is a reason why she does that.

If you could see, each vector represents a certain movement, in a certain direction and a certain distance in space.

Let's consider a man standing at origin.
![[Man.png|300]]

If he's to move to a position that is an addition of both $A$ and $B$ 

![[Man_A_B.png|300]] which is  $(2,3)$ $+$ $(2,-1)$ $=$ (4,2) and will be the **target position**.

He can directly reach the $(4,2)$ 

![[Man_A_B(2).png|300]]

Or he can even move along in $A$ direction for  $A$ distance and then move in $B$ direction for $B$ distance and get to the exact same destination.
 
 ![[Man_A_B(3).png|300]]
 
 If you could compare both, they are literally the same.
 ![[Man_A_B(4).png|300]]

**Episode's conclusion :** So linear algebra is not about representing a vector in numerical or geometric representation, It is about attaining the ability to travel back and forth between both representations in order to achieve achieve a level of understanding that would help you with the challenge that you're facing.

We often as a game programmer face challenges such as finding the direction the enemy is facing to acquire his/her location over the GUI in real time, or determining the next NPC position based on the changes that the player has done to the world, These type of challenges would require us to conceptualize vectors which are in geometric form (position or direction of the NPC) into numerical form then work on the numerical form to determine the target vector/resultant vector and then apply it to the geometric form (The representing NPC) to achieve the required result.

---

## Ep:2 Linear combination, Span and Basis vectors

- Basis Vectors - Thinking coordinates as scalars
	In the last episode we saw a lot about vector coordinates and how you can work between geometric representation and numerical representation. If you look at these vectors there is this beautiful subtelty.
	There is this idea that any vector you take is actually a scalar multiple of a vector called the **basis vectors**
	The basis vectors are represented with these symbols $\hat{i}$ and $\hat{j}$ where they both are represented along the y and x axes respectively.
    	
	Let's take $\vec A$ here as an example
	![[VectorA.png|300]]
	This $\vec A$ can easily be represented in numerical representation as $(4,3)$ as the $vector$ reaches 4 units in $x-axis$ and 3 units in $y-axis$
![[VectorA Explanation.png|300]]
but according to our new idea both 4 and 3 are scalar multiples of $\hat{i}$ and $\hat{j}$ respectively.
where $\hat{j} * 3$ as $\hat{j}$ represented along $y-axis$ and $\hat{i}*4$ as $\hat{i}$ represented along $x-axis$
![[VectorAalongjxi 1.png|200]]
if we remove the scalar values 4 and 3, we will be left with what's called the actual **basis vectors** 

let's remove scalar along $\hat{j}$ first
![[Removed j cap.png|300]]
now let's remove $\hat{i}$ as well

![[Basis Vectors 2.png|300]]
Thus what now remains is called the **Basis Vectors**.

In essence when we talk about scalars and this type of scalar based understanding of coordinate system, understand that the basis vectors are what the scalars actually scale.

### What if we choose different Basis Vectors

Let's choose a different **basis vector** where one pointing somewhere along the upper right and another one pointing somewhere along the lower right.
![[DifferentBasisVectorsV2.png|500]]

now let us take two scalar values and scale each of these vectors.
where  $\vec{v}$ is scaled by $2$ and $\vec{w}$ is scaled by $3$. 
	
![[DifferentBasisVectorsScalarV2.png|500]]
	Now if you add these scaled vector together it will produce a resultant vector
 ![[DifferentBasisResultant.png|500]]
 this resultant vector marks a a point in the 2D dimensional space. 
 
 ** There is a unqiue subtelty with this concept where if you change scalar value of the this v and w vector to different value everytime and add those vectors, there is this possibility that the resultant vector can reach every possible vector in the 2 dimensional axis. **
 
 See changing the scalars with a different basis vector means, the changes are done along the lines of those vector values only like the diagram above but how does it still rach all the 2D coordinates ?
 
 It's because we do not construct the resultant vector by just adding scalar values to these different basis vectors $\vec{w}$ and $\vec{v}$ but we also add these two vectors to create a new resultant vectors, remember that this is the vector that we claim to reach all the possible 2D coordinates if we change scalar values.
 
 Also it has been said by the lecturer itself that the values of the scalar data can be used to represent in the numerical representation.
 

##### Let's see how it can be done
	This is the pair of different basis vectors we used for the previous example
![[DifferentBasisVectorsV2.png|300]]

If you try to represent both the  $\vec{w}$ and $\vec{v}$ into numerical representation you can do that is
 $\vec{v}$ $\begin{bmatrix}2\\2\end{bmatrix}$  and  $\vec{w}$ $\begin{bmatrix}3\\-1\end{bmatrix}$
 and we scalled them using two scallar values, $\vec{v}$ with 2 and  $\vec{w}$ with 3.
 this will result in this
 ![[DifferentBasisVectorsScalarV2.png|300]]
 
 and according to the lecturer we do not use the resultant vector or the original basis vectors  $\vec{v}$ and  $\vec{w}$ rather the scalar that we used to scale them both, which is 2 and 3. 
 
 and remember this is very different from using the $\hat{i}$ and $\hat{j}$ to represent the vectors.
 
 'from my own observation'
as you could see these require two scalars that scales already formed different basis vectors to represent a data, where the other one that requires $\hat{i}$ and $\hat{j}$ can be used on both $\vec{v}$ and  $\vec{w}$ seperately and  be used to find the basis vector of each of them.

- New basis vectors Vs i cap and j cap
- How numeric representation is affected by basis vectors
- What is Linear combination of two vectors ?
- The behaviour of basis vectors when subjected to linear combination
- Etimology of two basis vectors
- What if both the w and j cap are different ?
- The span 
- How the fundamental operation scalar amd vector addition operations complements to the defenition of linear algebra ?
- Vectors vs points
- Linear combo of 2 vectors in 3D Space
- Linear combo of 3 vectors 3D space

- Linear dependency
- Linear independednt
- Quiz