# Why are we learning this ?
- I wanted to learn how the heat maps are done, so I could proceed learning A* algorithm for the Dungeons part in the Bonfire 2 game
- This will also enable us to understand basic mesh manipulation

# What will we be learning ?
- We will be learning how to create basic polygon AKA triangle later we will make changes to the script and enhance it into a Quad

## Introduction - What are meshes
- Meshes are set of **vertices** connected together in a pattern to form a polygon
	- Vertices are the basic building block of any 3D mesh. Every 3D object you see in movies and gamers are just closely placed vertices in a particular order to form a mesh. To know more about this, head on here [[Math for GameDev - Freya Holmer]]
		![[BuzzLightear.png]]
	-  A **polygon** is a plane figure that is described by a finite number of straight line segments connected to form a closed polygonal chain or polygonal circuit. It can either be a triangle or a quad or any complex web of a structure.https://www.mathsisfun.com/definitions/polygon.html
	-  A basic polygon has 3 vertices and is in a shape of a triangle
	![[Polygon-3vertice.png]]
- Meshes might also possess **UV** that allows the mesh to have a texture over it
	- UV has it's own coordinates that determines how the texture is wrapped over the mesh

## Let's create a basic polygon and a quad(eventually) using the unity engine
### How to render a mesh in Unity ?
Unity requires a **Mesh Renderer** and a **Mesh Filter** to actually visualize a mesh.	
![[MeshRend_MeshFilter.png]]
**Mesh Filter** has all the details about a mesh like how the mesh should come into fruition.
**Mesh Renderer** generates a mesh, in technical term it plainly renders a mesh.

Let's create a script called `BasicPolygon` and add a Mesh Filter and Mesh Renderer to the game-object that this script will be on (Or you can do it through *Require Component* like I did).  Then later create a local instance of a mesh and get the Mesh Filter component that we got attatched to the gameobject the script is currently on. Now set the mesh we have generated to the mesh filter.
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(MeshRenderer))]
[RequireComponent(typeof(MeshFilter))]
/// This class helps you create a basic polygon AKA a triangle
public class BasicPolygon : MonoBehaviour
{
    void Start()
    {
        Mesh mesh = new Mesh();
        GetComponent<MeshFilter>().mesh = mesh;
    }
}
```

If you play the game, you'll see nothing being rendered because we have not provided the mesh instance with any vertices for it to lay out. If you see the mesh filter component, It'll have the mesh variable be filled.
![[Mesh filter-mesh.png]]
 If you double click it you'll see, how many **vertices(verts)** and **triangles(tris)** it has. In our case it's zero for both.
![[Mesh Data01.png]]

### So let's add them vertices shall we
Here we have three vertices in a triangular form, as we have said earlier a basic polygon is a triangle and to form a triangle we atleast need 3 vertices distanced away from each other.
![[Polygon-3vertice(numbers).png]]
Now let's create a `vector 3` array called `vertices` and add these values to it one by one and later assign it to `vertices` component of the `mesh` variable

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(MeshRenderer))]
[RequireComponent(typeof(MeshFilter))]
/// This class helps you create a basic polygon AKA a triangle
public class BasicPolygon : MonoBehaviour
{
    void Start()
    {
        Mesh mesh = new Mesh();

        ///Determines points these individual meshes will be in the world
        Vector3[] vertices = new Vector3[3]; ///Array length is 3 cause we need 3 vertices to create a basic polygon-triangle

        vertices[0] = new Vector2(0, 0);
        vertices[1] = new Vector2(0, 100);
        vertices[2] = new Vector2(100, 100);

        mesh.vertices = vertices;
        GetComponent<MeshFilter>().mesh = mesh;
    }
}

```

Now our `mesh` variable has vertices. Now it might able to render something right ? 
# NO 
you might still see nothing over the game view, yet if you double click over the **mesh** variable over the mesh filter this time you could able to witness that number verts have been pumped upto 3.

So what's the problem then ? Why cannot you able to see the mesh or the triangle. The resason is that you have only defined the vertices and not the order in which they should render. 

Every mesh's front is rendered in clockwise order in our polygon's case, it's V1, V2 and V3 in the mentioned order. if it is the opposite then it assumes that it is the back of them mesh, problem with being a back of a mesh is that some materials does not support back meshe's and downright render them invisible.

**So how do we do this in Unity ?**
That is why triangle parameter is part of any instance, these helps defines the order in which the mesh is rendered.

So we create a new `int` array called `triangles` and this will help us store the order in which the vertices must be rendered
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(MeshRenderer))]
[RequireComponent(typeof(MeshFilter))]
/// This class helps you create a basic polygon AKA a triangle
public class BasicPolygon : MonoBehaviour
{
    void Start()
    {
        Mesh mesh = new Mesh();

        ///Determines points these individual meshes will be in the world
        Vector3[] vertices = new Vector3[3]; ///Array length is 3 cause we need 3 vertices to create a basic polygon-triangle
        int[] triangles = new int[3]; ///Array length is 3 cause we are creating a triangle and we need to render all three vertices

        vertices[0] = new Vector2(0,   0);
        vertices[1] = new Vector2(0,   100);
        vertices[2] = new Vector2(100, 100);

        triangles[0] = 0;
        triangles[1] = 1;
        triangles[2] = 2;

        mesh.vertices = vertices;
        mesh.triangles = triangles;

        GetComponent<MeshFilter>().mesh = mesh;
    }
}
```
Array length of `triangles` is 3 cause we are creating a triangle and it requires us to render 3 vertices.

And the values inside the ** triangles array determines which index of the meshes array should be chosen and in which order.

And now this time is you play the the project in the editor you'll see a beautiful triangle. I really don't know what's beautiful about it but here's a triangle.
![[Pink-Triangle.png]]
But why is it pink?

It is because that the mesh has no material.
So create a material and drag and drop a texture on  the material if you'd like, I have put this  image as a texture.
![[Anime.jpg]]

Now drag and drop the material over the gameobject (which has the script and all the required components). Now if you play it you'll again see the same triangle but in brown.
But this is not what you wanted to see. Where is the cute anime girl ?

So the thing is , do you remember me mentioning about the UV, Like I said UV decides how a material/texture should wrap over the mesh. So let us define the UV. 
First create a `vector 2` array, why vector 2 ? cause UV are normalised vectors meaning they don't have a magnitude only direction. Give the order in which you want this texturer to be applied and assign it to the uv parameter of the mesh variable.

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(MeshRenderer))]
[RequireComponent(typeof(MeshFilter))]
/// This class helps you create a basic polygon AKA a triangle
public class BasicPolygon : MonoBehaviour
{
    void Start()
    {
        Mesh mesh = new Mesh();

        ///Determines points these individual meshes will be in the world
        Vector3[] vertices = new Vector3[3]; ///Array length is 3 cause we need 3 vertices to create a basic polygon-triangle
        Vector2[] uv = new Vector2[3]; ///Array length is 3 cause we need to cover three vertices to create a texture over them
        int[] triangles = new int[3]; ///Array length is 3 cause we are creating a triangle and we need to render all three vertices

        vertices[0] = new Vector2(0,   0);
        vertices[1] = new Vector2(0,   100);
        vertices[2] = new Vector2(100, 100);


        uv[0] = new Vector2(0, 0);
        uv[1] = new Vector2(0, 1);
        uv[2] = new Vector2(1, 1);

        triangles[0] = 0;
        triangles[1] = 1;
        triangles[2] = 2;

        mesh.vertices = vertices;
        mesh.uv = uv;
        mesh.triangles = triangles;

        GetComponent<MeshFilter>().mesh = mesh;
    }
```

And you can see the texture now over the triangular mesh you have implemented.
![[AnimegirlHalf.png]]

### Time to upgrade this triangle into a quad
So in order for you to complete this triangle into a quad you need to add another vertex. 
![[Quad-4vertice(numbers).png]]
Now its a perfect quad! Voila! 
Add one more index to both `vertices`  and `UV` array cause of the new vertex but `triangles` array will be pumped to **6**

## Woah that's huge jump in numbers right ? why though?
The reason is that we have to render both triangles seperately the one at the top and the one in the bottom, both in clockwise order. So it'll be (0,0 (0,100)(100,100) then (0,0) (100,100) and (100,0) This way we get two triangles that comprised as one to be seen as a quad.

For this wee create a new script called and create new game-object and add mesh filer and render, so could we let the triangle undisturbed just in case if we need to use it again. 
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(MeshRenderer))]
[RequireComponent(typeof(MeshFilter))]
/// This class helps you create a quad AKA a square
public class Quad : MonoBehaviour
{
    void Start()
    {
        Mesh mesh = new Mesh();

        ///Determines points these individual meshes will be in the world
        Vector3[] vertices = new Vector3[4]; ///Array length is 3 cause we need 3 vertices to create a basic polygon-triangle
        Vector2[] uv = new Vector2[4]; ///Array length is 3 cause we need to cover three vertices to create a texture over them
        int[] triangles = new int[6]; ///Array length is 3 cause we are creating a triangle and we need to render all three vertices

        vertices[0] = new Vector2(0, 0);
        vertices[1] = new Vector2(0, 100);
        vertices[2] = new Vector2(100, 100);
        vertices[3] = new Vector2(100,0 );


        uv[0] = new Vector2(0, 0);
        uv[1] = new Vector2(0, 1);
        uv[2] = new Vector2(1, 1);
        uv[3] = new Vector2(1, 0);


        triangles[0] = 0;
        triangles[1] = 1;
        triangles[2] = 2;

        triangles[3] = 0;
        triangles[4] = 2;
        triangles[5] = 3;

        mesh.vertices = vertices;
        mesh.uv = uv;
        mesh.triangles = triangles;

        GetComponent<MeshFilter>().mesh = mesh;
    }
}
```

Now if you play it you'll see this!! The anime girl in full glory
![[Ainmegirlfull 1.png]]
This is how you create a quad or a triangle through script in unity

That's all folks :)