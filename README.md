# svgPathParser

Extremely powerful and extremely buggy library. It can save your day or make it a nightmare, depending on your needs.

The problem with SVG paths is that they are extremely hard to work with, since there are many commands
which are relative to the previous state of the path. This makes for a good compression but it is quite hard to programmatically modify the SVG path as it is.

This library has some functions to help with this matter,

- *parse* will parse the SVG path into a array of points
- *makePathAbsolute* will transform the relative parts of the path into absolute coordinates

The absolute coordinates means that commands in format 

  `c x1 y1 x2 y2 `

Where x1 y1 and x2 and y2 are relative coordinates to the current position are converted to format

  `C X0 Y1 X1 Y1 X2 Y2 `

Where all coordinates are absolute coordinates in the same coordinate system. After that you
can use commands like **transform path** to change the path structure arbitarily, for example

# examples

Examples of some functions are here:

http://jsfiddle.net/ygaheb1k/


# usage

```javascript
var parser = svgPathParser();
parser.parse( "M31.229,17.736c0.064-0.571,0.104-1.148,0.104-1.736s-0.04-1.166-0.104-1.737l-4.377-1.557c-0.218-0.716-0.504-1.401-0.851-2.05l1.993-4.192c-0.725-0.91-1.549-1.734-2.458-2.459l-4.193,1.994c-0.647-0.347-1.334-0.632-2.049-0.849l-1.558-4.378C17.165,0.708,16.588,0.667,16,0.667s-1.166,0.041-1.737,0.105L12.707,5.15c-0.716,0.217-1.401,0.502-2.05,0.849L6.464,4.005C5.554,4.73,4.73,5.554,4.005,6.464l1.994,4.192c-0.347,0.648-0.632,1.334-0.849,2.05l-4.378,1.557C0.708,14.834,0.667,15.412,0.667,16s0.041,1.165,0.105,1.736l4.378,1.558c0.217,0.715,0.502,1.401,0.849,2.049l-1.994,4.193c0.725,0.909,1.549,1.733,2.459,2.458l4.192-1.993c0.648,0.347,1.334,0.633,2.05,0.851l1.557,4.377c0.571,0.064,1.148,0.104,1.737,0.104c0.588,0,1.165-0.04,1.736-0.104l1.558-4.377c0.715-0.218,1.399-0.504,2.049-0.851l4.193,1.993c0.909-0.725,1.733-1.549,2.458-2.458l-1.993-4.193c0.347-0.647,0.633-1.334,0.851-2.049L31.229,17.736zM16,20.871c-2.69,0-4.872-2.182-4.872-4.871c0-2.69,2.182-4.872,4.872-4.872c2.689,0,4.871,2.182,4.871,4.872C20.871,18.689,18.689,20.871,16,20.871z" );

// change the path dimensions
parser.fitPathInto( 120, 120 );
parser.makePathAbsolute();

// get a new path out from the system
var newPathString = parser.svgString();


```
There are some useful commands

##drawPath( ctx, width, height )

This function will draw the SVG path into HTML5 canvas context.

##findDimensions

This function will return the position of the SVG path in array
```
 [minX, minY, maxX, maxY]
```
You can then use other functions to transform the path.

##fitPathInto( width, height )

Will make the path fit into dimensions width x height.

The path should be transformed to (0,0) coordinates.

##forCmds( function(cmd) {} ) 

This function will iterate through all SVG path commands

The callback will receive `cmd` which is Object of format:

```
{
  name : "M",
  points : [100,100]
}
```

##fromBezierArray

The package has also class `jsBezierCurve` which is ment for manipulating BezierCurves.

The class `jsBezierCurve` is still undocumented, but you can construct SVG path from BezierCurves too.

##makePathAbsolute

Will transform all commands at the current path to absolute presentation.

The absolute coordinates means that commands in format 

  `c x1 y1 x2 y2 `

Where x1 y1 and x2 and y2 are relative coordinates to the current position are converted to format

  `C X0 Y1 X1 Y1 X2 Y2 `

##parse

Will parse the SVG path into command objects. This function must be called before the class is used.

##replacePartWith

This function can be used to replace some part of the original path with some other path.
Extremely cool function, use with care.

```javascript
var fillStr = "M 23 236 C 210 156 271 90 187 22  C 306 15 333 18 414 212 ";

for( var i=0; i<10; i++)
    parser.replacePartWith(i, fillStr, false );
```

##svgString

Returns the SVG Path representation which can be used in SVG element like

  `<path d="put_the_path_here"></path>`

##toBezierArray

Returns list of Bezier objects representing the path. Lines and Quadratic paths are converted to Cubic paths.

##toQuaternionPath

Returns the path as list of quaternions.

##transformPoints( function( point) {  })

Before using this function transform the points to absolute coordinates.

example: reverse points around line `x=60`

```javascript
parser.transformPoints( function(p) {
    p.x = 60 + -1*(p.x-60);
})
```