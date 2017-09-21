---
ID_PAGE: 22091
PG_TITLE: 09. Cameras, Mesh Collisions and Gravity
---
Вы когда-нибудь играли в FPS (шутер от первого лица)? В этом уроке, мы собираемся имитировать те же движения камеры: камера находится на полу, в столкновении с землей и потенциально может столкнуться с любыми объектами сцены.

![Elements](https://camo.githubusercontent.com/7422be3bf5ae147243aa3d29d9660a0210530201/687474703a2f2f7777772e626162796c6f6e6a732e636f6d2f7475746f7269616c732f30392532302d253230436f6c6c6973696f6e73253230477261766974792f30392e706e67)

_Final result_

## Как это сделать ?

Чтобы воспроизвести это движение, мы должны сделать 3 простых шага:

**1 - Объявить и применить гравитацию**

Первое, что нужно сделать, это определить наш вектор силы тяжести, определим G-force. В классических мирах, таких как Земля, направление силы тяжести - вниз (отрицательно) по оси Y , но вы можете это менять!
```javascript
scene.gravity = new BABYLON.Vector3(0, -9.81, 0);
```
 
Гравитация может применяться к любой камере, которую вы определили ранее в своем коде.
```javascript 
camera.applyGravity = true; 
```

**2 - Задаем элипсоидd**

Следующий важный шаг, определить эллипсоид вокруг нашей камеры. Этот эллипсоид представляет размеры нашего игрока: событие столкновения будет вызвано если меш столкнется с этим эллипсоидом, предотвращая слишком сильное сближение нашей камеры с этим мешем:

![Ellipsoid](https://camo.githubusercontent.com/19931f529e19679a0e2556e23fc94536e6a9b88c/687474703a2f2f7777772e626162796c6f6e6a732e636f6d2f7475746f7269616c732f30392532302d253230436f6c6c6973696f6e73253230477261766974792f30392d312e6a7067)

Свойство _ellipsoid_ самеры в babylon.js по-умолчанию (0.5, 1, 0.5), но изменение значений сделает вас выше, больше, меньше или тоньше, это зависит от настраиваемой оси. В приведенном ниже примере мы сделаем эллипсоид нашей камеры немного больше, чем стандартный:

```javascript
//Set the ellipsoid around the camera (e.g. your player's size)
camera.ellipsoid = new BABYLON.Vector3(1, 1, 1);
```

**3 - Применение коллизий**

Once you have those previous settings completed, our final step is to declare that we are interested in sensing collisions in our scene:

```javascript
// Enable Collisions
scene.collisionsEnabled = true;
camera.checkCollisions = true;
```

And declare which meshes could be in collision with our camera:

```javascript
ground.checkCollisions = true;
box.checkCollisions = true;
```

That’s it! Easy!

You can play with the scene used in this tutorial... by visiting the Babylon.js [**playground demo**]( https://www.babylonjs-playground.com/#4HUQQ).

Now, your camera is going to fall on the y-axis until it collides with the ground. And, your camera will collide with the box when you move it too near to it.

**4 - Столкновение объектов с объектами**

Вы также можете сделать то же самое с сеткой, играя с свойством _mesh.ellipsoid_ и _mesh.moveWithCollisions (velocity) _. Эта функция будет пытаться перемещать сетку в соответствии с заданной скоростью и будет проверять, нет ли конфликта между текущей сеткой и всеми сетками с активированными checkCollisions.

Вы также можете использовать _mesh.ellipsoidOffset_ для перемещения эллипсоида на сетку (По умолчанию эллипсоид центрирован на сетке)

```javascript
var speedCharacter = 8;
var gravity = 0.15;
var character = Your mesh;

character.ellipsoid = new BABYLON.Vector3(0.5, 1.0, 0.5);
character.ellipsoidOffset = new BABYLON.Vector3(0, 1.0, 0);

var forwards = new BABYLON.Vector3(parseFloat(Math.sin(character.rotation.y)) / speedCharacter, gravity, parseFloat(Math.cos(character.rotation.y)) / speedCharacter);
forwards.negate();
character.moveWithCollisions(forwards);
// or
var backwards = new BABYLON.Vector3(parseFloat(Math.sin(character.rotation.y)) / speedCharacter, -gravity, parseFloat(Math.cos(character.rotation.y)) / speedCharacter);
character.moveWithCollisions(backwards);
```

Demo by Dad72: [**Move character with gravity and collision**](http://www.babylon.actifgames.com/moveCharacter/)

## Web worker based collision system (Since 2.1)

BabylonJS 2.1 позволяет пользователю перемещать вычисления столкновений внешнему web worker что ускорит рендер.
The worker is integrated in the single framework file, and no changes are required by the developer.
The scene has now a new flag (false per default):
```javascript
scene.workerCollisions = true|false
```
Setting this flag to true will start the worker in the background. The worker will then receive all collision requests from the cameras and meshes. Setting it to false will set the collision to the regular collision calculation as it always was.

To read more about how workers were integrated head to Raanan Weber's blog:

* https://blog.raananweber.com/2015/05/26/collisions-using-workers-for-babylonjs/
* https://blog.raananweber.com/2015/06/06/collisions-using-workers-for-babylonjs-part-2/

## ArcRotateCamera
The ArcRotateCamera can also check collisions but instead of sliding along obstacles, this camera won't move when a collision appends.

To activate collisions, just call ```camera.checkCollisions = true```. You can define the collision radius with this code:

```javascript
camera.collisionRadius = new BABYLON.Vector3(0.5, 0.5, 0.5)
```

## Next step
Great, now you can develop a real FPS game! But maybe you would like to know when a mesh is in collision with another mesh? Good, because that is exactly the purpose of our [next tutorial](http://doc.babylonjs.com/tutorials/Intersect_Collisions_-_mesh).
