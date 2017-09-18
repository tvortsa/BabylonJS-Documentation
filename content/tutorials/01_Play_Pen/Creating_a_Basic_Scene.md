---
ID_PAGE: 21911
PG_TITLE: 01. Creating Basic Scene
---
### В этом уроке, мы собираемся создать базовую 3D сцену в Babylon.js.
![Babylon JS 01](http://urbanproductions.com/wingy/babylon/misc/tut01pic01.jpg)

_Two Basic Shapes in a Basic Scene_


Сперва, убедитесь что у вас WebGL совместимый браузер (e.g.  Internet Explorer 11+, Firefox 4+, Google Chrome 9+, Opera 15+, etc.).


### Часть HTML
Первое, создадим базовую HTML5 web страницу:

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">

   <head>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
      <title>Babylon - Базовая сцена</title>
   </head>

   <body>
   </body>

</html>
```
### Часть CSS стилей

Внутри ```<head>``` , добавьте этот CSS чтобы видеть canvas в максимальном размере:
```css
<style>
  html, body {
    overflow: hidden;
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
  }

  #renderCanvas {
    width: 100%;
    height: 100%;
    touch-action: none;
  }
</style>
```

### Внешние Javascript включения (фрэймворк)

Теперь мы звгрузим файлы нашего фрейм-ворка.  После CSS, (но все еще внутри ```<head>``` ), добавьте:

```html
<script src="babylon.js"></script>
<script src="hand.js"></script>
<script src="cannon.js"></script>  <!-- опционально, движок физики -->
<!-- <script src="Oimo.js"></script>  новый физ. движок -->
```
(если у вас еще нет этих файлов, вы можете найти их здесь: https://github.com/BabylonJS/Babylon.js, и здесь: http://handjs.codeplex.com/)


Затем, перейдем внутрь ```<body>``` нашей страницы... и добавим HTML5 canvas element, который и будет отрисовывать нашу сцену.

```html
<canvas id="renderCanvas"></canvas>
```

Теперь, сделаем переход от HTML5 в Javascript.  Оставаясь в ```<body>``` ,  добавьте:
```javascript
<script>

  // Получаем canvas element из нашего HTML выше
  var canvas = document.getElementById("renderCanvas");

  // Загружаем движок BABYLON 3D
  var engine = new BABYLON.Engine(canvas, true);
```

После чего, нужно добавить код содания сцены.  Чтобы сохранить ваш код совместимым с Babylon.js Playground, мы рекомендуем чтобы вставка функции 'createScene' была именно здесь.  Помимо генерации объекта сцены Babylon Scene, createScene() это место где вы будете добавлять ваши базовые requirements для сцены:  Одна камера, один источник света, и один или более shapes/meshes.

А теперь, добавим всю вашу функцию createScene на вашу web страницу:
 
```javascript
  // Она начинается с создания функции которая будет 'call' сразу после сборки
  var createScene = function () {

    // создается объект базовой сцены - Babylon Scene 
    var scene = new BABYLON.Scene(engine);

    // меняем цвет фона на green.
    scene.clearColor = new BABYLON.Color3(0, 1, 0);

    // создаем и позиционируем камеру free camera
    var camera = new BABYLON.FreeCamera("camera1", new BABYLON.Vector3(0, 5, -10), scene);

    // задает нацеливание камеры на центр сцены
    camera.setTarget(BABYLON.Vector3.Zero());

    // присоединяем камеру к canvas
    camera.attachControl(canvas, false);
        
    // создаем источник света, aiming 0,1,0 - to the sky.
    var light = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(0, 1, 0), scene);

    // уменьшим интенсивность света
    light.intensity = .5;

    // попробуем встроенную фигуру сферы - 'sphere'. Параметры: имя, тесселяция, размер, сцена
    var sphere = BABYLON.Mesh.CreateSphere("sphere1", 16, 2, scene);

    // переместим сферу на половину ее высоты
    sphere.position.y = 1;

    // попробуем встроенную фигуру 'ground' .  Параметры: имя, ширина, глубина, тесселяция, сцена
    var ground = BABYLON.Mesh.CreateGround("ground1", 6, 6, 2, scene);

    // покидаем эту функцию
    return scene;

  };  // конец функции createScene
```

Вы узнаете больше о параметрах, свойствах lights, cameras, и встренных геометрических объектах... из уроков.  Главное знать что наша функция createScene выполняет все требования.  Она содержит:  

*  объект Babylon Scene
*  камеру которая должна быть присоединена
*  источник света который был направлен
*  сферу которая размещена в координатах 0,1,0 (мы переместили ее по +y)
*  и плоскость земли которая размещена в координатах 0,0,0 (координаты по-умолчанию)

Есть еще три вещи, которые нужно добавить на web страницу.  Первое, 'call' на функцию createScene которую мы только что сделали. 
Добавьте это:

```javascript
  // вызываем функцию createScene которую мы создали
  var scene = createScene();
```  

Затем, всеохватывающий цикл рендеринга.  добавляем:

```javascript
  // регистрируем render - цикл для повторяющегося рендеринга сцены
  engine.runRenderLoop(function () {
    scene.render();
  });
```  

И последнее, опциональный но полезный обработчик события изменения размера canvas/window.
Добавим:

```javascript
  // следит за событием изменения размера browser/canvas 
  window.addEventListener("resize", function () {
    engine.resize();
  });
```

Итак.  Все вставки Javascript inserting закончены.  Убедитесь что закрыли элементы script, body, и html. Последние три строчки вашей HTML5 страницы... должны быть:

```html
</script>
</body>
</html>
```

Сохраните файл (в той-же папке что и babylon.js, hand.js, и cannon.js) и откройте его вашим WebGL-ready браузером.  Вы должны увидеть new scene displayed in 3D on its canvas.

A near-exact duplicate of the createScene function used in this tutorial... can be seen [**RIGHT HERE**](http://www.babylonjs.com/playground/#1GM4YQ) at the Babylon.js Playground.  You will also see the scene render LIVE, ONLINE!  Use the playground's 'Get .zip' choice if you want to download the entire index.html file used in this tutorial.

## Возникли проблемы? ##
Вот как должна выглядеть вся веб-страница:

```html
<!doctype html>
<html>
<head>
   <meta charset="utf-8">
   <title>Babylon - Basic scene</title>
   <style>
      html, body {
         overflow: hidden;
         width: 100%;
         height: 100%;
         margin: 0;
         padding: 0;
      }
      #renderCanvas {
         width: 100%;
         height: 100%;
         touch-action: none;
      }
   </style>
   <script src="babylon.js"></script>
   <script src="hand.js"></script>
   <script src="cannon.js"></script> <!-- optional physics engine -->
</head>
<body>
   <canvas id="renderCanvas"></canvas>
   <script type="text/javascript">
      // Get the canvas element from our HTML below
      var canvas = document.querySelector("#renderCanvas");
      // Load the BABYLON 3D engine
      var engine = new BABYLON.Engine(canvas, true);
      // -------------------------------------------------------------
      // Here begins a function that we will 'call' just after it's built
      var createScene = function () {
         // Now create a basic Babylon Scene object
         var scene = new BABYLON.Scene(engine);
         // Change the scene background color to green.
         scene.clearColor = new BABYLON.Color3(0, 1, 0);
         // This creates and positions a free camera
         var camera = new BABYLON.FreeCamera("camera1", new BABYLON.Vector3(0, 5, -10), scene);
         // This targets the camera to scene origin
         camera.setTarget(BABYLON.Vector3.Zero());
         // This attaches the camera to the canvas
         camera.attachControl(canvas, false);
         // This creates a light, aiming 0,1,0 - to the sky.
         var light = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(0, 1, 0), scene);
         // Dim the light a small amount
         light.intensity = .5;
         // Let's try our built-in 'sphere' shape. Params: name, subdivisions, size, scene
         var sphere = BABYLON.Mesh.CreateSphere("sphere1", 16, 2, scene);
         // Move the sphere upward 1/2 its height
         sphere.position.y = 1;
         // Let's try our built-in 'ground' shape. Params: name, width, depth, subdivisions, scene
         var ground = BABYLON.Mesh.CreateGround("ground1", 6, 6, 2, scene);
         // Leave this function
         return scene;
      }; // End of createScene function
      // -------------------------------------------------------------
      // Now, call the createScene function that you just finished creating
      var scene = createScene();
      // Register a render loop to repeatedly render the scene
      engine.runRenderLoop(function () {
         scene.render();
      });
      // Watch for browser/canvas resize events
      window.addEventListener("resize", function () {
         engine.resize();
      });
   </script>
</body>
</html>

```

## Moving On ##

From this point forward in the Basic Series tutorials, I will mostly talk about things that are contained in the createScene function (the part between the dashed lines). I will assume that you already know how to insert a createScene function into a Babylon.js HTML5 scene document (like the one above).

Try to memorize this web page layout, and see how the createScene function is at the heart of it. After you have spent some time using the Babylon.js Playground, you will see how createScene() is portable, and can be easily copied and pasted TO and FROM the playground editor window. This will allow others to help you with problems, and will also allow you to help others with their problems.

## Next step ##
----

Now you are ready to go further and learn how to create more elements like spheres, cylinders, boxes, etc.

Next in the Playpen Series - [**Basic elements**](http://doc.babylonjs.com/tutorials/Discover_Basic_Elements)
