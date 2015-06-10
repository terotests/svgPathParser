# svgPathParser

Extremely powerful and extremely buggy library. It can save your day or make it a nightmare, depending on your needs.

The problem with SVG paths is that they are extremely hard to work with, since there are many commands
which are relative to the previous state of the path. This makes for a good compression but it is quite hard to programmatically modify the SVG path as it is.

This library has some functions to help with this matter,

- *parse* will parse the SVG path into a array of points
- *makePathAbsolute* will transform the relative parts of the path into absolute coordinates

The absoulte coordinates means that commands in format 

  `c x1 y1 x2 y2 `

Where x1 y1 and x2 and y2 are relative coordinates to the current position are converted to format

  `C X0 Y1 X1 Y1 X2 Y2 `

Where all coordinates are absolute coordinates in the same coordinate system. After that you
can use commands like **transform path** to change the path structure arbitarily, for example

There are some useful commands

##drawPath( ctx, width, height )

This function will draw the SVG path into HTML5 canvas context.

##findDimensions

This function will return the position of the SVG path in array
´´´
 [minX, minY, maxX, maxY]
´´´
You can then use other functions to transform the path.

##fitPathInto( width, height )

Will make the path fit into dimensions width x height.

The path should be transformed to (0,0) coordinates.

##forCmds( function(cmd) {} ) 

This function will iterate through all SVG path commands

The command structure is

```
{
  name : "M",
  points : [100,100]
}
```



##fromBezierArray
##getCommands
#makePathAbsolute
##parse
##replacePartWith
##svgString
##toBezierArray
##toQuaternionPath

##transformPoints( function( point) {  })

Before using this function transform the points to absolute coordinates.

example: reverse points around line `x=60`

```javascript
parser.transformPoints( function(p) {
    p.x = 60 + -1*(p.x-60);
})
```