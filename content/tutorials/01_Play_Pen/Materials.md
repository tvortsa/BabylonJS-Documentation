---
ID_PAGE: 22051
PG_TITLE: 04. Materials
---
## Введение

Теперь, когда вы можете создавать различные базовые элементы сетки в любой точке сцены, мы собираемся предоставить этим сеткам некоторые материалы, чтобы определить, как выглядят эти сетки.

![Elements](/img/tutorials/Materials/04.png)

[**Playground Demo Scene 4 - Materials**](http://www.babylonjs.com/playground/?4)

## Как это сделать ?
Мы настолько искусны в создании функций createScene, что можем сделать это во сне, не так ли? Итак, давайте прокатиться с всенаправленным PointLight и орбитальной ArcRotateCamera.  После чего, мы начнем создавать некоторые основные элементы сетки, чтобы проверить наши материалы на.

```javascript
function createScene() {
    var scene = new BABYLON.Scene(engine);
    var light = new BABYLON.PointLight("Omni", new BABYLON.Vector3(0, 100, 100), scene);
    var camera = new BABYLON.ArcRotateCamera("Camera", 0, 0.8, 100, BABYLON.Vector3.Zero(), scene);

    //Создаем сферы
    var sphere1 = BABYLON.Mesh.CreateSphere("Sphere1", 10.0, 6.0, scene);
    var sphere2 = BABYLON.Mesh.CreateSphere("Sphere2", 2.0, 7.0, scene);
    var sphere3 = BABYLON.Mesh.CreateSphere("Sphere3", 10.0, 8.0, scene);
[…]
    //Позиционируем меши
    sphere1.position.x = -40;
    sphere2.position.x = -30;
```

Пока что у вас есть только серая серая сетка. Как страшно! Чтобы применить к ним материал, вам нужно будет создать новый объект материала, подобный этому:
```javascript
var materialSphere1 = new BABYLON.StandardMaterial("texture1", scene);
```

И применить этот материал к объекту по вашему выбору:
```javascript
sphere1.material = materialSphere1;
```
Или, создайте и примените все за один шаг:
```javascript
sphere1.material = new BABYLON.StandardMaterial("texture1", scene);
```

“Я тестирую сцену, и …ничего не изменилось…”

Точняк, потому что это материал по умолчанию. Измените его настройки. You wВы не будете менять меш, только материал.

“Итак, как я могу настроить свой материал, чтобы дать прекрасный взгляд на мой объект?”

Это делается путем установки свойств материала:

* **Transparency** (прозрачность, альфа-канал)

Alpha композитинг и прозрачность в целом могут быть немного сложными. Можете прочесть [в википедии об этом](http://en.wikipedia.org/wiki/Alpha_compositing).  Вы столкнетесь с еще большим количеством применений для него, когда вам понравится система частиц BabylonJS, и BabylonJS sprites system. 

 Альфа-прозрачность, записывается в процентах (%), и может быть применена к материалу следующим образом:
```javascript
materialSphere1.alpha = 0.5;
```

* **Diffuse**

Diffuse это родной цвет материала когда он освещен. Можно указад сплошной цвет ```diffuseColor``` свойство:
```javascript
materialSphere1.diffuseColor = new BABYLON.Color3(1.0, 0.2, 0.7);
```

Или можно использовать текстуру:
```javascript
materialSphere1.diffuseTexture = new BABYLON.Texture("grass.png", scene);
```

![tof](/img/tutorials/Materials/04-1.png)

**Подробнее о текстурах:** Обязательно используйте правильный путь к своему изображению (relative or absolute path). Поддерживаются следующие форматы изображений JPG, PNG, JPEG, BMP, GIF… (они же поддерживаются браузером).

Если вы хотите перевести (сместить) текстуру на меше, используйте свойства “uOffset” и “vOffset”:
```javascript
materialSphere1.diffuseTexture.uOffset = 1.5;
materialSphere1.diffuseTexture.vOffset = 0.5;
```
И если вы хотите repeat/tile шаблон изображения (например текстура троавы), используйте свойства “uScale” и “vScale”:
```javascript
materialSphere1.diffuseTexture.uScale = 5.0;
materialSphere1.diffuseTexture.vScale = 5.0;
```

Помните что (u, v) coordinates refer to the following axis:

![tof](/img/tutorials/crate.jpg)

И если ваша текстура имеет alpha, вы должны указать это:
```javascript
materialSphere1.diffuseTexture.hasAlpha = true;
```

Тогда, alpha используется для альфа-тестирования. But you may want to use it for alpha blending. To do so, just set ```materialSphere1.useAlphaFromDiffuseTexture```

All of these texture settings apply to the other StandardMaterial properties as well. (.emissiveTexture, .ambientTexture, .specularTexture)  I will remind you.  Now let's continue talking about the other StandardMaterial properties.


* **Emissive**

The emissive is the color produced by the object itself. You can specify a solid color with the ```emissiveColor``` property:
```javascript
materialSphere1.emissiveColor = new BABYLON.Color3(1, .2, .7);
```

Or, you can use a texture:
```javascript
materialSphere1.emissiveTexture = new BABYLON.Texture("grass.png", scene);
```
See the **More About Textures** section above.  Change occurrences of 'diffuse' to 'emissive', of course.

* **Ambient**

The ambient can be seen as a second level of diffuse. The produced color is multiplied to the diffuse color. This is especially useful if you want to use light maps baked into textures. You can specify a solid color with the ```ambientColor``` property:
```javascript
materialSphere1.ambientColor = new BABYLON.Color3(1, 0.2, 0.7);
```
Or, you can use a texture:
```javascript
materialSphere1.ambientTexture = new BABYLON.Texture("grass.png", scene);
```
See the **More About Textures** section above.  Change occurrences of 'diffuse' to 'ambient', of course.

* **Specular**

The specular is the color produced by a light reflecting from a surface. You can specify a solid color with the ```specularColor``` property:
```javascript
materialSphere1.specularColor = new BABYLON.Color3(1.0, 0.2, 0.7);
```
Or, you can use a texture:
```javascript
materialSphere1.specularTexture = new BABYLON.Texture("grass.png", scene);
```
When using a texture you can set ```materialSphere1.useGlossinessFromSpecularMapAlpha``` to true to use specular map alpha as glossiness level.

You can also control how specular behaves with alpha. By default, specular does not interact with alpha, but you can set ```materialSphere1.useSpecularOverAlpha``` to true to have alpha inversely proportional to specular value.

Again, see the **More About Textures** section far above.  Change occurrences of 'diffuse' to 'specular', of course.

The specular property has one more setting.  The size/intensity of the specular reflection can be set using the ```specularPower``` property:
```javascript
materialSphere1.specularPower = 32;
```


*** Section on OpacityTexture needed here, coming soon. ***


There, we have visited the primary color and texture properties of StandardMaterial.  But we are not done yet.  Here are a few more handy properties.

* **Back-Face Culling**

Simply put, “back-face culling” determines whether or not a StandardMaterial is visible from its back side (from behind).  TRUE = NOT visible.  More precisely, this rendering-speed-optimization technique determines if a polygon of a graphical object is visible or not. If set to TRUE or boolean 1, the  Babylon engine won’t render hidden face(s) of the meshes that use this material. It is set TRUE by default, but can be changed to false as wanted. You may want to read more about back-face culling at [the wikipedia page about it](http://en.wikipedia.org/wiki/Back_face_culling).  

In this example, the texture has some alpha, and back-face culling is set to false for the front sphere... in order to see its black inside face:

![tof](/img/tutorials/Materials/04-2.png)

```javascript
materialSphere1.backFaceCulling = false;
```

* **WireFrame**

You can see your object in wireframe mode... by using:

```javascript
materialSphere1.wireframe = true;
```

![tof](/img/tutorials/Materials/04-3.png)

Again, you can see things from this tutorial... come to life... by browsing to [the Babylon.js Playground scene 4](http://www.babylonjs.com/playground/?4).

More information about materials can be found by reading [**Unleash the StandardMaterial**](https://www.eternalcoding.com/?p=303) and also [**Advanced Texturing**](http://doc.babylonjs.com/tutorials/Advanced_Texturing).



## Textures Available to Playground

The following images are available to use as textures or heightmaps in the playground using

```javascript
new BABYLON.Texture("textures/name", scene);
```

* albedo.png

* amiga.jpg

* bloc.jpg

* candleopacity.png

* cloud.png

* co.png

* crate.png

* distortion.png

* earth.jpg

* equirectangular.jpg

* fire.png

* flare.png

* floor.png

* floor_bump.PNG

* fur.jpg

* grass.jpg

* grass.png

* grassn.png

* ground.jpg

* heightMap.png

* heightMapTriPlanar.png

* impact.png

* invmask.png

* Logo.png

* mask.png

* misc.jpg

* mixMap.png

* normalMap.jpg

* orient.jpg

* palm.png

* player.png

* reflectivity.png

* rock.png

* rockn.png

* roundMask.png

* sand.png

* specmap.png

* specularglossymap.png

* sphereMap.png

* sun.png

* SunDiffuse.png

* tree.png

* walk.png

* waterbump.png

* worldHeightMap.jpg

* xStrip.jpg

* yStrip.jpg

* zStrip.jpg

## CubeMap Groups Available to Playground

The following groups of images are available to use as skyboxes in the playground using

```javascript
new BABYLON.CubeTexture("textures/common part of names", scene);
```
* skybox_nx.jpg

* skybox_ny.jpg

* skybox_nx.jpg

* skybox_px.jpg

* skybox_py.jpg

* skybox_pz.jpg

* skybox2_nx.jpg

* skybox2_ny.jpg

* skybox2_nx.jpg

* skybox2_px.jpg

* skybox2_py.jpg

* skybox2_pz.jpg

* skybox3_nx.jpg

* skybox3_ny.jpg

* skybox3_nx.jpg

* skybox3_px.jpg

* skybox3_py.jpg

* skybox3_pz.jpg

* skybox4_nx.jpg

* skybox4_ny.jpg

* skybox4_nx.jpg

* skybox4_px.jpg

* skybox4_py.jpg

* skybox4_pz.jpg

* TropicalSunnyDay_nx.jpg

* TropicalSunnyDay_ny.jpg

* TropicalSunnyDay_nx.jpg

* TropicalSunnyDay_px.jpg

* TropicalSunnyDay_py.jpg

* TropicalSunnyDay_pz.jpg


## HDR CubeMaps Available to Playground

The following images are available to use as textures or heightmaps in the playground using

```javascript
new BABYLON.HDRCubeTexture("textures/name", scene);
```

* country.hdr

* environment.babylon.hdr

* forest.hdr

* night.hdr

* parking.hdr

* room.hdr

## Environment textures
The following images are available to use as environment texture using

```javascript
BABYLON.CubeTexture.CreateFromPrefilteredData("/textures/environment.dds", scene);
```

* environment.dds

## Other Files Available to Playground in "textures" Directory

babylonjs.mp4

big_buck_bunny.mp4

babylonjs.webm

HorrorBlue.3dl

LateSunset.3dl


## Next step
Great, your scene is looking better than ever with those materials! Later we will see how to use advanced techniques with materials. But for now, we have to learn [**how to use cameras**](http://doc.babylonjs.com/tutorials/Cameras).
