# Введение

![Введение](/img/extensions/Editor/editor.png)

Для быстрого и полного ознакомления с видеороликами вы можете прочитать это сообщение : [https://medium.com/babylon-js/welcome-to-the-babylon-js-editor-c08dccdcec07#.e1lm87d4g](https://medium.com/babylon-js/welcome-to-the-babylon-js-editor-c08dccdcec07#.e1lm87d4g)

Babylon.js Editor является заключительным этапом для художников и разработчиков в сценах.
Он не предоставляет нескольких инструментов (или поддерживается экспортерами) как в 3D редакторах таких как 3ds Max, Blender, etc.

В качестве примера Babylon.js Materials Library, который не поддерживается 3D редакторами, поддерживается в Babylon.js Editor.

Другими словами, этот редактор является Web Application предоставление нескольких инструментов, помогающих художникам (and developers) отлаживать, анимировать,конфигурировать и экспортировать сцены Babylon.js. Другими словами, этот editor обеспечивает необязательный заключительный этап (в добавок к Babylon.js экспортерами 3ds Max, Blender, Unity3D, etc.) дизайнерам, прежде чем они выпустят свои финальные сцены.

Редактор Babylon.js Editor можно найти здесь: [http://editor.babylonjs.com/](http://editor.babylonjs.com/)

Github Repository можно найти здесь: [https://github.com/BabylonJS/Editor](https://github.com/BabylonJS/Editor)

## Доступные функции

### С версии v0.8

* Создание и редактирование систем частиц
* Создание и редактирование анимаций
* Создание и редактирование систем объективов
* Сохранить проекты на OneDrive (Drop Box появятся в будущих версиях)
* Развертывание шаблона проекта на OneDrive (Drop Box появятся в будущих версиях)
* Cinematic редактор
* Scene graph просмотр
* Создание и редактирование постпроцесса (вскоре экспортируется в финал .babylon сцены)
* Создание и редактирование целей рендеринга (вскоре экспортируется в финал .babylon сцены)

## From v0.9

* Создание и редактирование материалов (complete Babylon.js Materials Library)
* Импорт и настройка текстур для использования с материалами
* Предварительный просмотр рендеринга (including shadow maps)

## Coming in v1.0 (current)

* поддержка Actions Builder

## Coming in v1.1

* Установка и тестирование физических симуляций, включающих новые обновления RaananW
* инструмент Shader Materials Builder

## Теперь, что явно экспортируется?

* Конфигурация проекта (FPS, animated at launch)
* Системы частиц
* Блики
* Пост-процессы (not yet serialized in .babylon files)
* Анимации
* Skies
* Render target textures
* Пробы отражений (not yet serialized in .babylon files)
* Материалы из библиотеки материалов
* Actions с помощью Actions Builder
* Пользовательские метаданные, используемые расширениями (Post-Process Builder, etc.)
