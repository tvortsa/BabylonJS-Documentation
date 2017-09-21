---
ID_PAGE: 22111
PG_TITLE: 11. Picking Collisions
---
## Введение

Последний тип столкновения может быть очень полезен для вас: он выбирает объект с помощью мыши. Основная трудность состоит в том, чтобы щелкнуть на 3D-объекте, тогда как на вашем экране будет плоский 2D-дисплей.

Давайте посмотрим, как мы можем перенести вашу позицию мыши в вашу 3D-сцену с помощью примера выстрела из пистолета:


![Picking](/img/tutorials/Collisions%20PickResult/11.png)

_Final result_

## Как это сделать ?

Babylon engine позволяет вам делать это очень легко, предоставляя вам полезные функции.

Прежде всего, после создания плоскости, представляющей стену, и плоскости с изображением нашего попадания, мы должны обнаружить щелчок в UI (User Interface). Как только событие произойдет, используем функцию “pick” получить некоторую важную информацию о взаимодействии между вашим кликом и вашей сценой.
```javascript
//When click event is raised
window.addEventListener("click", function () {
   // We try to pick an object
   var pickResult = scene.pick(scene.pointerX, scene.pointerY);
}),
```
 
Объект pickResult объект в основном состоит из 4 частей информации:

1. _hit_ (bool): « True » если ваш клик попадает на объект в сцене.
1. _distance_ (float): «расстояние» между активной камерой и вашим кликом (infinite если ни один меш не затронут)
1. _pickedMesh_ (BABYLON.Mesh): если вы нажмете объект, это выбранный меш. Если нет, тогда null.
1. _pickedPoint_ (BABYLON.Vector3): точка в которую вы кликнули, представлена в 3D координатах, зависит от объекта по которому вы кликнули. Null если попадания не было.

Теперь у нас есть все данные чтобы построить сцену. Нам просто нужно позиционировать изображение попадания пули (плоскость созданная ранее... called impact) когда пользователь кликает на плоскости стены:
```javascript
// если клик попадает на объект стены, мы меняем положение картинки попадания
if (pickResult.hit) {
            impact.position.x = pickResult.pickedPoint.x;
            impact.position.y = pickResult.pickedPoint.y;
}
```
Быстро и просто, не так ли?

Поиграйте с этой сценой... [at our online playground]( https://www.babylonjs-playground.com/?11).

## Расширенные возможности пикинга

Заметьте что объект pickResult может дать вам дополнительную информацию:

- `faceId`: индекс пикнутого фейса в массиве индексов. Его можно получить так:
```
var indices = pickResult.pickedMesh.getIndices();
var index0 = indices[pickResult.faceId * 3];
var index1 = indices[pickResult.faceId * 3 + 1];
var index2 = indices[pickResult.faceId * 3 + 2];
```

- `submeshId`: ID пикнутого сабмеша внутри пикнутого меша

- свойства `bu` и `bv` : это барицентрические координаты выбранной точки на грани. Пикнутый фейс представляет собой 3 вершины, и выбранная точка - это барицентр этих трех вершин со следующими весами:

  * `1 - bu - bv` для вершины n. 0
  * `bu` для вершины n. 1
  * `bv` для вершины n. 2

- `getTextureCoordinates()`: вычисляет координаты текстуры в точке указания (pick); они будут возвращены как `Vector2` в текстурном пространстве, что значит, эти координаты будут между 0 и 1.

Возможные использования включают:

- Рисование по текстуре используя DynamicTexture,
- Модифицирование фейса в который было попадание (delete, move vertices, change color...),
- Изменение материала субмеша,
- другое.


## Следующий шаг
Этот метод столкновения удобен во многих ситуациях. Разобравшись с событиями пика мышью, you can begin using that functionality to advance your application’s development.

Now you should know everything about collisions, so it’s time to move on to a classic effect in 3D : [particles](http://doc.babylonjs.com/tutorials/Particles).
