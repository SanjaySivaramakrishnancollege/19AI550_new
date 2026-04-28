# Ex.No: 3  Basic movements in Unity 
### DATE: 28.04.2026                                                                        
### REGISTER NUMBER : 212223240151 
### AIM: 
 To learn the basic movements translation,scaling and rotation of game objects through code.
### Procedure:
1. Setup the Scene
2. Open Unity and create a 3D Scene.
3. Add three objects:Cube → Rename to Object1 (for movement),Sphere → Rename to Object2 (for rotation).Capsule → Rename to Object3 (for scaling).
4. Add the Script,Create a C# Script → Name it TransformOperations.cs.
5. Write the code for translation,scaling and rotation,save and close the script
6. Save the script
7. Select any empty GameObject (or create one: GameObject → Create Empty).
8. Attach the TransformOperations script to it.
9. In the Inspector, assign Object1 → Drag the Cube,Object2 → Drag the Sphere.Object3 → Drag the Capsule.
10. Run the Scene Press Play ▶️ in Unity
11. Stop the program.
### Program 
```
using UnityEngine;

public class FirstScript : MonoBehaviour
{
    public Transform object1;
    public Transform object2;
    public Transform object3;

    void Start()
    {
        Debug.Log("Welcome to Unity!");
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.A) && object1 != null)
            object1.Translate(2f, 0, 0);

        if (Input.GetKeyDown(KeyCode.B) && object2 != null)
            object2.Rotate(0, 20f, 0);

        if (Input.GetKeyDown(KeyCode.C) && object3 != null)
            object3.localScale += new Vector3(0.2f, 0.2f, 0);
    }
}
```
### Output:

<img width="1919" height="1073" alt="image" src="https://github.com/user-attachments/assets/3e6853c0-7cde-4983-975f-339288195006" />

![Uploading image.png…]()






### Result:
Thus the basic movement is learned through scripting


