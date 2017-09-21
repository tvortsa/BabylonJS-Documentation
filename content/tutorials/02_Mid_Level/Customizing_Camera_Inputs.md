---
ID_PAGE: 29000
PG_TITLE: 19. Customizing camera inputs
---
Некоторые камеры Babylon.js's реагируют на ввод пользователя. Особенно ArcRotateCamera и FreeCamera. Babylon.js v2.4 представил другой способ управления вводом камеры to provide an approach oriented toward composability of inputs. Эти камеры теперь используют диспетчер ввода и каждый вход можно рассматривать как плагин, специфичный для семейства этой камеры, и заданному типу ввода (mouse, keyboard, gamepad, device orientation, ...).

Используя диспетчер ввода, вы можете добавлять, удалять, включать или отключать любой ввод, доступные для камеры. Вы также можете реализовать свой собственный механизм ввода или переопределить существующий, very easily.

Диспетчер ввода доступен на этих камерах через свойство, называемое "inputs".

```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
var inputManager = camera.inputs;
```

## Конфигурация вашего ввода

Most inputs provide settings to customize the sensibility and adapt it to your own scene.

Each input provides a short name available on the manager. The goal is to provide a friendly syntax when playing with your inputs.

```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
camera.inputs.add(new BABYLON.FreeCameraGamepadInput());
camera.inputs.attached.gamepad.gamepadAngularSensibility = 250;
```

## Adding an existing input
Input manager of both ArcRotateCamera and FreeCamera expose short-hand functions for adding built-in inputs.  

```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
camera.inputs.addGamepad();
```

If you wish, you can also add an instance of your own input (we will cover how to implement your own input at the end of this article).

```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
camera.inputs.add(new BABYLON.FreeCameraGamepadInput());
```

## Enable or disable inputs
When you call "attachControl" on the camera, you are activating all inputs attached to the input manager. In the same way, you could turn off all inputs by calling "detachControl" on the camera.

If you want to disable an input temporarily, you can call "detachControl" directly on the input... like this:

```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
camera.inputs.attached.mouse.detachControl();
camera.inputs.addGamepad();
```

You can then call "attachInput" when you want to turn it on again.
```javascript
camera.inputs.attachInput(camera.inputs.attached.mouse);
```

## Removing inputs
Sometimes you want a very specific input mechanism. The best approach in such case is probably to clear all inputs and add only those you may want in your scene.

```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
camera.inputs.clear();
camera.inputs.addMouse();
```

You can also remove a single input from your input manager. You can remove them by instance, or by Type name
```javascript
var camera = new BABYLON.FreeCamera("sceneCamera", new BABYLON.Vector3(0, 1, -15), scene);
//remove by instance
camera.inputs.remove(camera.inputs.attached.mouse);
//remove by type
camera.inputs.removeByType("FreeCameraKeyboardMoveInput");
```

## Implementing your own input
The input must be provided to the input manager as an object instance with a few required functions. If you use TypeScript, you could implement the interface ICameraInput.

Even if you don't use TypeScript for your project, you will probably understand the signature of the input from the interface

```javascript
interface ICameraInput<TCamera extends BABYLON.Camera> {   	
    // the input manager will fill the parent camera
    camera: TCamera;        

    //this function must return the type name of the camera, it could be used for serializing your scene
    getTypeName(): string;
    
    //this function must return the simple name that will be injected in the input manager as short hand
    //for example "mouse" will turn into camera.inputs.attached.mouse
    getSimpleName(): string;
    
    //this function must activate your input, event if your input does not need a DOM element
    attachControl: (element: HTMLElement, noPreventDefault?: boolean) => void;
    
    //detach control must deactivate your input and release all pointers, closures or event listeners
    detachControl: (element: HTMLElement) => void;        
    
    //this optional function will get called for each rendered frame, if you want to synchronize your input to rendering,
    //no need to use requestAnimationFrame. It's a good place for applying calculations if you have to
    checkInputs?: () => void;
}
```

Composable inputs is new, powerful, flexible, and extensible.  Familiarize yourself with its simple interface, and you will enjoy more and better camera control than ever before.

You can find an example here:  https://www.babylonjs-playground.com/#1WFOOA#2
