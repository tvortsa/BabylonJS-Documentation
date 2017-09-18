---
ID_PAGE: 22011
PG_TITLE: 02. Discover Basic Elements
---
## Введение

В этом уроке, мы узнаем как моздавать базовые элементы используя Babylon.js, такие как боксы, сферы, и плоскости.

![Elements](http://urbanproductions.com/wingy/babylon/misc/tut02pic.jpg)

[**Playground Demo Scene 2 - Seven basic shapes/mesh**]( https://www.babylonjs-playground.com/?2)

## Как это делается ?
Простейший путь узнать как использовать базовые элементы... это посетить [**Playground Demo Scene 02**]( https://www.babylonjs-playground.com/?2).  Вы можете использовать 'Get .zip' в меню.  Страница index.html которую вы получите в этом zip... содержит все необходимое для создания основных элементов.  Помните что сылка, мы поговорим подробнее об этом.

Я уверен, что вы уже прочитали  [**Babylon.js Primer**](http://doc.babylonjs.com/generals/A_Babylon.js_Primer) и  [**previous tutorial**](http://doc.babylonjs.com/tutorials/Creating_a_Basic_Scene), и, следовательно, вы знаете, как форматировать файлы сцен.  Так что, мы не будем об этом говорить, здесь.  Мы пройдем шаг за шагом [**Playground Demo Scene 02**]( https://www.babylonjs-playground.com/?2).  Откройте эту ссылку в новой вкладке или окне, а затем вернитесь сюда, и мы начнем.

Начиная с коробки, мы создаем различные базовые элементы, а затем позиционируем их в конце функции (чтобы они не были на одном уровне).  Давайте поговорим о каждом из базовых элементов shapes/meshes.  

* **Создание Box**
```javascript
var box = BABYLON.Mesh.CreateBox("box", 6.0, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```
Параметры: имя, размер бокса, сцена в которую прикрепляется меш, обновляемое? (если меш должен модифицироваться впоследствии) и опциональная боковая ориентация (см ниже).Последние два параметра могут быть опущены, если вам просто нужно поведение по умолчанию :
```javascript
var box = BABYLON.Mesh.CreateBox("box", 6.0, scene);
```

* **Создание Sphere**
```javascript
var sphere = BABYLON.Mesh.CreateSphere("sphere", 10.0, 10.0, scene, false,  BABYLON.Mesh.DEFAULTSIDE);
```
Параметры: имя, количество сегментов (highly detailed or not), размер, сцена в которую прикрепляется меш, обновляемое? (если меш должен модифицироваться впоследствии) и опциональная боковая ориентация (см ниже). Последние два параметра могут быть опущены, если вам просто нужно поведение по умолчанию :
```javascript
var sphere = BABYLON.Mesh.CreateSphere("sphere", 10.0, 10.0, scene);
```
Beware to adapt the number of segments to the size of your mesh ;)

* **Создание Plane**

```javascript
var plane = BABYLON.Mesh.CreatePlane("plane", 10.0, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```

Параметры: имя, размер, сцена в которую прикрепляется меш, updatable? (если меш должен модифицироваться впоследствии) и опциональная боковая ориентация (see below). Последние два параметра могут быть опущены, если вам просто нужно поведение по умолчанию :
```javascript
var plane = BABYLON.Mesh.CreatePlane("plane", 10.0, scene);
```
* **Создание Disc (или regular polygon)**
```javascript
var disc = BABYLON.Mesh.CreateDisc("disc", 5, 30, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```
Параметры: имя, радиус, тесселяция, сцена, updatable and the optional side orientation (see below). Последние два параметра могут быть опущены, если вам просто нужно поведение по умолчанию :
```javascript
var disc = BABYLON.Mesh.CreateDisc("disc", 5, 30, scene);
```
Параметр  _tessellation_ , позволяет получить regular polygon :  
3 дает треугольник,  
4 четырехугольник,  
5 пятиугольник,  
6 шестиугольник, 7 семиугольник, 8 восьми-угольник и т.д.

* **Создание цилиндра**

```javascript
var cylinder = BABYLON.Mesh.CreateCylinder("cylinder", 3, 3, 3, 6, 1, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```

Параметры: name, height, diamTop, diamBottom, tessellation, heightSubdivs, scene, updatable and the optional side orientation (see below). The last two parameters can be omitted if you just need the default behavior :
```javascript
var cylinder = BABYLON.Mesh.CreateCylinder("cylinder", 3, 3, 3, 6, 1, scene);
```

* **Creation of a Torus**

```javascript
var torus = BABYLON.Mesh.CreateTorus("torus", 5, 1, 10, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```
Параметры: имя, diameter, thickness, tessellation (highly detailed or not), scene, updatable and the optional side orientation (see below). The last two parameters can be omitted if you just need the default behavior :
```javascript
var torus = BABYLON.Mesh.CreateTorus("torus", 5, 1, 10, scene);
```

* **Создание Knot**

```javascript
var knot = BABYLON.Mesh.CreateTorusKnot("knot", 2, 0.5, 128, 64, 2, 3, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```
Параметры: name, radius, tube, radialSegments, tubularSegments, p, q, scene, updatable and the optional side orientation (see below). The last two parameters can be omitted if you just need the default behavior :
```javascript
var knot = BABYLON.Mesh.CreateTorusKnot("knot", 2, 0.5, 128, 64, 2, 3, scene);
```
You can learn more about torus knots... [**RIGHT HERE**](http://en.wikipedia.org/wiki/Torus_knot).

* **Создание Polygon**

```javascript
var polygon = BABYLON.Mesh.CreatePolygon("polygon", [V1, V2, ..., Vn], scene, [[V1, V2, ..., Vn], [V1, V2, ..., Vn], ....[V1, V2, ..., Vn]], false, BABYLON.Mesh.DEFAULTSIDE);
```

Параметры: имя, polygon shape как массив vectors разделенных запятыми,  сцена, опциональные отверстия как массив массивов векторов разделенных запятыми, optional updatable and the optional side orientation. Последние три параметра можно опустить если нужно только поведение по-умолчанию :

NOTE все векторы это Vector3 и должны быть в плоскости XoZ , т.е. формы BABYLON.Vector3(x, 0, z);

```javascript
var polygon = BABYLON.Mesh.CreatePolygon("cylinder", [V1, V2, ..., Vn], scene);
```
Использование [PolygonMeshBuilder](http://doc.babylonjs.com/tutorials/polygonmeshbuilder)

* **Выдавливание Polygon**

```javascript
var polygon = BABYLON.Mesh.ExtrudePolygon("polygon", [V1, V2, ..., Vn], 2, scene, [[V1, V2, ..., Vn], [V1, V2, ..., Vn], ....[V1, V2, ..., Vn]], false, BABYLON.Mesh.DEFAULTSIDE);
```

Параметры: имя, polygon shape как массив vectors разделенных запятыми, глубина, сцена, опциональные отверстия как массив массивов векторов разделенных запятыми, optional updatable and the optional side orientation. The last three parameters can be omitted if you just need the default behavior :

NOTE все векторы это Vector3 и должны быть в плоскости XoZ , т.е. формы BABYLON.Vector3(x, 0, z) и считаются в порядке по-часовой стрелке;

```javascript
var polygon = BABYLON.Mesh.CreatePolygon("polygon", [V1, V2, ..., Vn], 2, scene);
```

Использование [PolygonMeshBuilder](http://doc.babylonjs.com/tutorials/polygonmeshbuilder)

* **Создание Lines Mesh**

```javascript
var lines = BABYLON.Mesh.CreateLines("lines", [
    new BABYLON.Vector3(-10, 0, 0),
    new BABYLON.Vector3(10, 0, 0),
    new BABYLON.Vector3(0, 0, -10),
    new BABYLON.Vector3(0, 0, 10)
], scene);
```
Параметры: имя, [array of comma-separated vectors], сцена. 

Я мог бы объяснить как работает конструктор Lines Mesh, но я думаю, вы можете увидеть, как это работает, просто просмотрев демо-код выше.  Обратите внимание на [ and ].  Это enclosing tokens для массива, еще одного типа данных в Javascript.  Первый vector3 массива это стартовое положение для отрисовки линии.  После, запятая, и следующий vector3 положения... указывает, где линия рисуется - к следующему.  Потом, еще запятая, и следующий vector3 нового положения.  Можно добавлять сколько угодно векторов, но ПОСЛЕДНИЙ vector3 не должен иметь запятую после него.  Пожалуйста, сделайте так, чтобы ваш массив векторов был отформатирован аналогично.    

* **Создание DashedLines Mesh**

```javascript
var dashedlines = BABYLON.Mesh.CreateDashedLines("dashedLines", [v1, v2, ... vn], dashSize, gapSize, dashNb, scene);
```
Параметры : имя, [массив Vectors3], dashSize, gapSize, dashNumber, scene.    
Как и Lines, линия вдоль vectors3 появится в пространстве. Она попытается установить _dashNumber_ штриха на этой линии в зависимости по длине каждого сегмента между двумя последовательными vectors3.    
_dashSize_ и _gapSize_ соответственно размеры dash и gap для этого штриха.   

Вам также може понравится наша новая [LinesSystem](http://doc.babylonjs.com/tutorials/Mesh_CreateXXX_Methods_With_Options_Parameter#linesystem).


* **Создание Ribbon**

Что такое ribbon ?  

Во-первых, представьте себе последовательность последовательных точек, определяющих путь.  
Затем представьте себе еще одну последовательность последовательных точек, так что еще один путь.  
Теперь, если вы создаете треугольные грани, соединяя альтернативные точки первого и второго путей, например, когда вы кружате обувь, вы получаете ленту.  

Ваши пути не обязательно должны быть параллельными. Они даже не должны быть прямыми или в одной плоскости.  
Они, ну, что бы вы ни хотели. Лента будет просто следовать вашим дорожкам.  

Теперь, представьте себе, вместо того, чтобы иметь только два пути, у вас есть много последовательных разных путей.  
Тогда полная лента будет сплошной поверхностью, соединяющей все эти промежуточные пары поверхностей пути.

```javascript
var ribbon = BABYLON.Mesh.CreateRibbon("ribbon", [path1, path2, ..., pathn], false, false, 0, scene, false, BABYLON.Mesh.DEFAULTSIDE);
```

Параметры: имя, pathArray, closeArray, closePath, offset, scene, updatable? (if the mesh must be modified later)  and the optional side orientation (see below).


  * name : строка, имя которое вы хотите дать вашему объекту,
  * pathArray : массив, заполненный путями. Пути это тоже массивы, заполненные серией последовательных _Vector3_. Вам нужен хотя бы один путь для создания ленты, и каждый путь должен содержать не менее четырех _Vector3_,
  * closeArray : boolean, если true между последним путем и первым путем создается дополнительный набор треугольников _pathArray_,
  * closePath : boolean, если true  последняя точка каждого пути массива _pathArray_ соединяется с первой точкой этого пути,
  * offset : integer (по-умолчанию половина размера _path_) обязательно, только если _pathArray_ содержит только один path. Ribbon  будет построена, соединяющая каждую i-ю точку единственного пути с i + смещенной точкой. It is ignored if _pathArray_ has more than one path,
  * scene : текущий объект-сцена,
  * updatable : boolean, если ribbon should allow updating later,
  * sideOrientation : the wanted side-orientation (BABYLON.Mesh.FRONTSIDE / BACKSIDE / DOUBLESIDE / DEFAULT).

The last two parameters can be omitted if you just need the default behavior :
```javascript
var ribbon = BABYLON.Mesh.CreateRibbon("ribbon", [path1, path2, ..., pathn], false, false, 0, scene);
```

I you need more details about how to deal with this method, you would probably read the [**Parametric Shapes**](http://doc.babylonjs.com/tutorials/Parametric_Shapes) part.

* ** Создание Tube**

```javascript
var tube = BABYLON.Mesh.CreateTube("tube", [V1, V2, ..., Vn], radius, tesselation, radiusFunction, cap, scene, false, BABYLON.Mesh.DEFAULTSIDE);

```
Параметры : name, path, radius, tesselation, optional radiusFunction, cap, scene, updatable, sideOrientation.

  * name : string, the name of the tube mesh,
  * path : an array of successive Vector3, at least two Vector3,
  * radius : nuumber, the tube radius, used when _radiusFunction_ parameter set to _null_,
  * tesselation : the number of radial segments,
  * radiusFunction : _optional_, a javascript function returns a radius value. This can be set to _null_,
  * cap : BABYLON.Mesh.NO_CAP, BABYLON.Mesh.CAP_START, BABYLON.Mesh.CAP_END, BABYLON.Mesh.CAP_ALL,  
  * updatable : boolean, if the tube should allow updating later,
  * sideOrientation : the wanted side orientation (front, back or double side).

The last two parameters can be omitted if you just need the default behavior :
```javascript
var tube = BABYLON.Mesh.CreateTube("tube", [V1, V2, ..., Vn], radius, tesselation, radiusFunction, cap, scene);
```
The tube can also be used as a [**Parametric Shapes**](http://doc.babylonjs.com/tutorials/Parametric_Shapes) by setting a radius function.



#### Updatable (обновляемый)
Этот параметр, присутствует в конструкторе каждого объекта - фигуры... указывает, может ли сетка обновляться после ее создания.  
Если false (по-умолчанию), данные сетки передаются только один раз в GPU.  
Если true, данные сетки могут быть пересчитаны и переданы в GPU при каждом обновлении фрейма.  

#### Side Orientation
Когда сетка создана, ему предоставляется дополнительная боковая ориентация.  
Side orientation используется для обеспечения видимости и / или отражения света на каждой стороне сетки.  
Существует четыре возможных значения для этого параметра :  

  * BABYLON.Mesh.FRONTSIDE,
  * BABYLON.Mesh.BACKSIDE,
  * BABYLON.Mesh.DOUBLESIDE,
  * BABYLON.Mesh.DEFAULT который является значением по умолчанию и равен FRONTSIDE.

Этот параметр является необязательным. If not given, the DEFAULT value is set.

*(Мы предполагаем что backFaceCulling включен по-умолчанию)*  

Например, представьте, что вы создаете базовую форму, такую как коробка, шар или плоскость, и вы не даете ей материала.   
Если вы находитесь позади плоскости или внутри коробки или сферы, вы заметите, что поверхности больше не видны : Babylon.js mesh часто создаются с ориентацией по умолчанию _FRONTSIDE_. Это означает, что каждая сторона имеет только вид спереди.  
Test it :  https://www.babylonjs-playground.com/#14RNAU#4  

If you apply a test material to your mesh, set _material.backFaceCulling = false;_, and light it up, you will notice that the back (or internal) face... is now visible, but it doesn't reflect the light.  Same reason : the default side orientation is still _FRONTSIDE_.  
*(You can disable _backFaceCulling_ with this _sideOrientation_ value)*

Now, just change the _sideOrientation_ parameter in your mesh constructor... to _BABYLON.Mesh.BACKSIDE_.  (Remove your test material, too.)  You can only see the backs of planes, or only see the insides (internal faces) of the box and sphere.  
Test it :  https://www.babylonjs-playground.com/#14RNAU#5

If you give your mesh some material, you can see that the light now only reflects on the back face (plane) or only inside (box, sphere, etc).  
*(you can disable _backFaceCulling_ with this _sideOrientation_ value)*


At last, change the _sideOrientation_ parameter to _BABYLON.Mesh.DOUBLESIDE_.  
As you guessed, the mesh faces are now visible on both sides. And if you give it a material, the light then reflects from both sides, too.  
Test it :  https://www.babylonjs-playground.com/#14RNAU#6   

So why not always use _BABYLON.Mesh.DOUBLESIDE_ by default ?  

Because this value creates twice the vertices of a frontside mesh. In other terms, your mesh will be twice heavier.  
*(you shouldn't disable _backFaceCulling_ with _BABYLON.Mesh.DOUBLESIDE_ value)*



### Еще базовые элементы - Grounds
До этого момента, we have been talking about basic elements from our [**Playground Demo Scene 02**]( https://www.babylonjs-playground.com/?2), but a few important mesh shapes (basic elements) are not included in that demo scene.  They are each ways of making 'ground' in Babylon.js.  Let's take a look: 

* **Создание Ground**

```javascript
var ground = BABYLON.Mesh.CreateGround("ground", 6, 6, 2, scene);
```

Parameters are: name, width, depth, subdivs, scene

Our [**Playground Demo Scene 01**]( https://www.babylonjs-playground.com/?1) uses a CreateGround constructor... so you can see one in action by using the above link.

* **Создание Ground на основе HeightMap (карты высот)**

```javascript
var ground = BABYLON.Mesh.CreateGroundFromHeightMap("ground", "heightmap.jpg", 200, 200, 250, 0, 10, scene, false, successCallback);
```
Parameters are: name, heightmapPath, width, depth, subdivs, minheight, maxheight, scene, updatable, successCallback

HeightMap grounds are easy, but we decided to create a separate tutorial so we could say more about this important Babylon.js feature. Please see our [**HeightMap Tutorial**](http://doc.babylonjs.com/tutorials/Height_Map) to learn all about heightMap grounds.

* **Create of a Tiled Ground**

Thanks to forum user Kostar111 for this handy Tiled Ground constructor. Here is the basic code needed to create a tiled ground.

```javascript

var precision = {
    "w" : 2,
    "h" : 2
};
var subdivisions = {
    'h' : 8,
    'w' : 8
};
var tiledGround = BABYLON.Mesh.CreateTiledGround("Tiled Ground", -3, -3, 3, 3, subdivisions, precision, scene, false);
```

Parameters are: name, xmin, zmin, xmax, zmax, subdivisions = the number of tiles. (subdivisions.w : in width; subdivisions.h: in height), precision = the number of subdivisions inside a tile. (precision.w : in width; precision.h: in height), scene, updatable.

Kostar111 was also kind enough to give us a fine tutorial about how to use tiled grounds. [**Click right here**](http://makina-corpus.com/blog/metier/how-to-use-multimaterials-with-a-tiled-ground-in-babylonjs) to view it. At that link, Kostar111 thoroughly explains how the tiled ground works, and also provides some Babylon.js Playground scenes that nicely demonstrate some of its many uses.

## Завершение ##
Это все! Теперь вы видите все ваши базовые элементы, and some ways to use them. Keep watching this area of the tutorial for new basic elements, as they are being added quite quickly : you'll find the updated list with all parameter explanations [**in this section**](http://doc.babylonjs.com/tutorials/Mesh_CreateXXX_Methods_With_Options_Parameter). 
Feel free to imagine a few of your own basic element ideas, and present them on the forum. Help us make our list of basic elements grow, if you can.  

## Next step ##
----
We saw that we needed a bit of 'positioning' to keep our basic elements from sitting atop one another in the scene. Now let's learn more about positions (sometimes called translations) as well as about rotation and scaling. Ready? Sure you are! [**Click here for the next tutorial.**](http://doc.babylonjs.com/tutorials/Materials)
