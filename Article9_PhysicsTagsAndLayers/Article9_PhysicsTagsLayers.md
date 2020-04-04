# Unity Physics Engine Part 2

![](MainTitle.jpg)


In this tutorial, we will cover tags and layers. How to create them and what they are used for.

## Overview
The Unity version used in this tutorial is **2017.3.1f1**. Most of what we are going to cover applies to the previous and the new versions as well. So it's safe to follow. We will continue from the previous tutorial [Unity Physics Engine](https://boostlog.io/@mohammedalsayedomar/unity-physics-engine-5aeec61e47018500491f4421) and talk about the tags and layers.

## Scene Setup
Before we start, let's set up our scene. I used an awesome free model called [Space Robot Kyle](https://assetstore.unity.com/packages/3d/characters/robots/space-robot-kyle-4696).

![](https://imgur.com/vA6CMm1.png)
*Download and Import the Space Robot Kyle Package*

Let's get started:
* Create Cube and call it **Ground**. Set it's **scale** to **(10, 0.1, 10)** with zeros in transform and scale
* Create a material for it and add it to a **Materials** folder
* Create another cube named **Bullet** with **scale (0.1, 0.1, 0.5)**
* Add a Rigidbody to the **Bullet** and uncheck **Use Gravity**
* Drag and drop the **Bullet** in a **Prefabs** folder.
* Drag and drop **Robot Kyle** from **Robot Kyle > Model** to the **Hierarchy**
* **Reset transform** and set **Y position** to **0.05**
* Change the **rotation** to **(0,180,0)**
* Add **Box Collider** and Adjust it's parameters

    ![](https://imgur.com/TyT926B.gif)
    *Adjusting Collider*

* Change the **Main Camera  position** to **(0, 1, -3)**
* Change the **Main Camera rotation** to **(0, 0, 0)**
* **Save the scene** in the **_Scenes** folder

![](https://imgur.com/3i7DdyP.png)

*Scene Setup*

## Tags
#### Why Tags?
Let's say, you want to start shooting stuff with bullets. You also want to increase the score every time an enemy is shot. From our [previous tutorial](https://boostlog.io/@mohammedalsayedomar/unity-physics-engine-5aeec61e47018500491f4421), we would simply call an **OnCollisionEnter** provided by the MonoBehavior to detect collision. But this detects ANY collision where we want to gain score only when a bullet collides. For this reason, we would **create** a new Tag and **assign** it to the enemy. Now, whenever the bullet collides with Kyle, we will first check if the **Tag** of the collided object is enemy, then we increase the score, else we ignore it or do whatever we want.

#### Create and assign tag

Creating and assigning a tag are 2 different steps. Some people think that added tags are automatically assigned but you need to do it manually.

Select the **Robot Kyle** from the **Hierarchy**. In the **Inspector** window, Select **Tag** then **Add Tag**.

![](https://imgur.com/7clAcSN.png)

*Add Tag button*

Press on the **+** sign and name the new tag **Enemy**. The tag name is **CASE SENSITIVE** as we will write the actual string of the tag name later in our code. So, make sure you spelled it right.

![](https://imgur.com/hhEbYYV.png)

*Name the new tag*

If you went back to check the **Robot Kyle** prefab now, you will see that it is still **Untagged**. The previous step was just creating the tag. Open the drop down and select the new tag called **Enemy** that we just created.

![](https://imgur.com/8ZOGiyV.png)

*Assign a tag*


#### Code example
Let's start shooting bullets. 
* Create two script called **BulletShooting.cs** and **Bullet.cs** add place them inside the **Scripts** folder
* Add the **BulletShooting.cs** script to the **MainCamera**
* Add the **Bullet.cs** script to the **Bullet** prefab in the **Prefabs** folder

    ![](https://imgur.com/9G84KPm.gif)
    *Adding Scripts*

* In the **Bullet** script, copy and paste this
``` C#
    //The speed parameter to controll the bullet speed.Can be changed from the bullet Prefab.
    public float bulletSpeed = 10f;

    //Update is called once per frame
    void Update()
    {
        transform.Translate(transform.forward * bulletSpeed * Time.deltaTime);
    }

    //Detect Collision - Unity's messages
    public void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.tag == "Enemy")
            collision.gameObject.SetActive(false);

        Destroy(gameObject);
    }
```

we specified a public variable to be able to control it in the inspector

![](https://imgur.com/7p4BBsu.png)
*Public **Bullet Speed** variable is editable in the inscpector*

* In the **BulletShooting** script, copy and paste this
``` C#
    //The prefab of the bullet that we will shoot
    public GameObject bulletPrefab;

    // Update is called once per frame
    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            var bullet = Instantiate(bulletPrefab);
            bullet.transform.position = transform.position;
            bullet.transform.rotation = transform.rotation;
            Destroy(bullet, 10f);
        }
    }
```

We simply **instantiate** (Spawn) a bullet each time we press the left mouse button.

We only need to specify which prefab are we going to instantiate by dragging and dropping the **Bullet** from the prefabs folder to the inspector.

![](https://imgur.com/YJAKGf1.gif)
*Assigning the bullet prefab*

If we pressed **Play** now and clicked the left mouse button anywhere in the **Game** tab. A bullet will be shot and will deactivate the Robot **ONLY IF the Enemy tag is assigned**

![](https://imgur.com/4u6HyPl.gif)
*Affecting only the tagged object*

This happened because in the **Bullet.cs** script inside the **OnCollisionEnter** message, we checked the tag to do a certain functionality which is disable the enemy.

## Layers
#### Why layers?
Layers on the other hand are created to group physics object that shares something similar. Let's say that our bullets special enough that it can pass through walls. To do that, we will add our bullet to a different layer so that the physics engine doesn't even try calculating anything for it.

#### Create and assign layers
Creating layers doesn't differ from creating tags. In fact, both are done in the same menu. Be careful again that creating layers and assigning layers are two different steps.

Select any **GameObject** and in the **Inspector** window, Select **Layer** then **Add Layer**.

![](https://imgur.com/Yo0KVo3.png)
*Add Layer button*

The first 8 (0 to 7) layers are reserved for Unity we can't edit them. We will add two new layers called **SpecialBullet** and **Special Wall**.

![](https://imgur.com/TRUwNpF.png)

*Create 2 new layers*

We need now to tell the physics system which layers should collide with what. Goto **Edit**>**Project Settings**>**Physics**

![](https://imgur.com/91PZvFg.png)

*Physics Settings*

At the bottom you see something called **Layer Collision Matrix**. This matrix specifies which layer should collide with what. Don't feel lost, between 2 different layers, there is a checkbox. So, just look carefully. Right now we **disabled** the collision between **SpecialBullet** layer and **SpecialWall**.

![](https://imgur.com/4XoeNiX.png)

*Collision Matrix*

Assign the **SpecialBullet** layer to the **Bullet** prefab

![](https://imgur.com/Vj9Zw8T.png)

*Assign Layer*

Create a new cube as a wall for testing
* Set **position** to (0, 0.8, -0.7)
* Set **rotation** to (0, 0, 0)
* Set **scale** to (0, 0, 0.01)

![](https://imgur.com/8YmnsHE.png)

*Adding special wall*

We will assign the **SpecialWall** layer to test during runtime. But, be careful because all changes that are made while the game is running are reset back after turning off the **Play mode**.

Press **Play button** and try shooting and you will find that the Robot can't be hit. Select the **Cube** you just created and assign the **Special Wall** layer to it and you will find that the Kyle got hit.

![](https://imgur.com/MuZr4rn.gif)
*Changing layers and shooting*

## Summary
We have covered how to create tags and layers and how to use them. What we have covered is not everything. There are more use cases for them. Layers can be used with raycasting to create complex functionalities like teleporting inside triggers using laser pointer. Check the reference section for more info about tags and layers. 

## Reference
* Previous tutorial [Unity Physics Engine](https://boostlog.io/@mohammedalsayedomar/unity-physics-engine-5aeec61e47018500491f4421)
* [Unity Manual Tags] (https://docs.unity3d.com/Manual/Tags.html)
* [Unity Manual Layers] (https://docs.unity3d.com/Manual/Layers.html)![Uploading...MainTitle.JPG]()

## Social Media
* Connect with me on [LinkedIn](https://www.linkedin.com/in/mohammedalsayedomar/) to stay updated with the upcoming tutorials
* Follow me on [Twitter](https://twitter.com/Mohammed_Omar_U)