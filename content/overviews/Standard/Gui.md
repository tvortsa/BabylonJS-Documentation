# Babylon.GUI

Библиотека Babylon.js GUI это расширение которое можно использовать для создания интерактивного пользовательского интерфейса0.
Она построена поверх DynamicTexture.

Последнюю версию можно найти здесь: https://github.com/BabylonJS/Babylon.js/tree/master/dist/preview%20release/gui.

Исходники доступны в главном реппозитории Babylon.js : https://github.com/BabylonJS/Babylon.js/tree/master/gui.

Здесь вы можете найти демо: http://www.babylonjs.com/demos/gui/

![Babylon.GUI](http://www.babylonjs.com/screenshots/gui.jpg)

## Введение
Babylon.GUI использует DynamicTexture для генерации полно-функционального интерфейса. Это альтернатива [Canvas2D](http://doc.babylonjs.com/extensions/Canvas2D_home).

Основное отличие в том, что Canvas2D полностью GPU - ориентирован (text constructrion, animations, etc..) а Babylon.GUI полагается на HTML canvas API.

Хотя это можно рассматривать как менее производительный подход, он также более гибкий. Более того, HTML canvas также GPU accelerated в большинстве браузеров.

## AdvancedDynamicTexture
Чтобы работать с Babylon.GUI, сперва вам нужен объект AdvancedDynamicTexture.

Babylon.GUI имеет два режима:
* Fullscreen mode: В котором, Babylon.GUI будет охватывать весь экран и будет масштабироваться, чтобы всегда адаптироваться к вашему разрешению экрана. Он также будет перехватывать клики (включая касания). Для создания AdvancedDynamicTexture в полно-экранном режиме, просто запустите этот код:

```
var advancedTexture = BABYLON.GUI.AdvancedDynamicTexture.CreateFullscreenUI("myUI");
```

Вот пример простого fullscreen mode GUI:  https://www.babylonjs-playground.com/#XCPP9Y#1

* Texture mode: в этом режиме, BABYLON.GUI будет использовать текстуру для переданного меша. Вам нужно будет определить разрешение вашей текстуры. Для создания AdvancedDynamicTexture в texture mode, запустите такой код:

```
var advancedTexture2 = BABYLON.GUI.AdvancedDynamicTexture.CreateForMesh(myPlane, 1024, 1024);
```

Вот пример простого texture mode GUI:  https://www.babylonjs-playground.com/#ZI9AK7#1

Обратите внимание, что обработка событий перемещения указателя мыши может быть дорогостоящей на сложных мешах, поэтому вы можете отключить отслеживание перемещения указателя четвертым параметром:

```
var advancedTexture2 = BABYLON.GUI.AdvancedDynamicTexture.CreateForMesh(myPlane, 1024, 1024, false);
```

Получив объект AdvancedDynamicTexture, вы можете начинать добавлять контролы.

## Основные свойства

### События
Все контролы имеют следующих наблюдателей:

Наблюдатели|Комментарии
-----------|--------
onPointerMoveObservable|Происходит когда курсор входит в границы контрола. Доступно только в полноэкранном режиме
onPointerEnterObservable|Происходит когда курсор enters the control. Доступно только в полноэкранном режиме
onPointerOutObservable|Происходит когда курсор покидает control. Доступно только в полноэкранном режиме
onPointerDownObservable|Происходит когда указатель is down on the control.
onPointerUpObservable|Происходит когда указатель is up on the control.

Вы можете также сделать control невидимым для событий (поэтому вы можете щелкнуть по нему, например). Для чего просто вызовите: `control.isHitTestVisible`.

Заметьте, что `onPointerMoveObservable`, `onPointerDownObservable` и `onPointerUpObservable` принимают параметр Vector2 содержащий координаты указателя. Если вы хотите получить координаты указателя в локальном пространстве контрола, вызовите `control.getLocalCoordinates(coordinates)`.

Вот пример того как использовать observables:  https://www.babylonjs-playground.com/#XCPP9Y#121

### Выравнивание
Вы можете определить выравнивания, используемые вашим элементом управления, со следующими свойствами:

Свойство|Дефолтно|Коммент.
--------|-------|--------
horizontalAlignment|BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_CENTER|Может быть left, right или center.
verticalAlignment|BABYLON.GUI.Control.VERTICAL_ALIGNMENT_CENTER|Может быть top, bottom или center.

Вот пример использования alignments:  https://www.babylonjs-playground.com/#XCPP9Y#13

### Положение и размер
Вы можете установить позицию элемента управления со следующими свойствами:

Свойство|Тип|Default|Default unit
--------|----|-------|------------
left|valueAndUnit|0|Pixel
top|valueAndUnit|0|Pixel

Размер можно задать:

Свойство|Тип|Default|Default unit
--------|----|-------|------------
width|valueAndUnit|100%|Percentage
height|valueAndUnit|100%|Percentage

Paddings можно задать:

Свойство|Тип|Default|Default unit
--------|----|-------|------------
paddingTop|valueAndUnit|0px|Pixel
paddingBottom|valueAndUnit|0px|Pixel
paddingLeft|valueAndUnit|0px|Pixel
paddingRight|valueAndUnit|0px|Pixel

Заметьте, что paddings внутри control. То-есть: usableWidth = width - paddingLeft - paddingRight. И так же для usableHeight = height - paddingTop - paddingBottom.

Все эти свойства можно задавать в пикселях или в процентах.
В пикселях: `control.left = "50px"`
В процентах: `control.left = "50%"`

Можно и не указывать единицы измерения (тогда будут использоваться единицы измерения по-умолчанию): `control.width = 0.5` (эквивалентно `control.width = "50%"`)

Вот пример использования positions и sizes:  https://www.babylonjs-playground.com/#XCPP9Y#14

### Трекинг положения
Все элементы управления можно перемещать для отслеживания положения сетки.
Для чего, просто вызовите `control.linkWithMesh(mesh)`. Затем вы можете смещать позицию с помощью `control.linkOffsetX` и `control.linkOffsetY`.

Вот пример trackable label:  https://www.babylonjs-playground.com/#XCPP9Y#16

Заметьте, что контролы которые хотят отслеживать положение сетки, должны быть на корневом уровне (на уровне AdvancedDynamicTexture).

Вы также можете переместить элемент управления на определенные координаты в вашей сцене `control.moveToVector3(position)`. Заметьте, что контролы не будет придерживаться вектора, если вы измените его впоследствии.

Для Line control, вы доложны также присоединить вторую точку к control с помощью `line.connectedControl = control`. Тогда свойства `x2` и `y2` используются для смещения второй точки от присоединенного контрола.

С этими двумя опциями вы можете создать полностью trackable label:  https://www.babylonjs-playground.com/#XCPP9Y#20

### Адаптивное масштабирование
В полноэкранном UI, вы можете задавать фиксированное разрешение UI.
Просто задайте `myAdvancedDynamicTexture.idealWidth = 600` **или** `myAdvancedDynamicTexture.idealHeight = 400`.

Если заданы оба, используется idealWidth.

Когда ideal resolution задан, все значения, выраженные **в пикселях** считаются относительно этого разрешения и масштабируются в соответствии с текущим разрешением.

Даже если ideal size задан, полноэкранный UI будет рендериться в том же разрешении вашего холста, но вы можете решить (прежде всего из соображений производительности) чтобы заставить текстуру использовать идеальный размер для разрешения. Для этого просто вызовите `myAdvancedDynamicTexture.renderAtIdealSize = true`.

Вот пример использования horizontal adaptive scaling:  https://www.babylonjs-playground.com/#XCPP9Y#39

### Вращение и масштабирование

Controls можно трансформировать с помощью следующих свойств:

Свойство|Type|Default|Comments
--------|----|-------|--------
rotation|number|0|Значение в радианах
scaleX|number|1|
scaleY|number|1|
transformCenterX|number|0.5|Определить центр трансформации по оси X. Значение между 0 и 1
transformCenterY|number|0.5|Определить центр трансформации по оси Y. Значение между 0 и 1

**Пожалуйста, убедитесь, что преобразования выполняются на уровне рендеринга, после всех вычислений.** Это означает, что выравнивание или позиционирование будут выполняться первыми без учета трансформирования.

Пример использования rotation and scaling:  https://www.babylonjs-playground.com/#XCPP9Y#22

## Controls

Control это абстрактная часть UI. Есть два вида контролов:
* Чистый контрол: определяет действие или информацию, полезную для пользователя. Например TextBlock или Button.
* Контейнеры: Контейнеры используют для организации вашего UI. Они могут содержать другие элементы управления или контейнеры.

Все контролы имеют следующие свойства:

Свойство|Тип|Default|Коммент
--------|----|-------|--------
alpha|number|1|Между 0 и 1. 0 - полностью прозрачный. 1 - полностью непрозрачный
color|string|Black|Цвет переднего плана
fontFamily|string|Arial|Семейство шрифтов может быть унаследовано. Тоесть, если вы зададите его для контейнера, оно будет передано всем детям контейнера
fontStyle|string|Empty string|может быть унаследовано. Значения могут быть: "italic", "bold" или "oblique"
fontSize|number|18|может быть унаследовано
zIndex|number|0|zIndex используют для упорядочивания по оси z 

Controls можно добавлять прямо в AdvancedDynamicTexture или в контейнер:

```
container.addControl(control);
```

Контрол может быть удален:

```
container.removeControl(control);
```

Можно также управлять видимостью контролов `control.isVisible = false`.

### TextBlock

TextBlock это простой контрол используемый для отображения текста:  https://www.babylonjs-playground.com/#XCPP9Y#2

Вот его свойства:

Свойство|Тип|Default|Comments
--------|----|-------|--------
text|string|null|отображаемый текст
textWrapping|boolean|false|может быть true для включения переноса текста
textHorizontalAlignment|number|BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_CENTER|может быть: left, right или center
textVerticalAlignment|number|BABYLON.GUI.Control.VERTICAL_ALIGNMENT_CENTER|может быть: top, bottom или center

### InputText

Контрол InputText чтобы дать пользователю возможность ввода строки текста: https://www.babylonjs-playground.com/#UWS0TS

Вот его свойства:

Свойство|Тип|Default|Comments
--------|----|-------|--------
text|string|null|отображаемый текст
color|string|white|Цвет переднего плана
background|string|black|Цвет фона
focusedBackground|string|black|Цвет фона, используемый при фокусировке на контроле
autoStretchWidth|boolean|true|контрол может подгоняться по размеру горизонтально для адаптации под текст
maxWidth|valueAndUnit|100%|Максимально доступная ширина при установленном в true autoStretchWidth 
margin|valueAndUnit|10px|Margin используется left и right внутри самого контрола. Этот margin используется для определения места, где будет нарисован текст
thickness|number|1|Толщина рамки

InputText это фокусируемый контрол. Это значит вы можете кликнуть / тачнуть it in order to give it the focus and control over the keyboard events. You can remove the focus from the control by hitting enter or clicking outside of the control.

Контрол предоставляет несколько наблюдателей чтобы отслеживать его состояние:

Observables|Comments
-----------|--------
onTextChangedObservable|Наступает когда текст изменен
onFocusObservable|Наступает когда контрол теряет фокус
onBlurObservable|Наступает когда контрол получает фокус

Имейте в виду, что InputText имеет довольно ограниченные возможности редактирования. Поддерживаются клавиши:
* Delete
* Backspace
* Home
* End
* Enter
* Left / Right (used to move the cursor)

Furthermore, please note that due to JavaScript platform limitation, the InputText cannot invoke the onscreen keyboard. On mobile, the InputText will use the `prompt()` command to get user input. You can define the title of the prompt by setting `control.promptMessage`.

### Button

A button can be used to interact with your user.
Please see the events chapter to see how to connect your events with your buttons.

There are three kinds of buttons available out of the box:

* ImageButton: An image button is a button made with an image and a text. You can create one with:

```
var button = BABYLON.GUI.Button.CreateImageButton("but", "Click Me", "textures/grass.png");
```

You can try it here:  https://www.babylonjs-playground.com/#XCPP9Y#3

* SimpleButton: A simple button with text only

```
var button = BABYLON.GUI.Button.CreateSimpleButton("but", "Click Me");
```

You can try it here:  https://www.babylonjs-playground.com/#XCPP9Y#4

* ImageOnlyButton:

```
var button = BABYLON.GUI.Button.CreateImageOnlyButton("but", "textures/grass.png");
```

You can try it here:  https://www.babylonjs-playground.com/#XCPP9Y#28

#### Visual animations
By default a button will change its opacity on pointerover and will change it scale when clicked.
You can define your own animations with the following callbacks:

* pointerEnterAnimation
* pointerOutAnimation
* pointerDownAnimation
* pointerUpAnimation

#### Custom button
You can also create a complete custom button by manually adding children to the button. Here is how the ImageButton is built:

```
var result = new Button(name);

// Adding text
var textBlock = new BABYLON.GUI.TextBlock(name + "_button", text);
textBlock.textWrapping = true;
textBlock.textHorizontalAlignment = BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_CENTER;
textBlock.paddingLeft = "20%";
result.addControl(textBlock);   

// Adding image
var iconImage = new BABYLON.GUI.Image(name + "_icon", imageUrl);
iconImage.width = "20%";
iconImage.stretch = BABYLON.GUI.Image.STRETCH_UNIFORM;
iconImage.horizontalAlignment = BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
result.addControl(iconImage);            

return result;
```  

### Checkbox

The checkbox is used to control a boolean value.
You can specify the value with `checkbox.isChecked`.

Changing the `isChecked` property will raise an observable called `checkbox.onIsCheckedChangedObservable`.

The control is rendered using the following properties:

Свойство|Тип|Default|Comments
--------|----|-------|--------
color|string|white|Foreground color
background|string|black|Background color
checkSizeRatio|number|0.8|Define the ratio used to compute the size of the inner checkbox (0.8 by default, which means the inner check size is equal to 80% of the control itself)

Here is an example of a checkbox: https://www.babylonjs-playground.com/#U9AC0N#2

### RadioButton

The radio button is used to define a value among a list by using a group of radio buttons where only one can be true.
You can specify the selected value with `radiobutton.isChecked`.

Changing the `isChecked` property will raise an observable called `checkbox.onIsCheckedChangedObservable`. Furthermore, if you select a radio button, all other radio buttons within the same group will turn to false.

The control is rendered using the following properties:

Property|Тип|Default|Comments
--------|----|-------|--------
color|string|white|Foreground color
background|string|black|Background color
checkSizeRatio|number|0.8|Define the ratio used to compute the size of the inner checkbox (0.8 by default, which means the inner check size is equal to 80% of the control itself)
group|string|empty string|Use the group property to gather radio buttons working on the same value set

Here is an example of a radiobutton: https://www.babylonjs-playground.com/#U9AC0N#13

### Slider

The slider is used to control a value within a range.
You can specify the range with `slider.minimum` and `slider.maximum`.

The value itself is specified with `slider.value` and will raise an observable everytime it is changed (`slider.onValueChangedObservable`).

The control is rendered using the following properties:

Свойство|Type|Default|Comments
--------|----|-------|--------
borderColor|string|white|Color used to render the border of the thumb
color|string|white|Foreground color
background|string|black|Background color
barOffset|valueAndUnit|5px|Offset used vertically to draw the background bar
thumbWidth|valueAndUnit|30px|Width of the thumb

Here is an example of a slider: https://www.babylonjs-playground.com/#U9AC0N#1

### Line

The line will draw a line (!!) between two points.

Here are the properties you can define:

Свойство|Тип|Default|Comments
--------|----|-------|--------
x1|number|0|X coordinate of the first point
y1|number|0|Y coordinate of the first point
x2|number|0|X coordinate of the second point
y2|number|0|Y coordinate of the second point
dash|array of numbers|Empty array|Defines the size of the dashes
lineWidth|number|1|Width in pixel

Here is an example of a line:  https://www.babylonjs-playground.com/#XCPP9Y#6

### Image

Use the image control to display an image in your UI.
You can control the stretch used by the image with `image.stretch` property. You can set it to one of these values:
* BABYLON.GUI.Image.STRETCH_NONE: Use original size
* BABYLON.GUI.Image.STRETCH_FILL: Scale the image to fill the container (This is the default value)
* BABYLON.GUI.Image.STRETCH_UNIFORM: Scale the image to fill the container but maintain aspect ratio
* BABYLON.GUI.Image.STRETCH_EXTEND: Scale the container to adapt to the image size.

You may want to have the Image control adapt its size to the source image. To do so just call `image.autoScale = true`.

You can change image source at any time with `image.source="myimage.jpg"`.

You can also define which part of the source image you want to use with the following properties:
* sourceLeft: x coordinate in the source image (in pixel)
* sourceTop: y coordinate in the source image (in pixel)
* sourceWidth: width of the source image you want to use (in pixel)
* sourceHeight: height of the source image you want to use (in pixel)

Here is an example of an image:  https://www.babylonjs-playground.com/#XCPP9Y#7

### VirtualKeyboard

The VirtualKeyboard is a control used to display simple onscreen keyboard. This is mostly useful with WebVR scenarios where the user cannot easily use his keyboard.

#### Keys

Вы можете определить клавиши, предоставленные клавиатурой, следующим кодом:

```
var keyboard = new BABYLON.GUI.VirtualKeyboard();
keyboard.addKeysRow(["1", "2", "3", "4", "5", "6", "7", "8", "9", "0","\u2190"]);
```

Every key will be created using default values specified by the following properties:

Свойство|Default
--------|----
defaultButtonWidth|40px
defaultButtonHeight|40px
defaultButtonPaddingLeft|2px
defaultButtonPaddingRight|2px
defaultButtonPaddingTop|2px
defaultButtonPaddingBottom|2px
defaultButtonColor|#DDD
defaultButtonBackground|#070707

You can also override each property by providing an array containing properties for keys (or null):

```
addKeysRow(["a", "b"], [null, { width: "200px"}]);
```

You can define each default properties based on the following class:
```
class KeyPropertySet {
      width?: string;
      height?: string;
      paddingLeft?: string;
      paddingRight?: string;
      paddingTop?: string;
      paddingBottom?: string;
      color?: string;
      background?: string;
  }
```

#### Layouts

The VirtualKeyboard provides a static method to create a default layout:

```
var keyboard = BABYLON.GUI.VirtualKeyboard.CreateDefaultLayout();
```

The default layout is equivalent to:

```
addKeysRow(["1", "2", "3", "4", "5", "6", "7", "8", "9", "0","\u2190"]);
addKeysRow(["q", "w", "e", "r", "t", "y", "u", "i", "o", "p"]);
addKeysRow(["a", "s", "d", "f", "g", "h", "j", "k", "l",";","'","\u21B5"]);
addKeysRow(["z", "x", "c", "v", "b", "n", "m", ",", ".", "/"]);
addKeysRow([" "], [{ width: "200px"}]);
```

#### Events
Every time a key is pressed the `onKeyPressObservable` observable is triggered. But you can also rely on `keyboard.connect(inputText)` to automatically connect a VirtualKeyboard to an InputText. In this case, the keyboard will only appear when the InputText will be focused and all key pressed events will be sent to the InputText.

You can find a complete demo here: https://www.babylonjs-playground.com/#S7L7FE

## Containers

The containers are controls used to host other controls. Use them to organize your UI.
Containers has one specific property: `container.background`. Use it to define the background color of your container.

### Rectangle
The Rectangle is a rectangular container with the following properties:

Свойство|Type|Default|Comments
--------|----|-------|--------
thickness|number|1|Thickness of the border
cornerRadius|number|0|Size in pixel of each corner. Used to create rounded rectangles

Here is an example of a rectangle control:  https://www.babylonjs-playground.com/#XCPP9Y#8

### Ellipse
The Ellipse is a ellipsoidal container with the following properties:

Свойство|Type|Default|Comments
--------|----|-------|--------
thickness|number|1|Thickness of the border

Here is an example of an ellipse control:  https://www.babylonjs-playground.com/#XCPP9Y#10

### StackPanel

The StackPanel is a control which stacks its children based on its orientation (can be horizontal or vertical).
All children must have a defined width or height (depending on the orientation).

The height (or width) of the StackPanel is defined automatically based on children.

Here is an example of a StackPanel:  https://www.babylonjs-playground.com/#XCPP9Y#11

### ColorPicker

The color picker control allows users to set colors in your scene.

Whenever a user interacts with the color picker an observable is triggered (`colorPicker.onValueChangedObservable`) which returns the current value (Color3) of the color picker.

The control is rendered using the following properties:

Свойство|Тип|Default|Comments
--------|----|-------|--------
size|string or number|"200px"|The size, width, and height property will always be the same value since the color picker can only be a square.


Here is an example of a color picker: https://www.babylonjs-playground.com/#91I2RE#1


## Helpers

To reduce the amount of code required to achieve frequent tasks you can use the following helpers:

* `BABYLON.GUI.Control.AddHeader(control, text, size, options { isHorizontal, controlFirst })`: This function will create a StackPanel (horizontal or vertical based on options) and will add your control plus a TextBlock in it. Options can also be used to specify if the control is inserted first of after the header. Depending on the orientation, size will either specify the widht or the height used for the TextBlock.
