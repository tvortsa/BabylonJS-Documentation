---
PG_TITLE: 01. Первые шаги
---

# Первые шаги

Babylon.JS это отличный способ кодировать 3D-среду в Интернете с помощью элемента холста HTML5. 

## The Playground

Это самый быстрый и простой способ сделать свою собственную сцену. Создание 3D-сцены легко, просто добавьте камеру, источники света и 3D-фигуры (сетки), и все. 

[Playground](http://babylonjs-playground.com) это веб-сайт, на котором есть все необходимое для создания вашей собственной сцены или редактирования существующей. [больше о Playground](/features/Playground).

Шаблон для создания сцены в playground:

```javascript
var createScene = function () {

    // Создаем пространство сцены
    var scene = new BABYLON.Scene(engine);

    // Добавляем камеру и присоединяем ее к canvas
    var camera = new BABYLON.ArcRotateCamera("Camera", Math.PI / 2, Math.PI / 2, 2, BABYLON.Vector3.Zero(), scene);
    camera.attachControl(canvas, true);

    // Добавляем свет к сцене
    var light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), scene);
    var light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), scene);

    // Здесь мы создаем и манипулируем мешами
    var sphere = BABYLON.MeshBuilder.CreateSphere("sphere", {}, scene);

    return scene;

};
```

обо всем остальном позаботится Playground.

* [Playground example of above code](http://www.babylonjs-playground.com/#WG9OY#1)

## Ваш собственный HTML

When writing your own HTML you just need to embed the createScene function into an HTML page structure with a &lt; script &gt; tag along with a few other items. You will need to load the BabylonJS javascript code. Also for use on tablets and mobiles BabylonJS uses pointer events rather than mouse events and so the PEP event system needs to be loaded as well. 

In addition a canvas element will have to be added to the body as this is where the 3D scene will be rendered and a reference variable *canvas* added to it in the code. You also need to generate the BabylonJS engine before the function for creating the scene.

Finally, add code to call the scene. This enables the engine to continually render the scene in a loop and to resize it if the browser is ever resized.

### HTML template

```javascript
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">

    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
        <title>Babylon Template</title>

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

        <script src="https://cdn.babylonjs.com/babylon.js"></script>
        <script src="https://preview.babylonjs.com/loaders/babylonjs.loaders.min.js"></script>
        <script src="https://code.jquery.com/pep/0.4.3/pep.js"></script>
    </head>

   <body>
   
	<canvas id="renderCanvas" touch-action="none"></canvas> //touch-action="none" for best results from PEP
	
	<script>
        var canvas = document.getElementById("renderCanvas"); // Get the canvas element 
        var engine = new BABYLON.Engine(canvas, true); // Generate the BABYLON 3D engine

        /******* Добавляем функцию создания сцены ******/
        var createScene = function () {

            // Создаем пространство сцены
            var scene = new BABYLON.Scene(engine);

            // Add a camera to the scene and attach it to the canvas
            var camera = new BABYLON.ArcRotateCamera("Camera", Math.PI / 2, Math.PI / 2, 2, new BABYLON.Vector3(0,0,5), scene);
            camera.attachControl(canvas, true);

            // Add lights to the scene
            var light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), scene);
            var light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), scene);

            // Add and manipulate meshes in the scene
            var sphere = BABYLON.MeshBuilder.CreateSphere("sphere", {diameter:2}, scene);

            return scene;
        };
        /******* Конец функции создания сцены ******/	

        var scene = createScene(); //Вызываем функцию createScene

        // Регистрируем цикл рендеринга для повторяющегося рендеринга сцены
        engine.runRenderLoop(function () { 
                scene.render();
        });

        // Следим за событиями изменения размера окна браузера/канваса
        window.addEventListener("resize", function () { 
                engine.resize();
        });
	</script>
   
   </body>

</html>
```

## Заметки

1. Приведенные выше примеры используют более новые методы MeshBuilder для создания форм где переменные для формы задаются в the options object parameter и имеют ряд преимуществ над старым BABYLON.Mesh.Create.... который использует список параметров для переменных формы. Большая часть Playgrounds использует более старый метод, поскольку многие из них были созданы до появления MeshBuilder. 

2. The use of PEP for pointer events is more recent advice, older advice was to use a system called hand.js. Both work, although hand.js is no longer maintained. You may still find references to hand.js in the documentation. 

# Следующий шаг

Now you are ready to go further and learn how to create more shapes like spheres, cylinders, boxes, etc. by visiting [Set Shapes](/babylon101/Discover_Basic_Elements)

# Дополнительная литература
[BabylonJS Forum](http://www.html5gamedevs.com/forum/16-babylonjs)  
[PEP and hand.js](http://www.html5gamedevs.com/topic/22474-how-does-babylonjs-get-pointer-events-working/#comment-127993)  

# Useful Links External

[BabylonJS Main Website](http://www.babylonjs.com/)  
[BabylonJS Playground](http://babylonjs-playground.com)  
[PEP Github](https://github.com/jquery/PEP)  
[hand.js Github](https://github.com/Deltakosh/handjs)  




