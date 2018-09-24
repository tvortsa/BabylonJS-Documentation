---
ID_PAGE: 22531
PG_TITLE: How to use Actions
---

# Actions

Actions это простой способ добавить взаимодействие в ваших сценах. Action запускается при запуске триггера.

Например, вы можете указать, что, когда пользователь нажимает (или касается)  mesh, то action выполняется.

## Как это использовать

Для использования actions, вы должны прикрепить `BABYLON.ActionManager` к мешу в вашей сцене:

```javascript
mesh.actionManager = new BABYLON.ActionManager(scene);
```

Как только ActionManager создан, вы можете начать регистрацию actions:

```javascript
mesh.actionManager.registerAction(new BABYLON.InterpolateValueAction(BABYLON.ActionManager.OnPickTrigger, light, "diffuse", BABYLON.Color3.Black(), 1000));
```

Например, это действие будет анимировать свойство `light.diffuse` до черного в течение 1000ms когда пользователь кликнет по мешу.

Вы можете также объединять actions в цепочки:

```javascript
mesh.actionManager.registerAction(new BABYLON.InterpolateValueAction(BABYLON.ActionManager.OnPickTrigger, light, "diffuse", BABYLON.Color3.Black(), 1000)).then(new BABYLON.SetValueAction(BABYLON.ActionManager.NothingTrigger, mesh.material, "wireframe", false));
```

В этом случае, первый клик будет анимировать свойство `light.diffuse` , второй клик будет устанавливать `mesh.material` в false. Третий будет запускать сноваи анимировать свойство `light.diffuse` и т.д.

Наконец, вы можете добавлять условия вашему действию. В этом случае, actions запустится если при срабатывании триггера - условие истинно:

```javascript
var condition1 = new BABYLON.PredicateCondition(sphere.actionManager, function () {
    return light1.diffuse.equals(BABYLON.Color3.Red());
});
sphere.actionManager.registerAction(new BABYLON.InterpolateValueAction(BABYLON.ActionManager.OnPickTrigger, camera, "alpha", 0, 500, condition1));
```

В этом примере, свойство `camera.alpha` будет анимировано до 0 за 500ms при клике пользователя по сфере только если свойство `light1.diffuse` эквивалентно red.

## Triggers

На сегодняшний момент, поддерживается до 12 отдельных триггеров:

Следующий список определяет триггеры, связанные с meshes:

* `BABYLON.ActionManager.NothingTrigger`: Никогда не происходит. Используют для sub-actions с функцией `action.then`.
* `BABYLON.ActionManager.OnPickTrigger`: Происходит, когда пользователь touches/clicks по мешу.
* `BABYLON.ActionManager.OnDoublePickTrigger`: Происходит когда пользователь дважды touches/clicks по мешу.
* `BABYLON.ActionManager.OnPickDownTrigger`: Происходит когда пользователь касается или нажимает меш (момент касания/нажатия)
* `BABYLON.ActionManager.OnPickUpTrigger`: Происходит когда пользователь отпускает нажатие/касание меша.
* `BABYLON.ActionManager.OnPickOutTrigger`: Происходит когда пользователь касается или нажимает меш (момент касания/нажатия) и затем перемещает .
* `BABYLON.ActionManager.OnLeftPickTrigger`: Происходит когда пользователь touches/clicks по мешу with left button.
* `BABYLON.ActionManager.OnRightPickTrigger`: Происходит когда пользователь touches/clicks по мешу правой кнопкой.
* `BABYLON.ActionManager.OnCenterPickTrigger`: Происходит когда пользователь touches/clicks по мешу средней кнопкой.
* `BABYLON.ActionManager.OnLongPressTrigger`: Происходит когда пользователь touches/clicks up по мешу с задержкой (заданной в BABYLONActionManager.LongPressDelay).
* `BABYLON.ActionManager.OnPointerOverTrigger`: Происходит когда указатель покидает меш. Происходит только раз.
* `BABYLON.ActionManager.OnPointerOutTrigger`: Происходит когда указатель больше не над мешем. Происходит только раз.
* `BABYLON.ActionManager.OnIntersectionEnterTrigger`: Происходит когда меш находится в пересечении с другим мешем. Происходит только раз.
* `BABYLON.ActionManager.OnIntersectionExitTrigger`: Происходит когда меш больше не пересекается с другим мешем. Происходит только раз.
* `BABYLON.ActionManager.OnKeyDownTrigger`: Происходит когда нажата клавиша.
* `BABYLON.ActionManager.OnKeyUpTrigger`: Происходит когда клавиша отпущена
* `BABYLON.ActionManager.OnEveryFrameTrigger`: ???

Для триггеров пересечения вы должны указать "другой" mesh в следующем коде:

```javascript
mesh.actionManager.registerAction(new BABYLON.SetValueAction({ trigger: BABYLON.ActionManager.OnIntersectionEnterTrigger, parameter: otherMesh }, mesh, "scaling", new BABYLON.Vector3(1.2, 1.2, 1.2)));
```

Вы также можете определить, хотите ли вы использовать точные пересечения:

```javascript
mesh.actionManager.registerAction(new BABYLON.SetValueAction({ trigger: BABYLON.ActionManager.OnIntersectionEnterTrigger, parameter: { mesh:otherMesh, usePreciseIntersection: true} }, mesh, "scaling", new BABYLON.Vector3(1.2, 1.2, 1.2)));
```

Следующий список определяет триггеры, связанные со сценой:

* `BABYLON.ActionManager.OnEveryFrameTrigger`: Происходит один раз за кадр.
* `BABYLON.ActionManager.OnKeyDownTrigger`: Происходит когда нажата клавиша.
* `BABYLON.ActionManager.OnKeyUpTrigger`: Происходит при отпускании клавиши.

Для триггеров OnKeyUpTrigger и OnKeyDownTrigger , вы можете фильтровать события на основе клавиши, либо в вашем коде, либо с параметром:

```javascript
scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyUpTrigger, function (evt) {
   if (evt.sourceEvent.key == "r") {
       ...
   }
}));
scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction({ trigger: BABYLON.ActionManager.OnKeyUpTrigger, parameter: "r" },
  function () {
            ...
}));
```

## список Actions

Большинство action имеют свойство `propertyPath`. Эта строка определяет путь к свойству на которое влияет action. Вы можете использовать прямые значения, такие как `position` или `diffuse`. Но вы также можете создавать сложные пути, такие как `position.x`

* `BABYLON.SwitchBooleanAction`: Используется для переключения текущего значения логического свойства:

    `SwitchBooleanAction(trigger, target, propertyPath, condition)`

* `BABYLON.SetValueAction`: Используется для указания прямого значения для свойства:

    `SetValueAction(trigger, target, propertyPath, value, condition)`

* `BABYLON.IncrementValueAction`: Добавить указанное значение в свойство number:

    `IncrementValueAction(trigger, target, propertyPath, value, condition)`

* `BABYLON.PlayAnimationAction`: Запуск анимации для заданной цели:

    `PlayAnimationAction(trigger, target, from, to, loop, condition)`

* `BABYLON.StopAnimationAction`: Остановка анимации для заданной цели:

    `StopAnimationAction(trigger, target, condition)`

* `BABYLON.DoNothingAction`: Ничего не делать :)

    `DoNothingAction(trigger, condition)`

* `BABYLON.CombineAction`: Это action представляет собой контейнер. Вы можете использовать его для выполнения многих actions одновременно на одном и том же триггере. Свойство children должно быть массивом actions:

    `CombineAction(trigger, children, condition)`

* `BABYLON.ExecuteCodeAction`:Выполните свой собственный код, когда триггер активируется и условие - true:

    `ExecuteCodeAction(trigger, func, condition)`

* `BABYLON.SetParentAction`: Используется для определения родителя узла (camera, light, mesh):

    `SetParentAction(trigger, target, parent, condition)`

* `BABYLON.InterpolateValueAction`: Это действие создает анимацию для интерполяции текущего значения свойства на заданную цель. Поддерживаются следующие типы:
   * `number`
   * `BABYLON.Color3`
   * `BABYLON.Vector3`
   * `BABYLON.Quaternion`

    `InterpolateValueAction(trigger, target, propertyPath, value, duration, condition, stopOtherAnimations)`

* `BABYLON.PlaySoundAction` и `BABYLON.StopSoundAction`: Параметр "sound" является ссылкой на звук, который вы создали, используя `var sound = new BABYLON.Sound(...)`

    `PlaySoundAction(trigger, sound, condition)`

    `StopSoundAction(trigger, sound, condition)`

## Условия

Существует три вида условий:

* `BABYLON.ValueCondition`: Это условие истинно, когда заданное свойство равно / больше / меньше / отличается от определенного значения. Таким образом поддерживаются следующие операнды:

  * `BABYLON.ValueCondition.IsEqual`
  * `BABYLON.ValueCondition.IsDifferent`
  * `BABYLON.ValueCondition.IsGreater`
  * `BABYLON.ValueCondition.IsLesser`

    `ValueCondition(actionManager, target, propertyPath, value, operator)`

* `BABYLON.PredicateCondition`: Это условие использует предикат для определения его состояния:

    `PredicateCondition(actionManager, predicate)`

* `BABYLON.StateCondition`: Это условие проверяет свойство ```state``` объекта и сравнивает его с заданным значением:

    `StateCondition(actionManager, target, value)`

## Эксперименты с actions

Итак, в принципе, давайте представим, что вы хотите почти скрыть меш когда пользователь касается его.
Прежде всего, вы должны добавить к нему `BABYLON.ActionManager`:

```javascript
mesh.actionManager = new BABYLON.ActionManager(scene);
```

Затем вы можете создать action, которое будет связано с триггером `BABYLON.ActionManager.OnPickTrigger`. Это действие будет интерполировать свойство ```mesh.visibility``` до 0.2:

```javascript
var action = new BABYLON.InterpolateValueAction(BABYLON.ActionManager.OnPickTrigger, mesh, "visibility", 0.2, 1000);
```

Затем добавьте это действие в меш:

```javascript
mesh.actionManager.registerAction(action);
```

И вы сделали! Легко, правда?

Вы также можете связать другое действие, чтобы восстановить свойство `mesh.visibility` в значение по умолчанию:

```javascript
var action = new BABYLON.InterpolateValueAction(BABYLON.ActionManager.OnPickTrigger, mesh, "visibility", 0.2, 1000);
var action2 = new BABYLON.InterpolateValueAction(BABYLON.ActionManager.OnPickTrigger, mesh, "visibility", 1.0, 1000);
mesh.actionManager.registerAction(action).then(action2);
```

В этом случае первый щелчок скроет кнопку, следующий щелчок восстановит ее и так далее ...

## Спрайты

Начиная с Babylon.js 2.3, спрайты могут иметь менеджера действий: http://www.babylonjs...nd.com/#9RUHH#5

Обратите внимание, что SpriteManager должен включить поддержку выбора, используя `spriteManager.isPickable = true`
Спрайты также могут контролировать возможность быть выбранными через `sprite.isPickable = false / true` (False по умолчанию)

## Playground

Если вы хотите поиграть с действиями, вы можете попробовать их на нашем [playground](http://www.babylonjs.com/playground/?17)
