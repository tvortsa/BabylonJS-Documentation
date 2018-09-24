# Использование Materials Builder

## Открытие Materials Builder

Как и в случае с Post-Processes Builder, вы можете разрабатывать пользовательские материалы, используя JSON конфигурацию.
Просто выберите его в main tool bar.

Доступные функции:

* Разработка GLSL кода прямо в Editor (vertex и pixel)
* Управление кастомной uniforms (float, Vector2, Vector3, Vector4)
* Manage custom samplers (textures)

![OpeningMaterialsBuilder](/img/extensions/Editor/MaterialsBuilder/OpeningMaterialsBuilder.png)

## Добавление нового материала

Перед открытием Materials Builder, вы можете добавить новый материал или выбрать существующий, чтобы редактировать его.
Чтобы добавить новый материал, просто нажмите "**Add New**: затем создается новый материал с файлами вершин, пикселей и конфигурации по умолчанию.

Чтобы отредактировать материал, просто выберите его и нажмите кнопку "**Select**"

![AddingMaterial](/img/extensions/Editor/MaterialsBuilder/AddingMaterial.png)

## Используем Materials Builder

После открытия, теперь вы можете настроить uniforms & samplers, и отредактировать сод для vertex & pixel shaders.

Слева у вас есть инструмент редактирования, который позволяет вам настроить материал:

* The material's name
* Build the material

И сценарий предварительного просмотра:

* Enable / disable shadows
* Enable / disable lights (проверить, поддерживаются ли все типы освещения вашим шейдером)

![MaterialsBuilder](/img/extensions/Editor/MaterialsBuilder/MaterialsBuilder.png)

## Конфигурация

Вкладка «Конфигурация» позволяет объявлять пользовательские uniforms and samplers.
В материале по умолчанию доступны все доступные параметры, такие как "**time**", используются в качестве примера (здесь время используется функцией волн в вершинном шейдере по умолчанию).

Для пробников параметр "**uniformName**" это важно, он используется для объявления текстурной матрицы и текстуры в вершинном шейдере.

![Configuration](/img/extensions/Editor/MaterialsBuilder/Configuration.png)

## Вершинный шейдер

The vertex and pixel shaders follow the way to create materials with Babylon.js. A lot of code is already written then you only have to include files (**#include**).
All default "includes" are already implemented in default material.
In the default material, a custom waves function is available as an example line 64

![VertexShader](/img/extensions/Editor/MaterialsBuilder/VertexShader.png)

On line 26, the uniforms related to the sampler named "**myTexture**" (in samplers configuration) are available as example.
The uniforms "**myTextureMatrix**" and "**vMyTextureInfos**" are sent automatically by the engine following the name you set in configuration: here "**myTexture**".

Free to you to use it in your vertex shader :)

![VertexShaderTexture](/img/extensions/Editor/MaterialsBuilder/VertexShaderTexture.png)

## The pixel shader

As for vertex shader, the uniforms "**vMyTextureInfos**" and "**myTextureSampler**" are set automatically by the engine.
Free to you to use it in the pixel shader

![PixelShader](/img/extensions/Editor/MaterialsBuilder/PixelShader.png)

## Building the material

In order to preview the material in the preview scene, just click the button "**Build Material**" in the edition tool (on the left).
Then, the material is applied on the mesh you specified in the edition tool (default "**Box**").

Once built, new fields are created in edition tool:
* Uniforms
* Samplers

These fields are used to realtime customize your material in order to get your configuration perfect.

![MaterialApplied](/img/extensions/Editor/MaterialsBuilder/MaterialApplied.png)

## Applying your new material on a mesh

Once built, you can apply your material in the main scene of your project. Then, apply the material on one/multiple meshes.
Just click "**Apply on scene**".

![ApplyOnScene](/img/extensions/Editor/MaterialsBuilder/ApplyOnScene.png)

Then, select a mesh in your scene and set the material you created :)

![ApplyOnMesh](/img/extensions/Editor/MaterialsBuilder/ApplyOnMesh.png)

# Known limitations

* Once the material is built, only 2D textures preview are supported in "**Samplers**" menu, in edition tool
