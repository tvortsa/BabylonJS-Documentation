---
ID_PAGE: 22041
PG_TITLE: 03. Position, Rotation, Scaling
---
## Введение

В этом уроке, мы узнаем как позиционировать, масштабировать и вращать любые объекты, созданные в нашем последнем уроке. Мы также установим родителя и начнем понимать, как иерархия влияет на положение, поворот и масштабирование.

![Elements](/img/tutorials/Rotation%20and%20scaling/03.png)

[**Playground Demo Scene 3 - Positioned, Scaled, and Rotated Boxes**]( https://www.babylonjs-playground.com/?3)

## Как это сделать ?
Как обычно, мы начинаем функцию createScene, включая основные элементы сцены
```javascript
function createScene() {
  var scene = new BABYLON.Scene(engine);
  var light = new BABYLON.PointLight("Omni", new BABYLON.Vector3(0, 100, 100), scene);
  var camera = new BABYLON.ArcRotateCamera("Camera", 0, 0.8, 100, new BABYLON.Vector3.Zero(), scene);
}
```

Затем создайте столько ящиков, сколько хотите.:
```javascript
//Creation of 3 boxes
var box1 = BABYLON.Mesh.CreateBox("Box1", 6.0, scene);
var box2 = BABYLON.Mesh.CreateBox("Box2", 6.0, scene);
var box3 = BABYLON.Mesh.CreateBox("Box3", 6.0, scene);
[…]
```
* **Position**

Вы можете легко разместить любые боксы в сцене, где угодно. Например:

```javascript
//Позиционирование боксов
box1.position = new BABYLON.Vector3(-20,0,0);
box2.position.x = -10; // или box2.position = new BABYLON.Vector3(-10,0,0);
box3.position.x = 0;
```

И теперь, с такой же легкостью кодирования, вы можете поворачивать ящики вокруг любой оси.&nbsp; Например:

* **Rotation** (углы в радианах)

```javascript
//Вращение бокса вокруг оси x 
box1.rotation.x = Math.PI/4; // or box1.rotation = new BABYLON.Vector3(Math.PI/4,0,0);

//Вращение бокса вокруг оси y 
box2.rotation.y = Math.PI/6;
```

* **Scaling**

И да, так же легко масштабировать ящики вдоль любых осей.&nbsp; Например:
```javascript
//Масштабирование 2x по оси x 
box3.scaling.x = 2; // or box3.scaling = new BABYLON.Vector3(2,1,1);
```

* **Parenting**

Еще одна фича Babylon - привязывать объект относительно другого, создавая связь между родителями и дочерними элементами между двумя сетками. This link implies that all parent transformations (position/rotation/scaling) will also be applied to the child’s transformations.
```javascript
//Positioning box3 relative to box1
box3.parent = box1;
box3.position.z = -10;
```

## Notes
Parent-child hierarchies are evaluated on every frame. So any position, rotation and scaling transformations made to the parent... prior to assigning it to children... will also be applied to the children when the parent is assigned.

All transformations made after assigning a parent to a child... will be maintained with the child in relation to the parent.

Basically in simple terms, don't rotate or move a child until after you've assigned it to the parent, and keep in mind that additional rotations will be in relation to the parent after the parent rotations are applied to the child.

### Some Links
This tutorial's createScene() can be viewed and experimented-with... by visiting [Babylon.js Playground scene 03](http://www.babylonjs.com/playground/?3). We also have some animated demonstrations that are part of the Babylon.js Primer, viewable in the Miscellaneous section.&nbsp; Here are links to those demos.

* [**Position demo**](http://www.babylonjs.com/playground/#35CPC)
* [**Rotation demo**](http://www.babylonjs.com/playground/#YIT1S)
* [**Scaling demo**](http://www.babylonjs.com/playground/#1VMQNH)


## Next step
Now you know how to create and move objects in a scene, but all your meshes have the same 'skin'. Not for long, if you read our next tutorial about materials.
