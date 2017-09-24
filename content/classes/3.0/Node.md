---
ID_PAGE: 25118
PG_TITLE: Node
PG_VERSION: 2.1
TAGS:
    - Node
---
## Описание

class [Node](/classes/3.0/Node)

[Node](/classes/3.0/Node) базовый класс для всех объектов сцены ([Mesh](/classes/3.0/Mesh), [Light](/classes/3.0/Light) [Camera](/classes/3.0/Camera)).

## Constructor

## new [Node](/classes/3.0/Node)(name, scene)

@constructor

#### Параметры
 | Имя | Тип | Описание
---|---|---|---
 | name | string |      Идентификатор узла
 | scene | [Scene](/classes/3.0/Scene) |      Сцена, связанная с этим узлом.
## Members

### name : string

Имя узла

### id : string

id узла

### uniqueId : number



### state : string

Состояние узла

### metadata : any



### doNotSerialize : boolean



### animations : [Animation](/classes/3.0/Animation)[]

Анимации узла

### onReady : (node: [Node](/classes/3.0/Node)) =&gt; void

Вызывается когда узел готов

### parent : [Node](/classes/3.0/Node)

Родитель узла

### onDisposeObservable : [Observable](/classes/3.0/Observable)&lt;[Node](/classes/3.0/Node)&gt;

Событие, инициируемое при размещении меша.

@type {BABYLON.[Observable](/classes/3.0/Observable)}

### onDispose : () =&gt; void



## Методы

### getClassName() &rarr; string


### getScene() &rarr; [Scene](/classes/3.0/Scene)

Получить сцену, связанную с этим узлом
### getEngine() &rarr; [Engine](/classes/3.0/Engine)

Получить engine связанный с этим узлом
### getWorldMatrix() &rarr; [Matrix](/classes/3.0/Matrix)

Получить матрицу мира (world matrix)
### updateCache(force) &rarr; void

Update the cache

#### Parameters
 | Name | Type | Description
---|---|---|---
optional | force | boolean |      True to force the update

### isSynchronizedWithParent() &rarr; boolean

Return true if the node is synchronized with parent
### isSynchronized(updateCache) &rarr; boolean

Return true if the node is synchronized

#### Parameters
 | Name | Type | Description
---|---|---|---
optional | updateCache | boolean |      True to update the cache

### hasNewParent(update) &rarr; boolean

Return true if the node has new parent

#### Parameters
 | Name | Type | Description
---|---|---|---
optional | update | boolean |      True to update the node

### isReady() &rarr; boolean

Is this node ready to be used/rendered

@return {boolean} is it ready
### isEnabled() &rarr; boolean

Включен ли этот узел.

Если узел имеет родительский элемент и включен, родитель также будет проверен.

@return {boolean} если этот узел (и его родитель) is enabled.

@see setEnabled
### setEnabled(value) &rarr; void

Установите разрешенное состояние этого узлаSet the enabled state of this node.

@see isEnabled

#### Parameters
 | Name | Type | Description
---|---|---|---
 | value | boolean |      True to set the node enable ; False otherwise

### isDescendantOf(ancestor) &rarr; boolean

Является ли этот узел потомком переданного узла.

Функция будет перебирать иерархию до тех пор, пока не будет найден предок или не будет определено больше родителей.

@see parent

#### Parameters
 | Name | Type | Description
---|---|---|---
 | ancestor | [Node](/classes/3.0/Node) |      The ancestor node to test

### getDescendants(directDescendantsOnly, predicate) &rarr; [Node](/classes/3.0/Node)[]

Вернет все узлы, которые имеют этот узел как восходящий.

@return {BABYLON.[Node](/classes/3.0/Node)[]} all children nodes of all types.

#### Parameters
 | Name | Type | Description
---|---|---|---
optional | directDescendantsOnly | boolean |   
optional | predicate | (node: [Node](/classes/3.0/Node)) =&gt; boolean | : an optional predicate that will be called on every evaluated children, the predicate must return true for a given child to be part of the result, otherwise it will be ignored.  
### getChildMeshes(directDecendantsOnly, predicate) &rarr; [AbstractMesh](/classes/3.0/AbstractMesh)[]

Получить все дочерние меши этого узла.

#### Parameters
 | Name | Type | Description
---|---|---|---
optional | directDecendantsOnly | boolean |   
optional | predicate | (node: [Node](/classes/3.0/Node)) =&gt; boolean |   
### getChildren(predicate) &rarr; [Node](/classes/3.0/Node)[]

Get all direct children of this node.

#### Parameters
 | Name | Type | Description
---|---|---|---
optional | predicate | (node: [Node](/classes/3.0/Node)) =&gt; boolean |   

### getAnimationByName(name) &rarr; [Animation](/classes/3.0/Animation)



#### Parameters
 | Name | Type | Description
---|---|---|---
 | name | string |      The node identifier

### createAnimationRange(name, from, to) &rarr; void



#### Parameters
 | Name | Type | Description
---|---|---|---
 | name | string |      The node identifier
 | from | number |    
 | to | number |    
### deleteAnimationRange(name, deleteFrames) &rarr; void



#### Parameters
 | Name | Type | Description
---|---|---|---
 | name | string |      The node identifier
optional | deleteFrames | boolean |    
### getAnimationRange(name) &rarr; [AnimationRange](/classes/3.0/AnimationRange)



#### Parameters
 | Name | Type | Description
---|---|---|---
 | name | string |      The node identifier

### beginAnimation(name, loop, speedRatio, onAnimationEnd) &rarr; void



#### Parameters
 | Name | Type | Description
---|---|---|---
 | name | string |      The node identifier
optional | loop | boolean |    
optional | speedRatio | number |    
### serializeAnimationRanges() &rarr; any


### dispose() &rarr; void


### static ParseAnimationRanges(node, parsedNode, scene) &rarr; void



#### Parameters
 | Name | Type | Description
---|---|---|---
 | node | [Node](/classes/3.0/Node) |    
 | parsedNode | any |    
 | scene | [Scene](/classes/3.0/Scene) |      The scene linked to this node.
