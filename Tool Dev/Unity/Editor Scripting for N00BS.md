## What is editor scripting and why is it needed ? 
We need editor scripting so we can create tools inside unity, which we could use to automate certain processes for both developers and designers.

### What are the topics covered
1) Gizmos
2) Custom Inspectors
3) Editor Window and Scene tools

### Reference 

[Unite Europe 2016 - Editor Scripting for n00bs ~By Oliver Eberlei](https://www.youtube.com/watch?v=9bHzTDIJX_Q&t=2037s)

---


### Gizmos
**On DrawGizmos **
Helps you draw gizmos on the scene, these gizmos can be both enabled and disabled in the scene view and game view using the gizmos button.

**OnDrawGizmosSelected**
Helps you to select a gizmo from the scene

---

### Custom Inspectors
Helps you create functionalities that would help you to control the scene objects using modules presented over the inspector during the **editor time**.

First and foremost these custom inspector scripts can only exist under a folder named **Editor** in the assets folder. 
![[Screenshot 2020-11-21 at 7.26.23 PM.png]]

to access this functionality you need to add `using UnityEditor` namespace and only then you can extend from `Editor` class instead of *Monobehaviour*. Remember the reason we have put all of under an *Editor* folder is to make sure that these editor functionalities weould work on them, other wise they would just return with a bunch of errors.

The `[CustomEditor(typeof(GameCamera))]` would inform unity that this Inspector script is assosiated with the *Game Camera* script, so whenever it sees a gameObejct with the *Game Camera* script on it. It would not just show public variables in the inspector like it'd normally do rather will wait for what the script has intructed it to do.

 ##### OnInspectorGUI

Use `public override void OnInspectorGUI()` is exactly like the `OnGUI`
 functionality where everytime the GUI is redrawn it'll see what the OnGUI method has instructed and draw the GUI accordingly, It'll do the same thing here but for the inspector.
 
 if you want some access to the GUI layout, you can use `EditorGUILayout` and it has more GUI elements that will come in handy for your inpector editing.
 
 In this case EditorGUILayout.Slider helps us to create a slider on the inspector that moves the camera when interacted with the slider.
 
 **Side-Note :** *This also works like a start function, since we never press play in the editor and all of them happens in the editor time, there is no initialization part in the editor scripting, thus after editing the script and coming back to the editor has it's own downfall as some of the data will be lost during the serialization, we can check whether these data exists even after the serialization here and help us maintain the persistence*
 
 ![[Screenshot 2020-11-21 at 8.03.40 PM.png]]
 
  ##### GUI Layout

 you can also use `GUILayout` to determine the layout of the objects you're trying to inspect. This can also help you over layouts in dedicated **Unity Window** creation, which we shall arrive at later point in the note.
 ![[Screenshot 2020-11-21 at 8.16.14 PM.png|400]]
 
 ##### System.Serialize
  you already know this but add `System.Serialize` over a class that normally would not support serialization to support serialization, serialization would in return help you view variales over the inspector. 
 
 When you create an editor script for a class, it means that an actual class lies somewhere and this class let's you work over it. So there must be a way to access that class from the editor class right, atleast at one point you will be wanting to do something like that. To do that you'd usually do 
 
 The **Undo.RecordObject** helps you undo the change you've done in the inspector, since serialize the way it usually does, you need to mark which ones to undo and whic could not. ->Later on in the video this would not work for the developer but I think we can work on it, if we are to implement this.
 Actually I did figure itout, actually he did further down in the video. He had forgotten to put the `EditorUtility.SetDirty("target-script-reference");`
 This will help the unity know that the changes made in the editor through editor scripting and lets it remember the changes, which will also help the script to support both undo and redo and this problem will only be there if you use the following `target` keyword to access the object, if you use `SerializeProperty`  *(both of which will be explained down the line)* you will not face this issue and you don't have to add this set dirty property
 
 ![[Screenshot 2020-11-21 at 8.38.12 PM.png|300]]
 
 About the `target` property, The `m_Target` will help you access all the *public variables and methods* of the actual class in essence *objects* of that particular you're trying to right write the editor script for. `target` is the keyword that acts as the reference for script that you're trying to write the inspector code for.

 #####  OR
 
 you can gain access to the *objects* by using the `Serialized property` but there is one difference, If you use this to access the objects Unity will take control of the **Undo** and **Redo** functionality.
 ![[Screenshot 2020-11-21 at 8.54.15 PM.png]]
 
 `GUI.BeginHorizontal` lets you write stuff in an horizontal layout and
  `GUI.BeginVertical` lets you do everything vertical
  
  `EditorGUI.BeginChangeCheck`
  `EditorGUI.EndChangeCheck`
  
  The begin change check helps you determine the following variables change during the course before the compiler comes to the end change check. and if it does, it does what you tell it to do, otherwise it won't. This helps us from restricting/optimizing the scripting from comparing and checking the variables all the time rather it is done only when the variables are being changed.
  
  Here it will only enter the  `EditorGUI.EndChangeCheck` when the `newName` or `newPosition` will be manipulated.
  
  ##### EditorApplication.Beep();
  This will help the unity editor to emit a beep sound when the compiler runs through this.
  
  ##### EditorUtility.DisplayDialog 
  This will display a dialog pop when the compiler runs through this
  ![[Screenshot 2020-11-21 at 9.22.39 PM 1.png]]
  like this 
  ![[Screenshot 2020-11-21 at 9.23.02 PM.png|300]]
  
  ---
  ### Editor Window and Scene Tools
  
  Usuallly an editor window can be crated by inheriting from the **Editor Window** class and for that as ususal you need to implement from a *using UnityEditor namespace* whence that is done, you need to create a constructor and write an attribute over it mentioning the pathway to open it and also you need to call the *API* that opens the editor `EditorWindow.GetWindow<PreviewPlayBackWindow>(false,"Window-name")`
  
  ![[Screenshot 2020-11-22 at 11.08.30 AM.png]]
  
  
  you can also pass the get window as an instance and set init window length.
  
  ![[Screenshot 2020-11-22 at 11.11.31 AM.png]]
  
  ##### "Update" in editor time ?
  
  There is no actual *Update* method in editor time but a delegate that runs 30 frames per second called `EditorApplication.update`.
  ![[Screenshot 2020-11-22 at 11.19.26 AM.png]]
  
  you can subscribe to this delegate and get that method run **30 FPS**
  
##### EditorPrefs
In the earlier part we have discussed how `OnInpectorGUI` helps us maintain the editor persistence if done correctly, Rather we can also have editor prefs more like the player prefs to maintain persistence. The advantage of using editor prefsis just that it only lives in editor time and would not even show up even in version control, you and the other devs you're working with will not even have conflicts. *(IDK what would happen if we collab ? maybe overrite each other's editor pref files)*

##### Writing a timer in editor scripting 
Since you can only use *Time.DeltaTime* only when the editor is played and  most of the operation with the editor scripting would run on editor time, there will be a serious need for timer in the editor side itself.
Thus we adapt to using `realTimeSinceStart`, the data persistence between the serialisation is maintained using `EditorPrefs.GetFloat` where
![[Screenshot 2020-11-22 at 12.55.57 PM.png]]
![[Screenshot 2020-11-22 at 12.56.23 PM.png]]

Also in the `EditorPrefs.GetFloat("PreviewTime,0")` where the `0` is there cause when the `PreviewTime` has not been set it will return 0 when `Get` is being called.

#####  OnGUI
you can use `OnGUI` to decide what to write over the window.

#####  `[IntializeOnLoad]`
If you put `[IntializeOnLoad]`  over the top your class, What it does is whenever Unity loads the assembly, that is whenever you open Unity or recompiles the assembly seeing a check in the script it will call the constructor of this particular script.

#####  `SceneView.OnSceneGUIDelegate`
This is an event, on subscribing it would call the subscribed class whenever the user tries to interact with the scene.
![[Screenshot 2020-11-22 at 3.02.18 PM.png]]
usually subscribed from a constructor such the one above, also the `OnSceneGUI` class must take a parameter of type `SceneView` this will help you do checks that happens in the **Scene view**.

##### `Handles`
This is like `Gizmos` but for *Editors*
you can draw *cubes, lines, labels(text/texture)* and so many things with this, over the scene view of course

#####  `Handles.BeginGUI` & ` Handle.EndGUI`
The handles are to be written inbetween these to write these into the scene view, If you're using `Handles` for the *Editor Windows* this ain't needed.

##### `EditorApplication.hierarchyWindowChanged`
This is an another event that helps us know if the hierarchy is changed when the user changes into a new scene.

##### `UnityEditor.SceneManagement.EditorSceneManager.GetActiveScene()`
Helps you get the active scene even in the editor time

##### Draw tools menu
This helps you draw a tools menu
![[Screenshot 2020-11-19 at 2.28.05 PM.png]]
and selection tool helps you create a selection tool that let's user choose an option among many. More like a tab, where you can view one tab at a time., and clicking the tab gives you the index of the tab you've selected. 
This is something I created on my own
![[Screenshot 2020-11-22 at 3.48.03 PM.png|300]]

#### `Tools.Hidden = true`
Will hide all your tools such as the X,Y,Z pivot representation on the scene view.


##### Invoking mouse input in the scene view

First ![[Screenshot 2020-11-22 at 6.24.37 PM.png]]
This passive means we only need mouse input, ignore any other sort of input llike the keyboard input.

You can check the events like this,
![[Screenshot 2020-11-22 at 6.44.00 PM.png]]
and you have to set your events in the end like this, Idk why exactly we do this, but this is how you do it.
![[Screenshot 2020-11-22 at 6.44.41 PM.png|300]]

**The whole thing**
![[Screenshot 2020-11-22 at 6.46.16 PM.png]]




##### Something I have figured on my own way and has not been shown in the video
###### How to do raycast from screen in the scene view
![[Screenshot 2020-11-22 at 7.03.47 PM.png]]

##### `AssetPreview.GetAssetPreview`
This will help you do your own asset preview over the inspector.

This is the example
![[Screenshot 2020-11-22 at 6.51.24 PM.png]]
and this is the code that creates it

![[Screenshot 2020-11-22 at 6.50.44 PM.png]]

Here we use `toggle` to select between the preview objects, which actually selects prefabs to be placed in the scene. Toggle will stay on the object that has been selected rather like a button where the functionality in envoked only when the button has been clicked.

`GUI.skin.button` gives the preview textures a button like portrait.

---

## Awesome this is it, I hope you've learned something about editor scripting here.