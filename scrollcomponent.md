# ScrollComponent

使用滚动组件来滚动内容，它支持自定义动量和物理弹性曲线，并发射不同事件。
>A ScrollComponent is used to scroll content. It implements momentum and spring physics, allows for customization, and emits different events.

滚动组件由两个图层组成，它本身作为遮罩的图层和内容图层。内容图层能够拖拽和约束，能够基于内容层中所有子层的总大小自动调整内容层的大小。
>The ScrollComponent is built with two layers. The ScrollComponent itself is a layer that masks its content. It has a content layer that has draggable enabled and constraints configured. It automatically manages the size of the content layer based on the total size of the sub layers of the content layer.

```coffeescript
     # Create a new ScrollComponent 
    scroll = new ScrollComponent
      width: 100
      height: 100
 
    # Include a Layer 
    layerA = new Layer
        parent: scroll.content
```

你也可以使用`ScrollComponent.wrap()`包裹一个已有图层，滚动组件会将自己插入到内容层与其父层之间。当你从Sketch或Photoshop导入设计并希望使图层滚动时，这会很有帮助。你可以在本章节了解更多有关于包裹图层的信息。
>You can also wrap an existing layer within a ScrollComponent, using ScrollComponent.wrap(). The ScrollComponent will insert itself in-between the content and its super layer. This is useful when you've imported designs from Sketch or Photoshop and want to make a layer scrollable. You can learn more about wrapping in the learn section.

```coffeescript

    layerA = new Layer
        width: 300
        height: 300
 
    scroll = ScrollComponent.wrap(layerA)
```
<a id="scroll.content"></a>
## scroll.content(layer)

将要导入内容的图层。要导入内容，先创建图层并把它的父级设置为`scroll.content`。当内容图层尺寸超过滚动组件时，将会被裁切。
>The layer to add content to. To add content, create a new Layer and set its parent to the scroll.content layer. When the content doesn't fit the ScrollComponent it will be clipped.

```coffeescript
    scroll = new ScrollComponent
      width: 100
      height: 100
 
    layerA = new Layer
        parent: scroll.content
        image: "images/bg.png"
        width: 100
        height: 200
```

<a id="scroll.contentInset"></a>
## scroll.contentInset(对象)

内容区域的内边距。将会在实际图层和约束区域内添加额外的填充空间。
>Inset for the content. This will give your content extra padding between the constraints and the actual content layers.

```coffeescript
    scroll = new ScrollComponent
        width: 100
        height: 100
 
    layerA = new Layer
        parent: scroll.content
        image: "images/bg.png"
        width: 100
        height: 200

    scroll.contentInset =
        top: 20
        right: 0
        bottom: 20
        left: 0
```

<a id="scroll.speedX"></a>
## scroll.speedX(数字)

改变水平方向滚动速度，其值是一个0到1的数字，默认为1。
>Horizontal scrolling speed, number between 0 and 1. Default value is 1.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content 

    scroll.speedX = 0.5
```

<a id="scroll.speedY"></a>
## scroll.speedY(数字)

改变垂直方向滚动速度，其值是一个0到1的数字，默认为1。
>Vertical scrolling speed, number between 0 and 1. Default value is 1.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content 

    scroll.speedY = 0.5
```
<a id="scroll.scroll"></a>
## scroll.scroll(布尔值)

启用或禁用滚动，默认启用。禁用状态将会同时禁用水平方向和垂直方向。
>Enable or disable scrolling. Enabled by default. If you set this to false, it will set both scrollVertical and scrollHorizontal to false.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content

    scroll.scroll = false
```

<a id="scroll.scrollHorizontal"></a>
## scroll.scrollHorizontal(布尔值)

启用或禁用水平方向滚动
>Enable or disable horizontal scrolling.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content

    scroll.scrollHorizontal = false
```

<a id="scroll.scrollVertical"></a>
## scroll.scrollVertical(布尔值)

启用或禁用垂直方向滚动
>Enable or disable vertical scrolling.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content

    scroll.scrollVertical = false
```

<a id="scroll.scrollX"></a>
## scroll.scrollX(数字)

水平滚动坐标
>Horizontal scroll location.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content

    scroll.scrollX = 250
```
<a id="scroll.scrollY"></a>
## scroll.scrollY(数字)

垂直滚动坐标
>Vertical scroll location.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content 

    scroll.scrollY = 250
```

<a id="scroll.scrollPoint"></a>
## scroll.scrollPoint(对象)

使用x和y数值来定义滚动坐标
>Define the scroll location with x and y properties.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content

    scroll.scrollPoint =
        x: 0
        y: 50
```

<a id="scroll.scrollFrame"></a>
## scroll.scrollFrame(对象)

可见滚动框
>Visible scroll frame.

```coffeescript
    scroll = new ScrollComponent

    layerA = new Layer
        parent: scroll.content

    scroll.scrollFrame =
        x: 0
        y: 250
        width: 250
        height: 250
```

<a id="scroll.velocity"></a>
## scroll.velocity(数字)

当前滚动速度和方向（以每秒像素为单位）
>Current scroll speed and direction in pixels per second at this current time.

```coffeescript
    scroll = new ScrollComponent

    # On scroll, print the velocity 
    scroll.on Events.Scroll, ->
        print scroll.velocity
```

<a id="scroll.direction"></a>
## scroll.direction(字符串)

当前滚动方向，会返回"up", "down", "left" 或 "right"中的一个。滚动方向与拖动方向相反：当向下拖动时，实际上向上滚动。（只读）
>Current scrolling direction. Returns "up", "down", "left", or "right". The scrolling direction is the inverse of the direction of the drag action: when dragging downwards, you're effectively scrolling upwards. (Read-only)

```coffeescript
    scroll = new ScrollComponent

    # On scroll, print the direction 
    scroll.on Events.Scroll, ->
        print scroll.direction
```

<a id="scroll.directionLock"></a>
## scroll.directionLock(布尔值)

在滚动距离超过某一上限之后，限定你只能在垂直和水平中的一个方向进行滚动。
>Snap to horizontal/vertical direction after a certain threshold.

```coffeescript
    scroll = new ScrollComponent

    # Allow dragging only in one direction at a time 
    scroll.directionLock = true
```

<a id="scroll.directionLockThreshold"></a>
## scroll.directionLockThreshold(对象)

锁定滚动方向的上限。x和y的值代表在它锁定方向之前你可以在两个方向上滚动的距离。
>The thresholds for lock directions. The x and y values represent the distance you can drag in a certain direction before it starts locking.

```coffeescript
    scroll = new ScrollComponent

    # Snap horizontally after dragging 50px 
    # Snap vertically instantly 
    scroll.directionLock = true

    scroll.directionLockThreshold =
        x: 50
        y: 0
```

<a id="scroll.angle"></a>
## scroll.angle(数字)

当前滚动角度（以度为单位）。滚动角度和拖动角度方向相反：当向下拖动时，实际上向上滚动。（只读）
>Current scrolling angle (in degrees). The scrolling angle is the inverse of the direction of the drag action: when dragging downwards, you're effectively scrolling upwards. (Read-only)

```coffeescript
    scroll = new ScrollComponent

    # On scroll, print the angle 
    scroll.on Events.Scroll, ->
        print scroll.angle
```

<a id="scroll.isDragging"></a>
## scroll.isDragging(布尔值)

判断现在某个图层是否正在滚动（松开后动画时返回的是false），它是只读的。
>Whether the layer is currently being dragged (returns false when animating). (Read-only)

```coffeescript
    scroll = new ScrollComponent

    # Check if the layer is being dragged 
    scroll.onMove ->
        print scroll.isDragging
```

<a id="scroll.isMoving"></a>
## scroll.isMoving(布尔值)

判断当前图层是否在移动，无论是因为拖动移动还是因为模拟动量或弹性动画，它是只读的
>Whether the content is currently moving, either by dragging or by a momentum/bounce animation. (Read-only)

```coffeescript
    scroll = new ScrollComponent

    # Check if the layer is moving 
    scroll.onMove ->
        print scroll.isMoving
```

<a id="scroll.closestContentLayer"></a>
## scroll.closestContentLayer(originX, originY)

使图层靠近滚动组件，取决于定义的原点。原点定义在0和1之间，左上角为（0,0），中心（0.5，0.5），右下角（1,1）。
>Get the layer closest to the ScrollComponent, depending on the defined origin. The origin is defined as numbers between 0 and 1, where (0,0) is the top-left corner, (0.5, 0.5) the center, and (1,1) the bottom-right corner.

默认值为（0,0）， 这意味着它计算从滚动组件的左上角到内容图层左上角的距离。
>The default values are (0,0). This means that it calculates the distance from the top-left of the ScrollComponent to the top-left of the content layers.

```coffeescript
    scroll = new ScrollComponent

    # Create content layers 
    layerA = new Layer
        parent: scroll.content
        name: "layerA"
        x: 0
        y: 0

    layerB = new Layer
        parent: scroll.content
        name: "layerB"
        x: 50
        y: 50

    # Get the Layer of which the center point is closest 
    # to the center point of the ScrollComponent 
    print scroll.closestContentLayer(0.5, 0.5)
```

<a id="scroll.closestContentLayerForScrollPoint"></a>
## scroll.closestContentLayerForScrollPoint(originX, originY)

使内容图层达到特定点。
>Get the content layer closest to a specific point.

```coffeescript
     scroll = new ScrollComponent

     # Create content layers 
     layerA = new Layer
         parent: scroll.content
         name: "layerA"
         x: 0
         y: 0

     layerB = new Layer
         parent: scroll.content
         name: "layerB"
         x: 50
         y: 50

     # Get the layer of which the top-left 
     # corner is closest to x: 50, y: 25 
     print scroll.closestContentLayerForScrollPoint(
         x: 50
         y: 25
     )

     # Returns layerB 
```

你可以调整原点值来定义距离的计算方式。默认值为（0,0）,这意味着它计算从滚动组件的左上角到内容图层左上角的距离。
>You can adjust the origin values to define how the distance is calculated. The default values are (0,0). This means that it calculates the distance from the top-left of the ScrollComponent to the top-left of the content layers.

```coffeescript
     scroll = new ScrollComponent

     # Create content layers 
     layerA = new Layer
         parent: scroll.content
         name: "layerA"
         x: 0
         y: 0


     layerB = new Layer
         parent: scroll.content
         name: "layerB"
         x: 50
         y: 50

     # With the origins set to the center, 
     # layerA becomes the closest 
     print scroll.closestContentLayerForScrollPoint({ x: 50, y: 25 }, 0.5, 0.5)

     # Returns layerA 
```

<a id="scroll.scrollToPoint"></a>
## scroll.scrollToPoint(point, animate, animationOptions)

滚动到特定点，使用任意动画。
>Scroll to a specific point, optionally animating.

### Arguments

* **point** — 具有x和y属性值的对象
* **animate** — 布尔值，默认设置为true。（可选的）
* **animationOptions** — 具有曲线，时间，延迟和重复属性的对象。（可选的）

```coffeescript
     scroll = new ScrollComponent

     # Scroll content to x: 200, y: 100 
     scroll.scrollToPoint(
         x: 200, y: 100
         true
         curve: "ease"
     )

     # Scroll very slowly 
     scroll.scrollToPoint(
         x: 200, y: 100
         true
         curve: "ease", time: 10
     )
```

<a id="scroll.scrollToLayer"></a>
## scroll.scrollToLayer(layer, originX, originY, animate, animationOptions)

滚动到特定图层。你只能滚动到`scroll.content`中的子图层。
>Scroll to a specific layer. You can only scroll to layers that are children of the scroll.content layer.

### Arguments

* **layer** — 一个图层对象.
* **originX** — 0到1之间的数字（可选）
* **originY** — 0到1之间的数字（可选）
* **animate** — 布尔值，默认设置为true。（可选的）
* **animationOptions** — 具有曲线，时间，延迟和重复属性的对象。（可选的）

```coffeescript
     # Create ScrollComponent 
     scroll = new ScrollComponent
         width: 500
         height: 500

     # Define Background 
     layerA = new Layer
         x: 500
         y: 1000
         image: "bg.png"
         parent: scroll.content

     # Scroll to this layer 
     scrollerA = new Layer
         parent: scroll.content

     scroll.scrollToLayer(scrollerA)
```

`originX`和`originY`参数定义要滚动到的图层内的点。左上角默认值为（0,0）。
>The originX and originY arguments define the point within the layer that will be scrolled to. The default values are 0,0 - which is the top-left corner.

```coffeescript
scroll.scrollToLayer(
    layerA
    0.5, 0
    true
    time: 2
)
```

<a id="scroll.scrollToClosestLayer"></a>
## scroll.scrollToClosestLayer(originX, originY)

使用已给的原点,滚动页面到到最近的内容图层。默认值为：左上角（0,0），中心（0.5,0.5），右下角（1,1）。
>Scroll to the closest content layer, using the given origin. The default values are (0,0) which is the top-left corner, (0.5, 0.5) the center, and (1,1) the bottom-right corner.

### Arguments

* **originX** — 0到1之间的数字。
* **originY** — 0到1之间的数字。

```coffeescript
     scroll = new ScrollComponent

     layerA = new Layer
         parent: scroll.content
         x: 75
         y: 75

     # Scroll to the center of layerA 
     scroll.scrollToClosestLayer(0.5, 0.5)
```

<a id="scroll.mouseWheelEnabled"></a>
## scroll.mouseWheelEnabled(布尔值)

启用或禁用鼠标滚轮，默认禁用。启用时，可以通过拖动和使用鼠标滚动图层。
>Enable or disable scrolling with mousewheel. Disabled by default. When set to true, layers can be scrolled both by dragging and with the mouse.

```coffeescript
     scroll = new ScrollComponent
         width: 100
         height: 100

     # Allow scrolling with mouse 
     scroll.mouseWheelEnabled = true

     layerA = new Layer
         parent: scroll.content
         image: "images/bg.png"
         width: 100
         height: 200
```
<a id="scroll.wrap"></a>
## scroll.wrap(layer)

在新的滚动组件中包裹一个图层。在导入的图层中创建可滚动图层。
 >Wraps a layer within a new ScrollComponent. This is useful to create scrollable layers out of imported layers.

```coffeescript
     # Import files from Sketch 
     sketch = Framer.Importer.load "imported/Scrollable"

     # Wrap the "content" layer group 
     scroll = ScrollComponent.wrap(sketch.content)
```

现在，`scroll`是滚动组件的变量名，它会自动将图层包裹在滚动层中，你可以用它来调整某些属性，如动量，叠加或反弹。
>Now, scroll is the variable name of the ScrollComponent. This also automatically wraps your layer within a ScrollContent layer, which you can select to adjust certain properties like momentum, overdrag or bounce.

```coffeescript
     # Import files from Sketch 
     sketch = Framer.Importer.load "imported/Scrollable"

     # Wrap the "content" layer group 
     scroll = ScrollComponent.wrap(sketch.content)

     # Change scroll properties 
     scroll.scrollHorizontal = false
     scroll.speedY = 0.5

     # Change scroll.content properties 
     scroll.content.draggable.momentum = true
     scroll.content.draggable.overdrag = false
     scroll.content.draggable.bounce = false
```

<a id="scroll.updateContent"></a>
## scroll.updateContent()

重新计算并更新内容图层的大小和拖动约束，包括内边距。
>Re-calculates and updates the size of the content and the dragging constraints. It also accounts for the contentInset.

如果你想要更改内容图层的大小，可以调用它来相应地改变滚动组件的大小。
>If you're looking to change the size of your content layers, you can call it to update the size of your ScrollComponent accordingly.

```coffeescript
     scroll = new ScrollComponent

     # Update the contents of the ScrollComponent 
     scroll.updateContent()
```

<a id="scroll.copy"></a>
## scroll.copy()

复制一个滚动组建，包括其内容和属性。
>Copies a ScrollComponent, including its content and properties.

```coffeescript
     scroll = new ScrollComponent

     layerA = new Layer
         parent: scroll.content

     # Copy the ScrollComponent 
     scrollB = scroll.copy()
```

<a id="scroll.propagateEvents"></a>
## scroll.propagateEvents(布尔值)

设置可拖动内容图层的传播事件属性。默认设置为true。当使用嵌套的滚动组件或页面组件时，这非常有用。
>Set the propagateEvents property of the draggable content layer. Set to true by default. This is useful when working with nested ScrollComponents or PageComponents.

假设你想在滚动图层中有一个可拖动的图层。默认情况下，移动图层也会滚动图层，这是因为两个图层都会监听拖动事件。
>Let's say you'd like to have a draggable layer within the scroll.content layer. By default, moving the layer will also move the scroll.content. This is because both layers will listen to the dragging events.

为了避免将任何子级的拖动事件传递给父级，请禁用`propagateEvents`。这适用于所有嵌套的可拖动图层。
>To prevent any draggable children from passing events to its parent, set propagateEvents to false. This applies to all nested draggable layers.

```coffeescript
     scroll = new ScrollComponent
         width: Screen.width,
         height: Screen.height

     scroll.content.backgroundColor = "#28affa"

     layerA = new Layer
         parent: scroll.content,
         backgroundColor: "#fff"

     layerA.draggable.enabled = true

     # Setting propagateEvents to false allows you to drag layerA 
     # without also scrolling within the ScrollComponent 
     layerA.draggable.propagateEvents = false
```
