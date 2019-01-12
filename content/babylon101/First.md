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

При написании своего HTML вам просто нужно вставить функцию createScene на страницу HTML в тегах &lt; script &gt; наряду с несколькими другими элементами. Вам нужно будет загрузить BabylonJS javascript код. Также для использования на планшетах и ​​мобильных телефонах BabylonJS использует события указателя, а не события мыши, поэтому необходимо также загрузить систему событий PEP. 

Кроме того, элемент canvas должен быть добавлен к body, так как это то где 3D сцена будет визуализирована и ссылка на переменную *canvas* добавляется в код. Вам также необходимо сгенерировать BabylonJS engine перед функцией для создания scene.

Наконец, добавьте код для вызова scene. Это позволит engine постоянно отображать сцену в цикле и изменять ее размер, если размер браузера был изменен.

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

            // Добавьте камеру на сцену и прикрепите ее к холсту
            var camera = new BABYLON.ArcRotateCamera("Camera", Math.PI / 2, Math.PI / 2, 2, new BABYLON.Vector3(0,0,5), scene);
            camera.attachControl(canvas, true);

            // Добавить свет на сцену
            var light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), scene);
            var light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), scene);

            // Добавить и управлять сетками на сцене
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

Теперь вы готовы пойти дальше и научиться создавать больше фигур, таких как spheres, cylinders, boxes, etc. by visiting [Set Shapes](/babylon101/Discover_Basic_Elements)

# Дополнительная литература
[BabylonJS Forum](http://www.html5gamedevs.com/forum/16-babylonjs)  
[PEP and hand.js](http://www.html5gamedevs.com/topic/22474-how-does-babylonjs-get-pointer-events-working/#comment-127993)  

# Useful Links External

[BabylonJS Main Website](http://www.babylonjs.com/)  
[BabylonJS Playground](http://babylonjs-playground.com)  
[PEP Github](https://github.com/jquery/PEP)  
[hand.js Github](https://github.com/Deltakosh/handjs)  




