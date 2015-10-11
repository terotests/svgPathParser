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

# Known bugs

There are few known bugs in the library

- The Arc element `a` or `A` are not currently supported
- does not understand "default" command 'line' in very simple paths like `M25.979,12.896,5.979,12.896,5.979,19.562,25.979,19.562z`


# Examples

Examples of some functions are here:

http://jsfiddle.net/vjyhxznL/2/


# Usage

```javascript
var parser = svgPathParser();
parser.parse( "M31.229,17.736c0.064-0.571,0.104-1.148,0.104-1.736s-0.04-1.166-0.104-1.737l-4.377-1.557c-0.218-0.716-0.504-1.401-0.851-2.05l1.993-4.192c-0.725-0.91-1.549-1.734-2.458-2.459l-4.193,1.994c-0.647-0.347-1.334-0.632-2.049-0.849l-1.558-4.378C17.165,0.708,16.588,0.667,16,0.667s-1.166,0.041-1.737,0.105L12.707,5.15c-0.716,0.217-1.401,0.502-2.05,0.849L6.464,4.005C5.554,4.73,4.73,5.554,4.005,6.464l1.994,4.192c-0.347,0.648-0.632,1.334-0.849,2.05l-4.378,1.557C0.708,14.834,0.667,15.412,0.667,16s0.041,1.165,0.105,1.736l4.378,1.558c0.217,0.715,0.502,1.401,0.849,2.049l-1.994,4.193c0.725,0.909,1.549,1.733,2.459,2.458l4.192-1.993c0.648,0.347,1.334,0.633,2.05,0.851l1.557,4.377c0.571,0.064,1.148,0.104,1.737,0.104c0.588,0,1.165-0.04,1.736-0.104l1.558-4.377c0.715-0.218,1.399-0.504,2.049-0.851l4.193,1.993c0.909-0.725,1.733-1.549,2.458-2.458l-1.993-4.193c0.347-0.647,0.633-1.334,0.851-2.049L31.229,17.736zM16,20.871c-2.69,0-4.872-2.182-4.872-4.871c0-2.69,2.182-4.872,4.872-4.872c2.689,0,4.871,2.182,4.871,4.872C20.871,18.689,18.689,20.871,16,20.871z" );

// change the path dimensions
parser.makePathAbsolute();
parser.fitPathInto( 120, 120 );

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

# License

MIT. Or whatever license fits your needs.


















   

 


   
#### Class svgPathParser


- [drawPath](README.md#svgPathParser_drawPath)
- [findDimensions](README.md#svgPathParser_findDimensions)
- [fitPathInto](README.md#svgPathParser_fitPathInto)
- [flowerCurve](README.md#svgPathParser_flowerCurve)
- [forCmds](README.md#svgPathParser_forCmds)
- [fromBezierArray](README.md#svgPathParser_fromBezierArray)
- [getCommands](README.md#svgPathParser_getCommands)
- [getPath](README.md#svgPathParser_getPath)
- [getSegmentCount](README.md#svgPathParser_getSegmentCount)
- [getSubPaths](README.md#svgPathParser_getSubPaths)
- [initCmd](README.md#svgPathParser_initCmd)
- [inverse](README.md#svgPathParser_inverse)
- [makePathAbsolute](README.md#svgPathParser_makePathAbsolute)
- [n](README.md#svgPathParser_n)
- [normalize](README.md#svgPathParser_normalize)
- [originals](README.md#svgPathParser_originals)
- [parse](README.md#svgPathParser_parse)
- [path](README.md#svgPathParser_path)
- [pathFunction](README.md#svgPathParser_pathFunction)
- [popCommand](README.md#svgPathParser_popCommand)
- [relativePosition](README.md#svgPathParser_relativePosition)
- [replacePartWith](README.md#svgPathParser_replacePartWith)
- [saveToOriginals](README.md#svgPathParser_saveToOriginals)
- [scaleFactor](README.md#svgPathParser_scaleFactor)
- [svgString](README.md#svgPathParser_svgString)
- [toBezierArray](README.md#svgPathParser_toBezierArray)
- [toQuaternionPath](README.md#svgPathParser_toQuaternionPath)
- [transformPoints](README.md#svgPathParser_transformPoints)



   
    
    
    
    
    
    
    
    


   
      
            
#### Class jsVectors


- [add](README.md#jsVectors_add)
- [angleBetween](README.md#jsVectors_angleBetween)
- [calc_cat](README.md#jsVectors_calc_cat)
- [crossProd](README.md#jsVectors_crossProd)
- [diff](README.md#jsVectors_diff)
- [dist](README.md#jsVectors_dist)
- [dotProd](README.md#jsVectors_dotProd)
- [getBarCoeffs](README.md#jsVectors_getBarCoeffs)
- [initProjection](README.md#jsVectors_initProjection)
- [length](README.md#jsVectors_length)
- [linesIntersect](README.md#jsVectors_linesIntersect)
- [mirrorVector](README.md#jsVectors_mirrorVector)
- [normalize](README.md#jsVectors_normalize)
- [opposeVector](README.md#jsVectors_opposeVector)
- [pointInTriangle](README.md#jsVectors_pointInTriangle)
- [pointInTriangleBc](README.md#jsVectors_pointInTriangleBc)
- [project](README.md#jsVectors_project)
- [rotate](README.md#jsVectors_rotate)
- [rotateAround](README.md#jsVectors_rotateAround)
- [sub](README.md#jsVectors_sub)
- [tangentNormal](README.md#jsVectors_tangentNormal)
- [triangleArea](README.md#jsVectors_triangleArea)
- [triangleInTriangle](README.md#jsVectors_triangleInTriangle)
- [unProject](README.md#jsVectors_unProject)



   


   



      
    
      
            
#### Class quaternion


- [copy](README.md#quaternion_copy)
- [inverse](README.md#quaternion_inverse)
- [multiply](README.md#quaternion_multiply)
- [normalizeVector3D](README.md#quaternion_normalizeVector3D)
- [projectVector](README.md#quaternion_projectVector)
- [rotate](README.md#quaternion_rotate)
- [setFromAxisRotation](README.md#quaternion_setFromAxisRotation)



   
    
    


   
      
            
#### Class jsVectors


- [add](README.md#jsVectors_add)
- [angleBetween](README.md#jsVectors_angleBetween)
- [calc_cat](README.md#jsVectors_calc_cat)
- [crossProd](README.md#jsVectors_crossProd)
- [diff](README.md#jsVectors_diff)
- [dist](README.md#jsVectors_dist)
- [dotProd](README.md#jsVectors_dotProd)
- [getBarCoeffs](README.md#jsVectors_getBarCoeffs)
- [initProjection](README.md#jsVectors_initProjection)
- [length](README.md#jsVectors_length)
- [linesIntersect](README.md#jsVectors_linesIntersect)
- [mirrorVector](README.md#jsVectors_mirrorVector)
- [normalize](README.md#jsVectors_normalize)
- [opposeVector](README.md#jsVectors_opposeVector)
- [pointInTriangle](README.md#jsVectors_pointInTriangle)
- [pointInTriangleBc](README.md#jsVectors_pointInTriangleBc)
- [project](README.md#jsVectors_project)
- [rotate](README.md#jsVectors_rotate)
- [rotateAround](README.md#jsVectors_rotateAround)
- [sub](README.md#jsVectors_sub)
- [tangentNormal](README.md#jsVectors_tangentNormal)
- [triangleArea](README.md#jsVectors_triangleArea)
- [triangleInTriangle](README.md#jsVectors_triangleInTriangle)
- [unProject](README.md#jsVectors_unProject)



   


   



      
    



      
    
      
            
#### Class jsBezierCurve


- [derivate](README.md#jsBezierCurve_derivate)
- [distanceOf](README.md#jsBezierCurve_distanceOf)
- [findClosestT](README.md#jsBezierCurve_findClosestT)
- [fitListTo](README.md#jsBezierCurve_fitListTo)
- [fromLine](README.md#jsBezierCurve_fromLine)
- [fromPoints](README.md#jsBezierCurve_fromPoints)
- [fromQuadCurve](README.md#jsBezierCurve_fromQuadCurve)
- [initCoeffs](README.md#jsBezierCurve_initCoeffs)
- [inverseProject](README.md#jsBezierCurve_inverseProject)
- [mirrorControls](README.md#jsBezierCurve_mirrorControls)
- [normal](README.md#jsBezierCurve_normal)
- [point_x](README.md#jsBezierCurve_point_x)
- [point_y](README.md#jsBezierCurve_point_y)
- [points](README.md#jsBezierCurve_points)
- [projectPoint](README.md#jsBezierCurve_projectPoint)
- [setControls](README.md#jsBezierCurve_setControls)
- [split](README.md#jsBezierCurve_split)
- [splitCoeff](README.md#jsBezierCurve_splitCoeff)
- [step](README.md#jsBezierCurve_step)
- [tangent](README.md#jsBezierCurve_tangent)
- [x](README.md#jsBezierCurve_x)
- [y](README.md#jsBezierCurve_y)
- [z](README.md#jsBezierCurve_z)



   


   



      
    
      
            
#### Class pathIterator


- [bezierSplit](README.md#pathIterator_bezierSplit)
- [endPoint](README.md#pathIterator_endPoint)
- [partToSvgPath](README.md#pathIterator_partToSvgPath)
- [pathFunction](README.md#pathIterator_pathFunction)
- [quadToCubic](README.md#pathIterator_quadToCubic)
- [toSvgCubicPath](README.md#pathIterator_toSvgCubicPath)
- [toSvgPath](README.md#pathIterator_toSvgPath)



   
    
    


   
      
            
#### Class jsVectors


- [add](README.md#jsVectors_add)
- [angleBetween](README.md#jsVectors_angleBetween)
- [calc_cat](README.md#jsVectors_calc_cat)
- [crossProd](README.md#jsVectors_crossProd)
- [diff](README.md#jsVectors_diff)
- [dist](README.md#jsVectors_dist)
- [dotProd](README.md#jsVectors_dotProd)
- [getBarCoeffs](README.md#jsVectors_getBarCoeffs)
- [initProjection](README.md#jsVectors_initProjection)
- [length](README.md#jsVectors_length)
- [linesIntersect](README.md#jsVectors_linesIntersect)
- [mirrorVector](README.md#jsVectors_mirrorVector)
- [normalize](README.md#jsVectors_normalize)
- [opposeVector](README.md#jsVectors_opposeVector)
- [pointInTriangle](README.md#jsVectors_pointInTriangle)
- [pointInTriangleBc](README.md#jsVectors_pointInTriangleBc)
- [project](README.md#jsVectors_project)
- [rotate](README.md#jsVectors_rotate)
- [rotateAround](README.md#jsVectors_rotateAround)
- [sub](README.md#jsVectors_sub)
- [tangentNormal](README.md#jsVectors_tangentNormal)
- [triangleArea](README.md#jsVectors_triangleArea)
- [triangleInTriangle](README.md#jsVectors_triangleInTriangle)
- [unProject](README.md#jsVectors_unProject)



   


   



      
    



      
    





   
# Class svgPathParser


The class has following internal singleton variables:
        
* _parsedData
        
        
### <a name="svgPathParser_drawPath"></a>svgPathParser::drawPath(ctx, w, h)


```javascript
var _firstX, _firstY, x, y;
ctx.beginPath();
this._all.forEach(function(cmd) {
   
   if(cmd.name =="M") {
       x = cmd.points[0];
       y = cmd.points[1];
       ctx.moveTo( x,y );
   }
   
   if(cmd.name =="m") {
       x = x + cmd.points[0];
       y = y + cmd.points[1];
       ctx.moveTo( x,y );
   }        
   
   if(cmd.name=="q") {
       for(var s=0; s<cmd.points.length;s+=4) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];
           //x=x0; y=y0;
           var x1 = x + p[s+2],
               y1 = y + p[s+3];
           x=x1; y=y1;
           ctx.quadraticCurveTo( x0,y0,x1,y1,x2,y2 );
       }
   }
   
   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="Q") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=4) {
           ctx.quadraticCurveTo( p[s+0],p[s+1],p[s+2],p[s+3]);
       }
   }
   
   if(cmd.name=="c") {
       for(var s=0; s<cmd.points.length;s+=6) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];
           //x=x0; y=y0;
           var x1 = x + p[s+2],
               y1 = y + p[s+3];
           // x=x1; y=y1;
          var x2 = x + p[s+4],
               y2 = y + p[s+5];
           x=x2; y=y2;
           ctx.bezierCurveTo( x0,y0,x1,y1,x2,y2 );
       }
   }
   
   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="C") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=6) {
           ctx.bezierCurveTo( p[s+0],p[s+1],p[s+2],p[s+3],p[s+4],p[s+5] );
       }
   }           
   if(cmd.name=="l") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];  
           x=x0; y=y0;
           ctx.lineTo( x0,y0 );
       }
   }
   
   if(cmd.name=="H") {
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var x0 = p[s+0];  
           x=x0; 
           ctx.lineTo( x0, y );
       }
   }    
   
   if(cmd.name=="V") {
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var y0 = p[s+0];  
           y=y0; 
           ctx.lineTo( x, y0 );
       }
   }
   

   if(cmd.name=="L") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = p[s+0],
               y0 = p[s+1];  
           x=x0; y=y0;
           ctx.lineTo( x0,y0 );
       }
   }           
   
   if(cmd.name=="z") {
       ctx.closePath();
   }
})
     
   
```

### <a name="svgPathParser_findDimensions"></a>svgPathParser::findDimensions()


```javascript

if(this._limits) return this._limits;

var _firstX, _firstY;
var _minX, _minY, _maxX, _maxY, x,y;

var limits = function(x,y) {

    if(typeof(_minX) == "undefined") {
       _minX = x;
       _maxX = x;
       _minY = y;
       _maxY = y;
    }
    _minX = Math.min(_minX, x);
    _minY = Math.min(_minY, y);
    _maxX = Math.max(_maxX, x);
    _maxY = Math.max(_maxY, y);            

}

this._all.forEach(function(cmd) {

    if(cmd.name =="M") {
       
       x = cmd.points[0];
       y = cmd.points[1];
       
       limits(x,y);
             
    }
    
    if(cmd.name =="m") {
       
       x = x + cmd.points[0];
       y = y + cmd.points[1];
       limits(x,y);
       
    }   
    
    if(cmd.name=="c") {
       for(var s=0; s<cmd.points.length;s+=6) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];
           //x=x0; y=y0;
           var x1 = x + p[s+2],
               y1 = y + p[s+3];
           // x=x1; y=y1;
          var x2 = x + p[s+4],
               y2 = y + p[s+5];
               
           limits(x0,y0);
           limits(x1,y1);
           limits(x2,y2);
           x=x2; y=y2;
           
       }
    }
    
    if(cmd.name=="C") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=6) {
           limits(p[s+0],p[s+1]);
           limits(p[s+2],p[s+3]);
           limits(p[s+4],p[s+5]);
       }
    }           
    if(cmd.name=="l") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];  
           x=x0; y=y0;
           limits(x,y);
       }
    }
    
    if(cmd.name=="L") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = p[s+0],
               y0 = p[s+1];  
           x=x0; y=y0;
           limits(x,y);
       }
    }           
});

// NOTE: in these SVG photos created by the potrace the y-axis
// is reversed, so the maxY is actually the minY 
this._limits = [_minX, _minY, _maxX, _maxY];
return this._limits;

```

### <a name="svgPathParser_fitPathInto"></a>svgPathParser::fitPathInto(w, h)


```javascript

var dim = this.findDimensions();

var allIn = true;
for(var i=0; i<4; i++) {
   if(dim[i]<0 || dim[i]>w) allIn = false;
}

var drawW = Math.abs( dim[2] - dim[0] ),
    drawH = Math.abs( dim[3] - dim[1] );
   
var flipY = false;

if(Math.abs( dim[3]) < Math.abs( dim[1]) ) {
   flipY = true;
}
   
var scale1 = w / drawW,
   scale2 = h / drawH,
   transX = -dim[0],
   transY = -dim[1];

var scaleX = Math.min(scale1, scale2),
   scaleY = scaleX;
   

if(flipY) {
   scaleY = -scaleY;
   transY = -dim[3]; // for example if -100 => +100
}

var tx = function(x) {
   return (x + transX)*scaleX;
}
var ty = function(y) {
   return (y + transY)*scaleY;
}

this._all.forEach(function(cmd) {
   
   if(cmd.name =="M") {
       
       cmd.points[0] = tx( cmd.points[0] );
       cmd.points[1] = ty( cmd.points[1] );
   }
   if(cmd.name =="m") {
       cmd.points[0] *= scaleX;
       cmd.points[1] *= scaleY;
       
   }        

   if(cmd.name =="L") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           p[s+0] = tx(p[s+0]); 
           p[s+1] = ty(p[s+1]);
       }
   }
   
   if(cmd.name=="c") {
       for(var s=0; s<cmd.points.length;s+=6) {
           var p = cmd.points;
           p[s+0] *= scaleX;
           p[s+2] *= scaleX;
           p[s+4] *= scaleX;
           p[s+1] *= scaleY;
           p[s+3] *= scaleY;
           p[s+5] *= scaleY;                   
       }
   }
   
   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="C") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=6) {
           p[s+0] = tx(p[s+0]); 
           p[s+2] = tx(p[s+2]); 
           p[s+4] = tx(p[s+4]); 
           p[s+1] = ty(p[s+1]); 
           p[s+3] = ty(p[s+3]); 
           p[s+5] = ty(p[s+5]); 
       }
   }      
   
   if(cmd.name=="Q") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=4) {
           p[s+0] = tx(p[s+0]); 
           p[s+2] = tx(p[s+2]); 
           p[s+1] = ty(p[s+1]); 
           p[s+3] = ty(p[s+3]); 
       }
   }            
   
   if(cmd.name=="l") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           p[s+0] *= scaleX;
           p[s+1] *= scaleY;    
       }
   }
   
  
});

this._limits = null;


```

### <a name="svgPathParser_flowerCurve"></a>svgPathParser::flowerCurve(svgPath, options)


```javascript

/*
options = {
    leafCount : 5,
    origo : { x : 0, y : 0},
    beziers : []
}
*/

options = options || {};

var leafCount = options.leafCount || 5;

var curve,i=0,bFirst=true;

var m = [
    { x: 0, y : 0},
    { x: 0, y : 0},
    { x: 0, y : 0},
    { x: 0, y : 0}
];

var rotateStep = 360 / leafCount,
rotateIndex = 0;

// could be this of course
var parser = svgPathParser();
parser.parse(svgPath);
parser.makePathAbsolute();

var curves = parser.toBezierArray();

console.log(curves);

var firstCurve = curves[0];

if(!firstCurve) return;

var base_x = firstCurve.point_x(0),
    base_y = firstCurve.point_y(0);

var ctx = canvasContext();
ctx.beginPath();
var chCnt = curves.length;


for(;rotateIndex<leafCount; rotateIndex++) {
    
    var angle = rotateIndex * rotateStep;
    
    // path.rotateContext( base_x, base_y, rotateStep, ctx );
    ctx.translate(base_x,base_y);
    ctx.rotate( rotateStep*Math.PI/180 );  // rotate 90 degrees
    ctx.translate(-base_x, -base_y);

    i=0,bFirst=true
    
    var along = { x: 0, y: 0};
    var base = { x: 0, y: 0},
        p;
    while( curve = curves[i++] ) {
        p = curve.points();
        if(!p[1]) break;
        if(bFirst) {
            ctx.moveTo(p[0].x, p[0].y);
            base.x = p[0].x;
            base.y = p[0].y;
        }
        ctx.bezierCurveTo(p[1].x, p[1].y,
                         p[2].x, p[2].y,
                         p[3].x, p[3].y);
        
        //console.log("=== render path mirrored, bezier ");
        //console.log(p);
        if(i==chCnt) break;
        bFirst = false;
    } 
    
    along.x = p[3].x;
    along.y = p[3].y;
        
    var jsMath = jsVectors();
    
    i=i-1;             
    while( curve = curves[i--] ) {

        var p = curve.points();
        
        m[0].x = p[0].x;
        m[0].y = p[0].y;
        m[1].x = p[1].x;
        m[1].y = p[1].y;
        m[2].x = p[2].x;
        m[2].y = p[2].y;
        jsMath.mirrorVector( m[0], along, base );
        jsMath.mirrorVector( m[1], along, base );
        jsMath.mirrorVector( m[2], along, base );
        
        ctx.bezierCurveTo(m[2].x, m[2].y,
                     m[1].x, m[1].y,
                     m[0].x, m[0].y);                 
        
        if(i<0) break;
        bFirst = false;
    }                          

} 


return ctx.svgPathString();
```

### <a name="svgPathParser_forCmds"></a>svgPathParser::forCmds(fn)


```javascript
this._all.forEach(fn);
```

### <a name="svgPathParser_fromBezierArray"></a>svgPathParser::fromBezierArray(list)


```javascript
var x,y,i,plen = list.length;
var target = this._all;
this._all = [];

for(var i=0; i<plen;i++) {
   
   var bez = list[i]; 
   if(i==0) {
       var c = {
           name : "M",
           points : [
            bez.point_x(0), bez.point_y(0) 
           ]
       };
       this._all.push(c);               
   }
   var c = {
       name : "C",
       points : [
        bez.point_x(1), bez.point_y(1), 
        bez.point_x(2), bez.point_y(2), 
        bez.point_x(3), bez.point_y(3)
       ]
   };
   this._all.push(c);
}
this.saveToOriginals();
          
```

### <a name="svgPathParser_getCommands"></a>svgPathParser::getCommands(t)


```javascript
return this._all;
```

### <a name="svgPathParser_getPath"></a>svgPathParser::getPath(i)


```javascript

return this._all[i];
```

### <a name="svgPathParser_getSegmentCount"></a>svgPathParser::getSegmentCount(t)


```javascript

var last = this._all.length;
if( this._all[last-1].name == "z" ) last--;

return last;
```

### <a name="svgPathParser_getSubPaths"></a>svgPathParser::getSubPaths(t)


```javascript
return this._subPaths;
```

### svgPathParser::constructor( w, h, intoDom )

```javascript
this._activeCmd = null;
this._all = [];
this._stringLeft = "";

this._original = null;

this._x = 0;
this._y = 0;

if(!_parsedData) {
    _parsedData = {};
}
```
        
### <a name="svgPathParser_initCmd"></a>svgPathParser::initCmd(n)


```javascript
this._activeCmd = {
   name : n,
   points : []
};
this._all.push(this._activeCmd);
return this._activeCmd;
   
```

### <a name="svgPathParser_inverse"></a>svgPathParser::inverse(t)


```javascript
var all = this.originals();

var point = { x: 0, y:0 };

var x,y,i,plen = all.length;

this._all.reverse();

var target = this._all;
var all = this._all;

var newCmds = [];

var getPrevPoints = function(currCmd, prevCmd) {
      var res = [];
      var n = (currCmd.points.length/2),
          i = currCmd.points.length-4;
      while(n>0) {
          if(n==1) {
            if(!prevCmd) return res;
            i = prevCmd.points.length - 2;
            res.push(prevCmd.points[i]);
            res.push(prevCmd.points[i+1]);
          } else {
            res.push(currCmd.points[i]);
            res.push(currCmd.points[i+1]);  
            i-=2;
          }
          n--;
      }
    return res;
};

if(all[0].name=="z") {
    all.shift();
    // plen--;
}

for(var i=0; i<plen;i++) {
   
   var cmd = all[i],
       tCmd = all[i],
       nextCmd = all[i+1],
       prevCmd;
       
   if(!cmd) break;
   if(i>0) prevCmd = all[i-1];
   
   if(i==0) {
        var ii = cmd.points.length-2;
        var cc = { name : "M", points : [
                cmd.points[ii], cmd.points[ii+1]
            ] };
        newCmds.push(cc);
   } else {
        var cc = { name : prevCmd.name, points : getPrevPoints(prevCmd, cmd) };   
        newCmds.push(cc);
   }
}

var cc = { name : "z", points : [] };
newCmds.push(cc);

// console.log(newCmds);

this._all = newCmds;
```

### <a name="svgPathParser_makePathAbsolute"></a>svgPathParser::makePathAbsolute()


```javascript


var _firstX, _firstY;
var x,y,
    lastBx, lastBy,
    bNoBx = true;
    
var firstSmoothPoint = function() {
    if(bNoBx) {
        lastBx = x;
        lastBy = y;
    }
    var dx = x - lastBx,
        dy = y - lastBy;
    return {
        x : x + dx,
        y : y + dy
    };
}
this._all.forEach(function(cmd) {

   if(cmd.name =="M") {
       x = cmd.points[0];
       y = cmd.points[1];
       bNoBx = true;
   }
   
   if(cmd.name =="L") {
       x = cmd.points[0];
       y = cmd.points[1];
       bNoBx = true;
   }   
   
   if(cmd.name =="m") {
       
       x = x + cmd.points[0];
       y = y + cmd.points[1];
       
       cmd.points[0] = x;
       cmd.points[1] = y;
       cmd.name = "M";
       bNoBx = true;
   }          
   
   if(cmd.name=="q") {
       for(var s=0; s<cmd.points.length;s+=4) {
           var p = cmd.points;
           
           p[s+0] = x + p[s+0];
           p[s+1] = y + p[s+1];
           p[s+2] = x + p[s+2];
           p[s+3] = y + p[s+3];
           x = p[s+2];
           y = p[s+3];
           cmd.name = "Q";
       }
       bNoBx = true;
   }   
   if(cmd.name=="C") {
       var p = cmd.points;
       lastBx = p[2];
       lastBy = p[3];   
       
       x = p[4];
       y = p[5];      
       bNoBx = false;
   }
   if(cmd.name=="c") {
       for(var s=0; s<cmd.points.length;s+=6) {
           var p = cmd.points;
           
           p[s+0] = x + p[s+0];
           p[s+1] = y + p[s+1];
           p[s+2] = x + p[s+2];
           p[s+3] = y + p[s+3];
           p[s+4] = x + p[s+4];
           p[s+5] = y + p[s+5];
           x = p[s+4];
           y = p[s+5];
           lastBx = p[s+2];
           lastBy = p[s+3];
           cmd.name = "C";
       }
       bNoBx = false;
   }
   
   if(cmd.name=="S") {
       var p = cmd.points;
       var first = firstSmoothPoint();
       var newPoints = [];
       newPoints[0] = first.x;
       newPoints[1] = first.y;
       newPoints[2] = p[0];
       newPoints[3] = p[1];
       newPoints[4] = p[2];
       newPoints[5] = p[3];
       x = newPoints[4];
       y = newPoints[5];
       lastBx = newPoints[2];
       lastBy = newPoints[3];     
       cmd.name = "C";
       cmd.points = newPoints;
       bNoBx = false;
   }
   if(cmd.name=="s") {
       var p = cmd.points;
       var first = firstSmoothPoint();
       var newPoints = [];
       newPoints[0] = first.x;
       newPoints[1] = first.y;
       newPoints[2] = x+p[0];
       newPoints[3] = y+p[1];
       newPoints[4] = x+p[2];
       newPoints[5] = y+p[3];
       x = newPoints[4];
       y = newPoints[5];
       lastBx = newPoints[2];
       lastBy = newPoints[3];     
       cmd.name = "C";
       cmd.points = newPoints;
       bNoBx = false;
   }   
   
   if(cmd.name=="h") {
       bNoBx = true;
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var x0 = x + p[s+0];  
           x=x0;
           p[s+0] = x0;
           cmd.points = [x0,y];
           cmd.name = "L";
           return;
       }
   }    
   
   if(cmd.name=="H") {
       bNoBx = true;
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var x0 = p[s+0];  
           x=x0;
           p[s+0] = x0;
           cmd.points = [x0,y];
           cmd.name = "L";
           return;
       }
   }    
   
   if(cmd.name=="V") {
       bNoBx = true;
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           //console.log("--- V ----");
           //console.log("Point cnt ", cmd.points.length);
           //console.log(p, "y : ",y, " delta :  ",p[s+0]);
           var y0 = p[s+0];  
           y=y0;
           //console.log("After add : ",y, "and y0 = ", y0);
           cmd.points = [x,y0];
           cmd.name = "L";
           //console.log(cmd);
           return;
       }
   }
   
    if(cmd.name=="v") {
       bNoBx = true;
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var y0 = y + p[s+0];  
           y=y0;
           cmd.points = [x,y0];
           cmd.name = "L";
           return;
       }
   }   
   
  
 
   if(cmd.name=="l") {
       bNoBx = true;
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];  
           x=x0; y=y0;
           p[s+0] = x0;
           p[s+1] = y0;
           cmd.name = "L";
       }
   }
})


```

### <a name="svgPathParser_n"></a>svgPathParser::n(n)


```javascript
return n.toFixed(5);
```

### <a name="svgPathParser_normalize"></a>svgPathParser::normalize(width, height)


```javascript
if(!width) width = 800;
if(!height) height = 800;
this.makePathAbsolute();
this.fitPathInto(width,height);
   
```

### <a name="svgPathParser_originals"></a>svgPathParser::originals()


```javascript

if(!this._original) {
   this._original = JSON.parse( JSON.stringify( this._all ) );
}
return this._original;
   
```

### <a name="svgPathParser_parse"></a>svgPathParser::parse(str)


```javascript
/*var old;
if(old = _parsedData[str]) {
    this._all = JSON.parse( old );
    return;
}*/

this._activeCmd = null;
this._all = [];
this._stringLeft = "";

this._original = null;

this._x = 0;
this._y = 0;
  
this._usedCommands = {};
if(!str) str = "M25.979,12.896 L 5.979,12.896,5.979,19.562,25.979,19.562z";
var c,
   leftString = str;
var lastLen = 0;
var maxCnt = 10000;


this._subPaths = str.split("M");
//console.log("Sub paths");
//console.log(this._subPaths);

this._subIndex = 0;

while(leftString = this.popCommand(leftString)) {
   if(leftString.length==0) break;
   if(leftString.length==lastLen) break;
   
   if(maxCnt-- < 0 ) break;
   
   lastLen = leftString.length;
}

// _parsedData[str] = JSON.stringify( this._all );

// console.log("Used commands", this._usedCommands);
return this._all;
   
```

### <a name="svgPathParser_path"></a>svgPathParser::path()


```javascript

return this._all;
   
```

### <a name="svgPathParser_pathFunction"></a>svgPathParser::pathFunction(t)


```javascript
/*
this.initBezier();
var ntCnt = this.getSegmentCount();
var t1 = ntCnt * t;
var t_index = Math.floor( t1 );
var seg = this.getSegmentNro(t_index);
var sub_t = t1 - t_index;

// for example ntCnt = 10
// t = 9,5
var stepLen = 1 / ntCnt,        // 0,1
    nowStep = t_index / ntCnt,  // 0,9
    totStep = t,                // 0,95
    remStep = totStep - nowStep, // 0,05
    relStep = remStep / stepLen; // 0,05 / 0,1 = 0,5

var bez = seg.bezier();
// console.log("Rel step "+relStep);
pathFnData.x = bez.x(relStep);
pathFnData.y = bez.y(relStep);
var nn = bez.tangent(relStep, true);

pathFnData.normal.x = nn.x;
pathFnData.normal.y = nn.y;

fn(pathFnData);
*/
```

### <a name="svgPathParser_popCommand"></a>svgPathParser::popCommand(str)


```javascript


//console.log("popCommand");
//console.log(str);

str = str.trim();

var cmdStr = str.charAt(0),
   cmd = null;

if(cmdStr=="M") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}

if(cmdStr=="m") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}  

if(cmdStr=="Q") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}       

if(cmdStr=="q") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}       

if(cmdStr=="S") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}       

if(cmdStr=="s") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}       

if(cmdStr=="C") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}       

if(cmdStr=="c") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}

if(cmdStr=="H") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}         

if(cmdStr=="h") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}         

if(cmdStr=="V") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}         

if(cmdStr=="v") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}         

if(cmdStr=="L") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}         

if(cmdStr=="l") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}      

if(cmdStr=="Z") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}          

if(cmdStr=="z") {
   cmd = this.initCmd(cmdStr);
   str = str.substring(1);
}       

// Find the points....
if(cmd) {
   
   this._usedCommands[cmdStr] = "true";
   str = str.trim();
   
   var ok = true;
   
   while(ok && str.length>0) {
       
       var firstChar = str.charAt(0);
       if(firstChar==",") {
           str = str.substring(1);
           str = str.trim();
       }
       var allowed = ["-","1","2","3","4","5","6","7","8","9","0", "."];
       var collect = "",
           minusCnt = 0;
       
       while( allowed.indexOf( str.charAt(0))>=0) {
           if(str.charAt(0)=="-") {
               minusCnt++;
               if(minusCnt>1) {
                   break;
               }
           }
           collect = collect + str.charAt(0);
           str = str.substring(1);
           minusCnt = 1;
       }
       
       // we have a number
       if(collect.length>0) {
          //console.log("Found number "+collect);
          cmd.points.push( parseFloat( collect ));    
       } else {
          // nothing more there...
          //console.log("Did not find number from "+str);
          break;
       }
       str = str.trim();
   }
}

if(!cmd) {
   console.error("No command found for");
   console.error(str);
}

this._activeCmd = cmd;
this._stringLeft = str;

return str;


```

### <a name="svgPathParser_relativePosition"></a>svgPathParser::relativePosition(t)


```javascript

// perhaps faster would be to manage the bezier array directly...
var list = this.toBezierArray();
var ntCnt = list.length;

var t1 = ntCnt * t;
var t_index = Math.floor( t1 );

if(t_index>=ntCnt) t_index = ntCnt-1;
if(t_index<0) t_index = 0;

var bez = list[t_index];
var sub_t = t1 - t_index;

// for example ntCnt = 10
// t = 9,5
var stepLen = 1 / ntCnt,        // 0,1
    nowStep = t_index / ntCnt,  // 0,9
    totStep = t,                // 0,95
    remStep = totStep - nowStep, // 0,05
    relStep = remStep / stepLen; // 0,05 / 0,1 = 0,5

var pathFnData = { x : 0, y : 0, normal : { x : 0, y : 0} };
pathFnData.x = bez.x(relStep);
pathFnData.y = bez.y(relStep);
var nn = bez.tangent(relStep, true);
pathFnData.normal.x = nn.x;
pathFnData.normal.y = nn.y;

return pathFnData;
```

### <a name="svgPathParser_replacePartWith"></a>svgPathParser::replacePartWith(index, pathStr, invert)


```javascript

var createQuatPath2 = function(str, invert) {
    var parser = svgPathParser();
    parser.parse(str);
    parser.makePathAbsolute();
    var list = parser.toBezierArray();
    parser.fromBezierArray( list );
    if(invert) parser.inverse();
    var qPath = parser.toQuaternionPath();
    
    var createQuatPath = function( startPoint, refVector ) {
        
        var iter = pathIterator( qPath );
        var ep = iter.endPoint();
        var str = "M 0 0 "+iter.toSvgPath();
        var sp = startPoint;
        /*
        var refVector = {
            x : -100,
            y : 100
        };*/
        
        if(refVector.x==0 && refVector.y==0) return "";
        
        var len = Math.sqrt(ep.x*ep.x + ep.y*ep.y),
            refLen = Math.sqrt(refVector.x*refVector.x + refVector.y*refVector.y),
            scale = refLen / len;
        if(len==0) return str;
        var math = jsVectors();
        var angle = math.angleBetween( ep, refVector );
        // var angle = math.angleBetween(  refVector, ep );
        var str = iter.toSvgPath(sp, quaternion().rotate(angle), function(p) {
            p.d = p.d*scale;
            return p;
        });
        return str;
    }
    return createQuatPath;
}

var ppp = this.getPath( index );
ppp.replaceFunction = createQuatPath2(pathStr, invert);

```

### <a name="svgPathParser_saveToOriginals"></a>svgPathParser::saveToOriginals()


```javascript
this._original = JSON.parse( JSON.stringify( this._all ) );
   
```

### <a name="svgPathParser_scaleFactor"></a>svgPathParser::scaleFactor(w, h)


```javascript

       var dim = this.findDimensions();
       
       var drawW = Math.abs( dim[2] - dim[0] ),
           drawH = Math.abs( dim[3] - dim[1] );
           
       var scale1 = w / drawW,
           scale2 = h / drawH;
       var x,y;
      
       var scale = Math.min(scale1, scale2);

       return scale; 
   
```

### <a name="svgPathParser_svgString"></a>svgPathParser::svgString(t)


```javascript
var _firstX, _firstY, x, y,
    str = "", me = this;

this._all.forEach(function(cmd) {
   
   if(cmd.name =="M") {

       x = cmd.points[0];
       y = cmd.points[1];
       str+="M"+me.n(x)+","+me.n(y)+" ";
   }
   
   if(cmd.name =="m") {
       x = x + cmd.points[0];
       y = y + cmd.points[1];
       str+="M"+me.n(x)+","+me.n(y)+" ";
   }        
   
   if(cmd.name=="q") {

       str+="Q";
       for(var s=0; s<cmd.points.length;s+=4) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];
           //x=x0; y=y0;
           var x1 = x + p[s+2],
               y1 = y + p[s+3];
           x=x1; y=y1;
           str+=me.n(x0)+","+me.n(y0)+" "+me.n(x1)+","+me.n(y1)+" ";
       }
   }
   
   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="Q") {
       var p = cmd.points,
           len = cmd.points.length;
       str+="Q";
       for(var s=0; s<len;s+=4) {
           var x0 = p[s+0],
               y0 = p[s+1];
           var x1 = p[s+2],
               y1 = p[s+3];
           x=x1; y=y1;
           str+=me.n(x0)+","+me.n(y0)+" "+me.n(x1)+","+me.n(y1)+" ";
       }
   }   
   
   if(cmd.name=="c") {
       str+="C";
       for(var s=0; s<cmd.points.length;s+=6) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];
           //x=x0; y=y0;
           var x1 = x + p[s+2],
               y1 = y + p[s+3];
           // x=x1; y=y1;
          var x2 = x + p[s+4],
               y2 = y + p[s+5];
           x=x2; y=y2;
           str+=me.n(x0)+","+me.n(y0)+" "+me.n(x1)+","+me.n(y1)+" "+me.n(x2)+","+me.n(y2)+" ";
       }
   }
   
   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="C") {
       
       var p = cmd.points,
           len = cmd.points.length;
           
       if(cmd.replaceFunction) {
           var sp = {
               x : x,
               y : y
           };
           for(var s=0; s<len;s+=6) {
               // str+=p[s+0]+","+p[s+1]+" "+p[s+2]+","+p[s+3]+" "+p[s+4]+","+p[s+5]+" ";
               x = p[s+4];
               y = p[s+5];
           }           
           var ref = {
               x : x - sp.x,
               y : y - sp.y
           }
           var strR = cmd.replaceFunction( sp, ref );

           str+=" "+strR+" ";
       } else {     
           str+="C";
           for(var s=0; s<len;s+=6) {
               str+=me.n(p[s+0])+","+me.n(p[s+1])+" "+me.n(p[s+2])+","+me.n(p[s+3])+" "+me.n(p[s+4])+","+me.n(p[s+5])+" ";
               x = p[s+4];
               y = p[s+5];
           }
       }
   }           
   if(cmd.name=="l") {
       str+="L";
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = x + p[s+0],
               y0 = y + p[s+1];  
           x=x0; y=y0;
           str+=me.n(x0)+","+me.n(y0)+" ";
       }
   }
   
   if(cmd.name=="H") {
       str+="L";
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var x0 = p[s+0];  
           x=x0; 
           // ctx.lineTo( x0, y );
           str+=me.n(x0)+","+me.n(y)+" ";
       }
   }    
   
   if(cmd.name=="V") {
       str+="L";
       for(var s=0; s<cmd.points.length;s++) {
           var p = cmd.points;
           var y0 = p[s+0];  
           y=y0; 
           // ctx.lineTo( x, y0 );
           str+=me.n(x)+","+me.n(y0)+" ";
       }
   }
   

   if(cmd.name=="L") {
       
       if(cmd.replaceFunction) {
           var sp = {
               x : x,
               y : y
           };
           for(var s=0; s<cmd.points.length;s+=2) {
               var p = cmd.points;
               var x0 = p[s+0],
                   y0 = p[s+1];  
               x=x0; y=y0;
           }         
           var ref = {
               x : x - sp.x,
               y : y - sp.y
           }
           var strR = cmd.replaceFunction( sp, ref );
           str+=" "+strR+" ";
       } else {       
           str+="L";
           for(var s=0; s<cmd.points.length;s+=2) {
               var p = cmd.points;
               var x0 = p[s+0],
                   y0 = p[s+1];  
               x=x0; y=y0;
               // ctx.lineTo( x0,y0 );
               str+=me.n(x0)+","+me.n(y0)+" ";
           }
       }
   }           
   
   if(cmd.name=="z") {
       str+="z";
   }
});
return str;
     
   
```

### <a name="svgPathParser_toBezierArray"></a>svgPathParser::toBezierArray(t)


```javascript
var _firstX, _firstY, x, y,
    str = "",
    res = [];
this._all.forEach(function(cmd) {
   
   if(cmd.name =="M") {
       x = cmd.points[0];
       y = cmd.points[1];
   }

   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="Q") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=4) {
           var x0 = p[s+0],
               y0 = p[s+1];
           var x1 = p[s+2],
               y1 = p[s+3];
           
           var bc = new jsBezierCurve();
           bc.fromQuadCurve({ x : x, y : y},{ x : x0, y : y0},{ x : x1, y : y1});
           res.push(bc);
           x=x1; y=y1;
       }
   }
   
   // Not relative coordinates... the algo is much simpler here...
   if(cmd.name=="C") {
       var p = cmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=6) {
           
           var x0 = p[s+0],
               y0 = p[s+1];
           var x1 = p[s+2],
               y1 = p[s+3];
           var x2 = p[s+4],
               y2 = p[s+5];       
           var bc = new jsBezierCurve();
           bc.fromPoints({ x : x, y : y},{ x : x0, y : y0},{ x : x1, y : y1}, { x : x2, y : y2});
           res.push(bc);
           x=x2; y=y2;
       }
   }           


   if(cmd.name=="L") {
       str+="L";
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points;
           var x0 = p[s+0],
               y0 = p[s+1];  
           var bc = new jsBezierCurve();
           bc.fromLine({ x : x, y : y},{ x : x0, y : y0});
           res.push(bc);               
               
           x=x0; y=y0;
       }
   }           

});
return res;
     
   
```

### <a name="svgPathParser_toQuaternionPath"></a>svgPathParser::toQuaternionPath(t)


```javascript

var isFirstPoint = true;
var pv = {
    x : 0,
    y : 0
};
var dv = {
    x : 100,
    y : 0
};
var lastDv = {
    x : 100,
    y : 0
};

var matLib = jsVectors();

var cmdList = [];

// {"name":"L","points":[374.29469458855607,171.03419547847162]}
this.forCmds( function(c) {
   //  main.div().text(JSON.stringify(c));
    var v = {};
    var cmd = { cmd : c.name, path : [] };
    
    var pickQuat = function(x,y) {

        dv.x = x - pv.x;
        dv.y = y - pv.y;
        var dist = Math.sqrt( dv.x*dv.x + dv.y*dv.y );
        if(dist==0) {
            dv.x += 0.2;
            dv.y += 0.2;
            x += 0.02;
            y += 0.02;
            dist = Math.sqrt( dv.x*dv.x + dv.y*dv.y );
        }
        var r = matLib.angleBetween( lastDv, dv );
        

        var q = quaternion();
        q.setFromAxisRotation({
            x : 0,
            y : 0,
            z : 1
        }, r);   
        
        if(!isFirstPoint) cmd.path.push({ q : q, d : dist});
        isFirstPoint = false;
        pv.x = x;
        pv.y = y;
        lastDv.x = dv.x;
        lastDv.y = dv.y;        
        
    }
    
    if(c.name=="M") {
        pickQuat( c.points[0], c.points[1]);
    }    
    if(c.name=="L") {
        pickQuat( c.points[0], c.points[1]);
    }
    if(c.name=="Q") {
        pickQuat( c.points[0], c.points[1]);
        pickQuat( c.points[2], c.points[3]);
    }    
    if(c.name=="C") {
        pickQuat( c.points[0], c.points[1]);
        pickQuat( c.points[2], c.points[3]);
        pickQuat( c.points[4], c.points[5]);
    }
    if(cmd.path.length) cmdList.push(cmd);
});

return cmdList;
```

### <a name="svgPathParser_transformPoints"></a>svgPathParser::transformPoints(fn)


```javascript

// creates a backup of the "all" and then uses the "all" as target
var all = this.originals();
var point = { x: 0, y:0 };
var x,y,i,plen = all.length;
var target = this._all;

for(var i=0; i<plen;i++) {
    
    var cmd = all[i],
       tCmd = this._all[i];
    
    if(!cmd) return;
    
    if(cmd.name =="M") {
       point.x  = cmd.points[0];
       point.y  = cmd.points[1];
       fn(point);
       tCmd.points[0] = point.x;
       tCmd.points[1] = point.y;
       
    }
    
    if(cmd.name=="Q") {
       var p = cmd.points,
           tp = tCmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=4) {
           
           point.x  = p[s+0], point.y  = p[s+1];     
           fn(point);
           tp[s+0] = point.x, tp[s+1] = point.y;
    
           point.x  = p[s+2], point.y  = p[s+3];     
           fn(point);
           tp[s+2] = point.x, tp[s+3] = point.y;
           
       }
    }
    
    
    if(cmd.name=="C") {
       var p = cmd.points,
           tp = tCmd.points,
           len = cmd.points.length;
       for(var s=0; s<len;s+=6) {
           
           point.x  = p[s+0], point.y  = p[s+1];     
           fn(point);
           tp[s+0] = point.x, tp[s+1] = point.y;
    
           point.x  = p[s+2], point.y  = p[s+3];     
           fn(point);
           tp[s+2] = point.x, tp[s+3] = point.y;
           
           point.x  = p[s+4], point.y  = p[s+5];     
           fn(point);
           tp[s+4] = point.x, tp[s+5] = point.y;                   
       }
    }           
    if(cmd.name=="L") {
       for(var s=0; s<cmd.points.length;s+=2) {
           var p = cmd.points,
               tp = tCmd.points;
           point.x  = p[s+0], point.y  = p[s+1];     
           fn(point);
           tp[s+0] = point.x, tp[s+1] = point.y;
       }
    }
    
}      
    
    
    

```



   
    
    
    
    
    
    
    
    


   
      
            
# Class jsVectors


The class has following internal singleton variables:
        
* projectionMatrix
        
* jVect
        
* iVect
        
* pBase
        
* tn1
        
* nv1
        
* barCoeffs
        
* deVector
        
        
### <a name="jsVectors_add"></a>jsVectors::add(v1, v2)


```javascript

    v1.x = v1.x + v2.x;
    v1.y = v1.y + v2.y;
    
```

### <a name="jsVectors_angleBetween"></a>jsVectors::angleBetween(v1, v2)


```javascript

var n1 = this.normalize( { x : v1.x, y : v1.y } );
var n2 = this.normalize( { x : v2.x, y : v2.y } );

var cp = this.crossProd( n1, n2 );
var dp = this.dotProd(n1, n2 );

var a = Math.acos( dp );
if(cp<0) a = a*-1; // other side...
return a;
    
```

### <a name="jsVectors_calc_cat"></a>jsVectors::calc_cat(t, p0, p1, p2, p3)


```javascript

var t2 = t*t;
var t3 = t2 * t;
return (0.5 *(  (2 * p1) + (-p0 + p2) * t +(2*p0 - 5*p1 + 4*p2 - p3) * t2 +(-p0 + 3*p1- 3*p2 + p3) * t3));

```

### <a name="jsVectors_crossProd"></a>jsVectors::crossProd(v1, v2)


```javascript

        // U x V = Ux*Vy-Uy*Vx
        return v1.x*v2.y - v1.y*v2.x;
    
```

### <a name="jsVectors_diff"></a>jsVectors::diff(p1, p2)


```javascript

return { x : p2.x - p1.x,
         y : p2.y - p1.y };
    
```

### <a name="jsVectors_dist"></a>jsVectors::dist(p1, p2)


```javascript
                    
var dx = p1.x - p2.x;
var dy = p1.y - p2.y;
return Math.sqrt( dx*dx + dy*dy );
    
```

### <a name="jsVectors_dotProd"></a>jsVectors::dotProd(v1, v2)


```javascript

return v1.x*v2.x + v1.y*v2.y;
    
```

### <a name="jsVectors_getBarCoeffs"></a>jsVectors::getBarCoeffs(p0, p1, p2)


```javascript

var bb = barCoeffs;
bb.A = 1/2 * (-p1.y * p2.x + p0.y * (-p1.x + p2.x) + p0.x * (p1.y - p2.y) + p1.x * p2.y);
bb.sign = bb.A < 0 ? -1 : 1;
bb.s1 = (p0.y * p2.x - p0.x * p2.y + (p2.y - p0.y) ) *bb.sign;
bb.s2 = (p2.y - p0.y) * bb.sign;
bb.s3 = (p0.x - p2.x) * bb.sign;
bb.t1 = (p0.x * p1.y - p0.y * p1.x)*bb.sign;
bb.t2 = (p0.y - p1.y) * bb.sign;
bb.t3 = (p1.x - p0.x) * bb.sign;
return bb;
    
```

### jsVectors::constructor( t )

```javascript

if(!tn1) { 
    
   tn1 = { x: 0, y : 0};
   nv1 = { x: 0, y : 0};
   
   projectionMatrix = [0,0,0,0];
   
   jVect = { x:0, y:0 };
   iVect = { x:0, y:0 };
   pBase = { x:0, y:0 }; 
   
   barCoeffs = { Area : 0, s1 : 0, s2 : 0, s3 : 0, t1:0, t2:0, t3:0, sign : 0 };   
   deVector = { x:0, y:0};
   
}
```
        
### <a name="jsVectors_initProjection"></a>jsVectors::initProjection(p1, p2)


```javascript

iVect.y = p2.y - p1.y;
iVect.x = p2.x - p1.x;

jVect.y = iVect.y;
jVect.x = iVect.x;

this.normalize(iVect);
this.normalize(jVect);

this.rotate( jVect, Math.PI/2);

pBase.x = p1.x;
pBase.y = p1.y;
       
   
```

### <a name="jsVectors_length"></a>jsVectors::length(p1)


```javascript

var dx = p1.x;
var dy = p1.y;
return Math.sqrt( dx*dx + dy*dy );        
    
```

### <a name="jsVectors_linesIntersect"></a>jsVectors::linesIntersect(p0, p1, v0, v1)


```javascript

var x1 = p0.x,
    y1 = p0.y,
    x2 = p1.x,
    y2 = p1.y,
    x3 = v0.x,
    y3 = v0.y,
    x4 = v1.x,
    y4 = v1.y;

var x=((x1*y2-y1*x2)*(x3-x4)-(x1-x2)*(x3*y4-y3*x4))/((x1-x2)*(y3-y4)-(y1-y2)*(x3-x4));
var y=((x1*y2-y1*x2)*(y3-y4)-(y1-y2)*(x3*y4-y3*x4))/((x1-x2)*(y3-y4)-(y1-y2)*(x3-x4));
if (isNaN(x)||isNaN(y)) {
    return false;
} else {
    if (x1>=x2) {
        if (!(x2<=x&&x<=x1)) {return false;}
    } else {
        if (!(x1<=x&&x<=x2)) {return false;}
    }
    if (y1>=y2) {
        if (!(y2<=y&&y<=y1)) {return false;}
    } else {
        if (!(y1<=y&&y<=y2)) {return false;}
    }
    if (x3>=x4) {
        if (!(x4<=x&&x<=x3)) {return false;}
    } else {
        if (!(x3<=x&&x<=x4)) {return false;}
    }
    if (y3>=y4) {
        if (!(y4<=y&&y<=y3)) {return false;}
    } else {
        if (!(y3<=y&&y<=y4)) {return false;}
    }
}
return true;
    
```

### <a name="jsVectors_mirrorVector"></a>jsVectors::mirrorVector(v1, along, base)


```javascript

// the direction tangent and normal are normalized and the vector is projected into it            
tn1.x = along.x - base.x;   
tn1.y = along.y - base.y;
nv1.x = -tn1.y;
nv1.y = tn1.x;

v1.x = v1.x - base.x;
v1.y = v1.y - base.y;

// if the 'j' or normal projection is positive, turn around
if( this.dotProd(v1,nv1) > 0) 
    this.rotate(nv1, Math.PI);        

this.normalize(tn1);
this.normalize(nv1);

// Create positive coordinates of the projection of the vector to the 'base' cordinates
var nvProd = Math.abs( this.dotProd(v1,nv1) );
//             tnProd = Math.abs( this.dotProd(v1,tn1) );
    
var tnProd = this.dotProd(v1,tn1);
// then, project the length of the base vectors to get the new vector space
v1.x = nv1.x * nvProd + tn1.x *tnProd,
v1.y = nv1.y * nvProd + tn1.y *tnProd;   

v1.x += base.x;
v1.y += base.y;

return v1;        
    
```

### <a name="jsVectors_normalize"></a>jsVectors::normalize(v)


```javascript

var len = Math.sqrt( v.x*v.x + v.y*v.y);

if(len==0) {
    throw "Error normalizing vector: the length of the vector was zero";
}

v.x = v.x/len;
v.y = v.y/len;
return v;
    
```

### <a name="jsVectors_opposeVector"></a>jsVectors::opposeVector(v1, along)


```javascript


// the direction tangent and normal are normalized and the vector is projected into it            
tn1.x = along,x;   
tn1.y = along.y;
nv1.x = -tn1.y;
nv1.y = tn1.x;

this.normalize(tn1);
this.normalize(nv1);

// Important: turn the tangent to opposing direction...
this.rotate(tn1, Math.PI);

// Create the projection of the vector to the 'base' cordinates
var nvProd = Math.abs( jsMath.dotProd(v1,nv1) ),
    tnProd = Math.abs( jsMath.dotProd(v1,tn1) );
    
// if the 'j' or normal projection is negative, turn around
if( this.dotProd(v1,nv1) < 0) 
    this.rotate(nv1, Math.PI);
    
// then, project the length of the vector to get the new vector
v1.x = nv1.x * nvProd + tn1.x *tnProd,
v1.y = nv1.y * nvProd + tn1.y *tnProd;        

return v1;
    
```

### <a name="jsVectors_pointInTriangle"></a>jsVectors::pointInTriangle(p, p0, p1, p2)


```javascript


var A = 1/2 * (-p1.y * p2.x + p0.y * (-p1.x + p2.x) + p0.x * (p1.y - p2.y) + p1.x * p2.y);
var sign = A < 0 ? -1 : 1;
var s = (p0.y * p2.x - p0.x * p2.y + (p2.y - p0.y) * p.x + (p0.x - p2.x) * p.y) * sign;
var t = (p0.x * p1.y - p0.y * p1.x + (p0.y - p1.y) * p.x + (p1.x - p0.x) * p.y) * sign;

return s > 0 && t > 0 && (s + t) < 2 * A * sign;
        
    
```

### <a name="jsVectors_pointInTriangleBc"></a>jsVectors::pointInTriangleBc(p, bb)


```javascript

var A = bb.A;
var sign = bb.sign;
var s = (bb.s1 +  bb.s2 * p.x + bb.s3 * p.y);
var t = (bb.t1 +  bb.t2 * p.x + bb.t3 * p.y);

return s > 0 && t > 0 && (s + t) < 2 * A * sign;
        
    
```

### <a name="jsVectors_project"></a>jsVectors::project(vectorToProject)


```javascript


var p = vectorToProject;

pVector.x = p.x - pBase.x;
pVector.y = p.y - pBase.y;

prodResult.i = this.dotProd( pVector, iVect);
prodResult.j = this.dotProd( pVector, jVect);

return prodResult;

```

### <a name="jsVectors_rotate"></a>jsVectors::rotate(v, angle)


```javascript


var s = Math.sin(angle);
var c = Math.cos(angle);

var x = v.x,
    y = v.y;

v.x = x * c + y * s;
v.y = -x * s + y * c;

return v;
    
```

### <a name="jsVectors_rotateAround"></a>jsVectors::rotateAround(angle, v, around)


```javascript

this.sub(v, around);
this.rotate(v,angle);
this.add(v,around);
    
```

### <a name="jsVectors_sub"></a>jsVectors::sub(v1, v2)


```javascript

v1.x = v1.x - v2.x;
v1.y = v1.y - v2.y;
    
```

### <a name="jsVectors_tangentNormal"></a>jsVectors::tangentNormal(v1, v2, v3)


```javascript


var t1 = {};
t1.x = v2.x - v1.x;
t1.y = v2.y - v1.y;
var t2 = {};
t2.x = v3.x - v2.x;
t2.y = v3.y - v2.y;

var p = { x : t1.x+t2.x,
          y : t1.y+t2.y
        };
return this.normalize(p);
    
```

### <a name="jsVectors_triangleArea"></a>jsVectors::triangleArea(A, B, C)


```javascript

        
var area = A.x * ( B.y - C.y ) +
           B.x * ( C.y - A.y ) +
           C.x * ( A.y - B.y );
        
return Math.abs( area / 2);        
    
```

### <a name="jsVectors_triangleInTriangle"></a>jsVectors::triangleInTriangle(p0, p1, p2, q0, q1, q2)


```javascript

        
var bb = this.getBarCoeffs(p0,p1,p2);

if(this.pointInTriangleBc( q0, bb) ) return true;
if(this.pointInTriangleBc( q1, bb) ) return true;
if(this.pointInTriangleBc( q2, bb) ) return true;

var bb = this.getBarCoeffs(q0, q1, q2 );

if(this.pointInTriangleBc( p0, bb) ) return true;
if(this.pointInTriangleBc( p1, bb) ) return true;
if(this.pointInTriangleBc( p2, bb) ) return true;


if(this.linesIntersect( p0,p1, q0,q1)) return true;
if(this.linesIntersect( p1,p2, q0,q1)) return true;
if(this.linesIntersect( p2,p0, q0,q1)) return true;

if(this.linesIntersect( p0,p1, q1,q2)) return true;
if(this.linesIntersect( p1,p2, q1,q2)) return true;
if(this.linesIntersect( p2,p0, q1,q2)) return true;        

if(this.linesIntersect( p0,p1, q2,q0)) return true;
if(this.linesIntersect( p1,p2, q2,q0)) return true;
if(this.linesIntersect( p2,p0, q2,q0)) return true;             

return false;
    
```

### <a name="jsVectors_unProject"></a>jsVectors::unProject(projectedVector)


```javascript

var p = projectedVector;
deVector.x = p.i * iVect.x + p.j * jVect.x;
deVector.y = p.i * iVect.y + p.j * jVect.y;

deVector.x += pBase.x;
deVector.y += pBase.y;
return deVector;
   
```



   


   



      
    
      
            
# Class quaternion


The class has following internal singleton variables:
        
        
### <a name="quaternion_copy"></a>quaternion::copy(q)


```javascript
this.x = q.x;
this.y = q.y;
this.z = q.z;
this.w = q.w;
```

### quaternion::constructor( x, y, z, w )

```javascript
this.x = x || 0;
this.y = y || 0;
this.z = z || 0;
this.w = ( w !== undefined ) ? w : 1;

```
        
### <a name="quaternion_inverse"></a>quaternion::inverse(t)


```javascript
this.x *= -1;
this.y *= -1;
this.z *= -1;
return this;
```

### <a name="quaternion_multiply"></a>quaternion::multiply(q1, q2)


```javascript

if(!q2) {
    q2 = q1;
    q1 = this;
}

var x =  q1.x * q2.w + q1.y * q2.z - q1.z * q2.y + q1.w * q2.x;
var y = -q1.x * q2.z + q1.y * q2.w + q1.z * q2.x + q1.w * q2.y;
var z =  q1.x * q2.y - q1.y * q2.x + q1.z * q2.w + q1.w * q2.z;
var w = -q1.x * q2.x - q1.y * q2.y - q1.z * q2.z + q1.w * q2.w;

this.x = x;
this.y = y;
this.z = z;
this.w = w;

return this;
```

### <a name="quaternion_normalizeVector3D"></a>quaternion::normalizeVector3D(v)


```javascript
var len = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );

if(len == 0 || isNaN(len)) return {
    x : 1,
    y : 0,
    z : 0
};

return {
    x : v.x / len,
    y : v.y / len,
    z : v.z / len
};

```

### <a name="quaternion_projectVector"></a>quaternion::projectVector(vector)


```javascript
var dest = {
    x : 0,
    y : 0,
    z : 0
};

// p=q∗vq

var x    = vector.x,  y  = vector.y,  z  = vector.z,
  qx   = this.x, qy = this.y, qz = this.z, qw = this.w;

// calculate quat * vector

var ix =  qw * x + qy * z - qz * y,
  iy =  qw * y + qz * x - qx * z,
  iz =  qw * z + qx * y - qy * x,
  iw = -qx * x - qy * y - qz * z;

// calculate result * inverse quat

dest.x = ix * qw + iw * -qx + iy * -qz - iz * -qy;
dest.y = iy * qw + iw * -qy + iz * -qx - ix * -qz;
dest.z = iz * qw + iw * -qz + ix * -qy - iy * -qx;

return dest;

```

### <a name="quaternion_rotate"></a>quaternion::rotate(r)


```javascript
this.setFromAxisRotation({
    x : 0,
    y : 0,
    z : 1
}, r);

return this;
```

### <a name="quaternion_setFromAxisRotation"></a>quaternion::setFromAxisRotation(v, rot)


```javascript
 
v = this.normalizeVector3D(v);

var halfAngle = rot / 2,
  s = Math.sin( halfAngle );

this.x = v.x * s;
this.y = v.y * s;
this.z = v.z * s;
this.w = Math.cos( halfAngle );

return this;

```



   
    
    


   
      
            
# Class jsVectors


The class has following internal singleton variables:
        
* projectionMatrix
        
* jVect
        
* iVect
        
* pBase
        
* tn1
        
* nv1
        
* barCoeffs
        
* deVector
        
        
### <a name="jsVectors_add"></a>jsVectors::add(v1, v2)


```javascript

    v1.x = v1.x + v2.x;
    v1.y = v1.y + v2.y;
    
```

### <a name="jsVectors_angleBetween"></a>jsVectors::angleBetween(v1, v2)


```javascript

var n1 = this.normalize( { x : v1.x, y : v1.y } );
var n2 = this.normalize( { x : v2.x, y : v2.y } );

var cp = this.crossProd( n1, n2 );
var dp = this.dotProd(n1, n2 );

var a = Math.acos( dp );
if(cp<0) a = a*-1; // other side...
return a;
    
```

### <a name="jsVectors_calc_cat"></a>jsVectors::calc_cat(t, p0, p1, p2, p3)


```javascript

var t2 = t*t;
var t3 = t2 * t;
return (0.5 *(  (2 * p1) + (-p0 + p2) * t +(2*p0 - 5*p1 + 4*p2 - p3) * t2 +(-p0 + 3*p1- 3*p2 + p3) * t3));

```

### <a name="jsVectors_crossProd"></a>jsVectors::crossProd(v1, v2)


```javascript

        // U x V = Ux*Vy-Uy*Vx
        return v1.x*v2.y - v1.y*v2.x;
    
```

### <a name="jsVectors_diff"></a>jsVectors::diff(p1, p2)


```javascript

return { x : p2.x - p1.x,
         y : p2.y - p1.y };
    
```

### <a name="jsVectors_dist"></a>jsVectors::dist(p1, p2)


```javascript
                    
var dx = p1.x - p2.x;
var dy = p1.y - p2.y;
return Math.sqrt( dx*dx + dy*dy );
    
```

### <a name="jsVectors_dotProd"></a>jsVectors::dotProd(v1, v2)


```javascript

return v1.x*v2.x + v1.y*v2.y;
    
```

### <a name="jsVectors_getBarCoeffs"></a>jsVectors::getBarCoeffs(p0, p1, p2)


```javascript

var bb = barCoeffs;
bb.A = 1/2 * (-p1.y * p2.x + p0.y * (-p1.x + p2.x) + p0.x * (p1.y - p2.y) + p1.x * p2.y);
bb.sign = bb.A < 0 ? -1 : 1;
bb.s1 = (p0.y * p2.x - p0.x * p2.y + (p2.y - p0.y) ) *bb.sign;
bb.s2 = (p2.y - p0.y) * bb.sign;
bb.s3 = (p0.x - p2.x) * bb.sign;
bb.t1 = (p0.x * p1.y - p0.y * p1.x)*bb.sign;
bb.t2 = (p0.y - p1.y) * bb.sign;
bb.t3 = (p1.x - p0.x) * bb.sign;
return bb;
    
```

### jsVectors::constructor( t )

```javascript

if(!tn1) { 
    
   tn1 = { x: 0, y : 0};
   nv1 = { x: 0, y : 0};
   
   projectionMatrix = [0,0,0,0];
   
   jVect = { x:0, y:0 };
   iVect = { x:0, y:0 };
   pBase = { x:0, y:0 }; 
   
   barCoeffs = { Area : 0, s1 : 0, s2 : 0, s3 : 0, t1:0, t2:0, t3:0, sign : 0 };   
   deVector = { x:0, y:0};
   
}
```
        
### <a name="jsVectors_initProjection"></a>jsVectors::initProjection(p1, p2)


```javascript

iVect.y = p2.y - p1.y;
iVect.x = p2.x - p1.x;

jVect.y = iVect.y;
jVect.x = iVect.x;

this.normalize(iVect);
this.normalize(jVect);

this.rotate( jVect, Math.PI/2);

pBase.x = p1.x;
pBase.y = p1.y;
       
   
```

### <a name="jsVectors_length"></a>jsVectors::length(p1)


```javascript

var dx = p1.x;
var dy = p1.y;
return Math.sqrt( dx*dx + dy*dy );        
    
```

### <a name="jsVectors_linesIntersect"></a>jsVectors::linesIntersect(p0, p1, v0, v1)


```javascript

var x1 = p0.x,
    y1 = p0.y,
    x2 = p1.x,
    y2 = p1.y,
    x3 = v0.x,
    y3 = v0.y,
    x4 = v1.x,
    y4 = v1.y;

var x=((x1*y2-y1*x2)*(x3-x4)-(x1-x2)*(x3*y4-y3*x4))/((x1-x2)*(y3-y4)-(y1-y2)*(x3-x4));
var y=((x1*y2-y1*x2)*(y3-y4)-(y1-y2)*(x3*y4-y3*x4))/((x1-x2)*(y3-y4)-(y1-y2)*(x3-x4));
if (isNaN(x)||isNaN(y)) {
    return false;
} else {
    if (x1>=x2) {
        if (!(x2<=x&&x<=x1)) {return false;}
    } else {
        if (!(x1<=x&&x<=x2)) {return false;}
    }
    if (y1>=y2) {
        if (!(y2<=y&&y<=y1)) {return false;}
    } else {
        if (!(y1<=y&&y<=y2)) {return false;}
    }
    if (x3>=x4) {
        if (!(x4<=x&&x<=x3)) {return false;}
    } else {
        if (!(x3<=x&&x<=x4)) {return false;}
    }
    if (y3>=y4) {
        if (!(y4<=y&&y<=y3)) {return false;}
    } else {
        if (!(y3<=y&&y<=y4)) {return false;}
    }
}
return true;
    
```

### <a name="jsVectors_mirrorVector"></a>jsVectors::mirrorVector(v1, along, base)


```javascript

// the direction tangent and normal are normalized and the vector is projected into it            
tn1.x = along.x - base.x;   
tn1.y = along.y - base.y;
nv1.x = -tn1.y;
nv1.y = tn1.x;

v1.x = v1.x - base.x;
v1.y = v1.y - base.y;

// if the 'j' or normal projection is positive, turn around
if( this.dotProd(v1,nv1) > 0) 
    this.rotate(nv1, Math.PI);        

this.normalize(tn1);
this.normalize(nv1);

// Create positive coordinates of the projection of the vector to the 'base' cordinates
var nvProd = Math.abs( this.dotProd(v1,nv1) );
//             tnProd = Math.abs( this.dotProd(v1,tn1) );
    
var tnProd = this.dotProd(v1,tn1);
// then, project the length of the base vectors to get the new vector space
v1.x = nv1.x * nvProd + tn1.x *tnProd,
v1.y = nv1.y * nvProd + tn1.y *tnProd;   

v1.x += base.x;
v1.y += base.y;

return v1;        
    
```

### <a name="jsVectors_normalize"></a>jsVectors::normalize(v)


```javascript

var len = Math.sqrt( v.x*v.x + v.y*v.y);

if(len==0) {
    throw "Error normalizing vector: the length of the vector was zero";
}

v.x = v.x/len;
v.y = v.y/len;
return v;
    
```

### <a name="jsVectors_opposeVector"></a>jsVectors::opposeVector(v1, along)


```javascript


// the direction tangent and normal are normalized and the vector is projected into it            
tn1.x = along,x;   
tn1.y = along.y;
nv1.x = -tn1.y;
nv1.y = tn1.x;

this.normalize(tn1);
this.normalize(nv1);

// Important: turn the tangent to opposing direction...
this.rotate(tn1, Math.PI);

// Create the projection of the vector to the 'base' cordinates
var nvProd = Math.abs( jsMath.dotProd(v1,nv1) ),
    tnProd = Math.abs( jsMath.dotProd(v1,tn1) );
    
// if the 'j' or normal projection is negative, turn around
if( this.dotProd(v1,nv1) < 0) 
    this.rotate(nv1, Math.PI);
    
// then, project the length of the vector to get the new vector
v1.x = nv1.x * nvProd + tn1.x *tnProd,
v1.y = nv1.y * nvProd + tn1.y *tnProd;        

return v1;
    
```

### <a name="jsVectors_pointInTriangle"></a>jsVectors::pointInTriangle(p, p0, p1, p2)


```javascript


var A = 1/2 * (-p1.y * p2.x + p0.y * (-p1.x + p2.x) + p0.x * (p1.y - p2.y) + p1.x * p2.y);
var sign = A < 0 ? -1 : 1;
var s = (p0.y * p2.x - p0.x * p2.y + (p2.y - p0.y) * p.x + (p0.x - p2.x) * p.y) * sign;
var t = (p0.x * p1.y - p0.y * p1.x + (p0.y - p1.y) * p.x + (p1.x - p0.x) * p.y) * sign;

return s > 0 && t > 0 && (s + t) < 2 * A * sign;
        
    
```

### <a name="jsVectors_pointInTriangleBc"></a>jsVectors::pointInTriangleBc(p, bb)


```javascript

var A = bb.A;
var sign = bb.sign;
var s = (bb.s1 +  bb.s2 * p.x + bb.s3 * p.y);
var t = (bb.t1 +  bb.t2 * p.x + bb.t3 * p.y);

return s > 0 && t > 0 && (s + t) < 2 * A * sign;
        
    
```

### <a name="jsVectors_project"></a>jsVectors::project(vectorToProject)


```javascript


var p = vectorToProject;

pVector.x = p.x - pBase.x;
pVector.y = p.y - pBase.y;

prodResult.i = this.dotProd( pVector, iVect);
prodResult.j = this.dotProd( pVector, jVect);

return prodResult;

```

### <a name="jsVectors_rotate"></a>jsVectors::rotate(v, angle)


```javascript


var s = Math.sin(angle);
var c = Math.cos(angle);

var x = v.x,
    y = v.y;

v.x = x * c + y * s;
v.y = -x * s + y * c;

return v;
    
```

### <a name="jsVectors_rotateAround"></a>jsVectors::rotateAround(angle, v, around)


```javascript

this.sub(v, around);
this.rotate(v,angle);
this.add(v,around);
    
```

### <a name="jsVectors_sub"></a>jsVectors::sub(v1, v2)


```javascript

v1.x = v1.x - v2.x;
v1.y = v1.y - v2.y;
    
```

### <a name="jsVectors_tangentNormal"></a>jsVectors::tangentNormal(v1, v2, v3)


```javascript


var t1 = {};
t1.x = v2.x - v1.x;
t1.y = v2.y - v1.y;
var t2 = {};
t2.x = v3.x - v2.x;
t2.y = v3.y - v2.y;

var p = { x : t1.x+t2.x,
          y : t1.y+t2.y
        };
return this.normalize(p);
    
```

### <a name="jsVectors_triangleArea"></a>jsVectors::triangleArea(A, B, C)


```javascript

        
var area = A.x * ( B.y - C.y ) +
           B.x * ( C.y - A.y ) +
           C.x * ( A.y - B.y );
        
return Math.abs( area / 2);        
    
```

### <a name="jsVectors_triangleInTriangle"></a>jsVectors::triangleInTriangle(p0, p1, p2, q0, q1, q2)


```javascript

        
var bb = this.getBarCoeffs(p0,p1,p2);

if(this.pointInTriangleBc( q0, bb) ) return true;
if(this.pointInTriangleBc( q1, bb) ) return true;
if(this.pointInTriangleBc( q2, bb) ) return true;

var bb = this.getBarCoeffs(q0, q1, q2 );

if(this.pointInTriangleBc( p0, bb) ) return true;
if(this.pointInTriangleBc( p1, bb) ) return true;
if(this.pointInTriangleBc( p2, bb) ) return true;


if(this.linesIntersect( p0,p1, q0,q1)) return true;
if(this.linesIntersect( p1,p2, q0,q1)) return true;
if(this.linesIntersect( p2,p0, q0,q1)) return true;

if(this.linesIntersect( p0,p1, q1,q2)) return true;
if(this.linesIntersect( p1,p2, q1,q2)) return true;
if(this.linesIntersect( p2,p0, q1,q2)) return true;        

if(this.linesIntersect( p0,p1, q2,q0)) return true;
if(this.linesIntersect( p1,p2, q2,q0)) return true;
if(this.linesIntersect( p2,p0, q2,q0)) return true;             

return false;
    
```

### <a name="jsVectors_unProject"></a>jsVectors::unProject(projectedVector)


```javascript

var p = projectedVector;
deVector.x = p.i * iVect.x + p.j * jVect.x;
deVector.y = p.i * iVect.y + p.j * jVect.y;

deVector.x += pBase.x;
deVector.y += pBase.y;
return deVector;
   
```



   


   



      
    



      
    
      
            
# Class jsBezierCurve


The class has following internal singleton variables:
        
* jsMath
        
        
### <a name="jsBezierCurve_derivate"></a>jsBezierCurve::derivate(d, t)


```javascript

        
var P0 = this._points[d][0],
    P1 = this._points[d][1],
    P2 = this._points[d][2],
    P3 = this._points[d][3];
    
var t2 = t*t;
var nt = 1-t;
var nt2 = nt*nt;

// dP(t) / dt =  -3(1-t)^2 * P0 + 3(1-t)^2 * P1 - 6t(1-t) * P1 - 3t^2 * P2 + 6t(1-t) * P2 + 3t^2 * P3
// or from Wikipedia
// 
// F(t)/dt = 3*nt2 * (P1-P0) + 6*t*nt*(P2-P1) + 3*t2*(P3-P2)

// var derivative = -3*nt2* P0 + 3*nt2 * P1 - 6*t*nt*P1 - 3*t2 * P2 + 6*t*nt * P2 + 3*t2 * P3;

// This should give the exact derivate of the point at certain position
var FT_dt = 3*nt2*(P1-P0) + 6*t*nt*(P2-P1) + 3*t2*(P3-P2);
return FT_dt;

```

### <a name="jsBezierCurve_distanceOf"></a>jsBezierCurve::distanceOf(x, y)


```javascript

        var t = this.findClosestT(x,y);
        var dx = this.x(t)-x,
            dy = this.y(t)-y;
        return Math.sqrt(dx*dx+ dy*dy);
    
```

### <a name="jsBezierCurve_findClosestT"></a>jsBezierCurve::findClosestT(x, y)


```javascript

var tStart = 0, tMiddle = 0.5, tEnd = 1;
var iterations = 10;

while(iterations--) {
    var d0_x = this.x(tStart) - x,
        d0_y = this.y(tStart) - y,
        d2_x = this.x(tEnd)-x,
        d2_y = this.y(tEnd)-y;
    var d0 = Math.sqrt( d0_x*d0_x +  d0_y*d0_y),
        d2 = Math.sqrt( d2_x*d2_x +  d2_y*d2_y);
        
    if(d0<d2) {
        tEnd = tMiddle;
    } else {
        tStart = tMiddle;
    }
    tMiddle = tStart + ( tEnd - tStart ) / 2;
}
var d0_x = this.x(tStart) - x,
    d0_y = this.y(tStart) - y,
    d1_x = this.x(tMiddle)-x,
    d1_y = this.y(tMiddle)-y;            
    d2_x = this.x(tEnd)-x,
    d2_y = this.y(tEnd)-y;
var d0 = Math.sqrt( d0_x*d0_x +  d0_y*d0_y),
    d1 = Math.sqrt( d1_x*d1_x +  d1_y*d1_y),
    d2 = Math.sqrt( d2_x*d2_x +  d2_y*d2_y);
    
if(d0<d1 && d0<d2) return tStart;
if(d2<d1 && d2<d0) return tEnd;
return tMiddle;

```

### <a name="jsBezierCurve_fitListTo"></a>jsBezierCurve::fitListTo(list)


```javascript

var start = {
  x:  list[0].point_x(0),
  y:  list[0].point_y(0)
};

var ei = list.length-1;

var end = {
  x:  list[ei].point_x(3),
  y:  list[ei].point_y(3)
};

// what we have here is a list of segments, starting from (x,y) ending to (x2,y2)
// have to rotate
// have to scale

var myStart = {
    x : this.x(0),
    y : this.y(0)
};
var myEnd = {
    x : this.x(1),
    y : this.y(1)
};
var dx = myEnd.x - myStart.x,
    dy = myEnd.y - myStart.y;
    
var myLen = Math.sqrt( dx*dx + dy*dy );

var ldx = end.x - start.x,
    ldy = end.y - start.y;

var listLen = Math.sqrt( ldx*ldx + ldy*ldy );
var relAngle = jsMath.angleBetween({
    x : dx, y : dy
}, {
    x : ldx, y : ldy
});

// TODO: convert to path parser fromBezierArray()
// make a quaternion list
// scale & rotate the quaternion data to create new path




```

### <a name="jsBezierCurve_fromLine"></a>jsBezierCurve::fromLine(p0, p1)


```javascript

var len  = p1.x - p0.x;
var step = len/3;
this.initCoeffs(0, p0.x, p0.x+step, p0.x+step*2, p1.x);

var len  = p1.y - p0.y;
var step = len/3;
this.initCoeffs(1, p0.y, p0.y+step, p0.y+step*2, p1.y);


```

### <a name="jsBezierCurve_fromPoints"></a>jsBezierCurve::fromPoints(p0, p1, p2, p3)


```javascript
this.initCoeffs(0, p0.x, p1.x, p2.x, p3.x);
this.initCoeffs(1, p0.y, p1.y, p2.y, p3.y);
```

### <a name="jsBezierCurve_fromQuadCurve"></a>jsBezierCurve::fromQuadCurve(p0, p1, p2)


```javascript
//CP1 = QP0 + 2/3 *(QP1-QP0)
//CP2 = QP2 + 2/3 *(QP1-QP2)
this.initCoeffs(0, p0.x, p0.x+(2/3)*(p1.x-p0.x), p2.x + (2/3)*(p1.x-p2.x), p2.x);
this.initCoeffs(0, p0.y, p0.y+(2/3)*(p1.y-p0.y), p2.y + (2/3)*(p1.y-p2.y), p2.y);

```

### jsBezierCurve::constructor( t )

```javascript

this._points = [];
this._m = [];

if(!jsMath) jsMath = jsVectors();

this._m = [
    { x: 0, y : 0},
    { x: 0, y : 0},
    { x: 0, y : 0},
    { x: 0, y : 0}
]; 
```
        
### <a name="jsBezierCurve_initCoeffs"></a>jsBezierCurve::initCoeffs(d, v0, v1, v2, v3)


```javascript

        if(!this._coeffs) 
            this._coeffs = [];
            
        if(!this._coeffs[d]) this._coeffs[d] = [];
        if(!this._points[d]) this._points[d] = [];

        // the actual points used in each dimension
        this._points[d][0] = v0;
        this._points[d][1] = v1;
        this._points[d][2] = v2;
        this._points[d][3] = v3;

        var c = this._coeffs[d];
        c[0] = 3 * (v1 - v0);
        c[1] = 3 * (v2 - v1) - c[0];
        c[2] = v3 - v0 - c[0] - c[1];
        c[3] = v0;

        if(d==0) {
            this._m[0].x = v0;
            this._m[1].x = v1;
            this._m[2].x = v2;
            this._m[3].x = v3;
        }  
        if(d==1) {
            this._m[0].y = v0;
            this._m[1].y = v1;
            this._m[2].y = v2;
            this._m[3].y = v3;
        }

```

### <a name="jsBezierCurve_inverseProject"></a>jsBezierCurve::inverseProject(projection)


```javascript

        
        var pt = projection.t;
        
        var n = this.normal(pt,true);
        
        var p_x = n.x * projection.nvProd + this.x(pt),
            p_y = n.y * projection.nvProd + this.y(pt);
        
        var t = this.tangent(pt, true);
        
        p_x = p_x + projection.tangetProd * t.x;
        p_y = p_y + projection.tangetProd * t.y;
        
        // inverse x and inverse y
        projection.ix = p_x;
        projection.iy = p_y;
            
    
```

### <a name="jsBezierCurve_mirrorControls"></a>jsBezierCurve::mirrorControls(t)


```javascript

var base = {
    x : this._points[0][0],
    y : this._points[1][0]
};

var along = {
    x : this._points[0][3],
    y : this._points[1][3]
};

var v1 = {
    x : this._points[0][1],
    y : this._points[1][1]
};
var v2 = {
    x : this._points[0][2],
    y : this._points[1][2]
};

jsMath.mirrorVector( v1, along, base);
jsMath.mirrorVector( v2, along, base);

this.initCoeffs( 0, base.x, v1.x, v2.x, along.x);
this.initCoeffs( 1, base.y, v1.y, v2.y, along.y);

```

### <a name="jsBezierCurve_normal"></a>jsBezierCurve::normal(t, bUnitVector)


```javascript

        var v = this.tangent(t);
        // direction of the curve at certain point...
        var vx = v.x;
        v.x = -v.y;
        v.y = vx;
        if( bUnitVector) jsMath.normalize(v);
        return v;
    
```

### <a name="jsBezierCurve_point_x"></a>jsBezierCurve::point_x(i)


```javascript

        return this._points[0][i];
    
```

### <a name="jsBezierCurve_point_y"></a>jsBezierCurve::point_y(i)


```javascript

        return this._points[1][i];
    
```

### <a name="jsBezierCurve_points"></a>jsBezierCurve::points()


```javascript

        return this._m;
    
```

### <a name="jsBezierCurve_projectPoint"></a>jsBezierCurve::projectPoint(x, y, projection)


```javascript

        
        // logaritmic function ? 
        
        var maxCnt=20;
        var t = 0.5, step = 0.25; // start from the middle
        
        while( maxCnt--) {
            
            // We try to find a point where the projection to the tangent is as small as possible
            var tn = this.tangent(t,true);
            dv.x = x - this.x(t);
            dv.y = y - this.y(t);
            var prod = dv.x * tn.x  +  dv.y*tn.y;
            
            // close enough
            if( Math.abs( prod ) < 0.05 ) {
                // found it...
                break;
            }
            if(prod > 0) {
                t += step;
            } else {
                t += -step;
            }
            step = step / 2;
        }
        
        var n = this.normal(t,true);
        if(!projection) projection = {};
        projection.tangentProd = prod;
        projection.nvProd = n.x * dv.x + n.y * d.y;
        projection.nv_x = n.x;
        projection.nv_y = n.y;
        projection.tn_x = tn.x;
        projection.tn_y = tn.y;
        projection.ix = 0; // when projected back, the inversed coords here
        projection.iy = 0;
        projection.t = t;
        
        return projection;        
    
```

### <a name="jsBezierCurve_setControls"></a>jsBezierCurve::setControls(p0, p1, p2, p3, fn)


```javascript

this.initCoeffs(0, p0.x, p1.x, p2.x, p3.x);
this.initCoeffs(1, p0.y, p1.y, p2.y, p3.y);

    
```

### <a name="jsBezierCurve_split"></a>jsBezierCurve::split(t)


```javascript


var plist = this._points[0];
var v1 = this.splitCoeff(plist[0],plist[1],plist[2],plist[3],t);
plist = this._points[1];
var v2 = this.splitCoeff(plist[0],plist[1],plist[2],plist[3],t);

this.fromPoints(  { x : v1.p0, y : v2.p0 },
                { x : v1.p1, y : v2.p1 },
                { x : v1.p2, y : v2.p2 },
                { x : v1.p3, y : v2.p3 }
);

var b2 = jsBezierCurve();
b2.fromPoints(  { x : v1.p3, y : v2.p3 },
                { x : v1.p4, y : v2.p4 },
                { x : v1.p5, y : v2.p5 },
                { x : v1.p6, y : v2.p6 }
);

return b2;

```

### <a name="jsBezierCurve_splitCoeff"></a>jsBezierCurve::splitCoeff(P0, P1, P2, P3, t)


```javascript
var v = {};
v.p0 = P0;
v.p1 = (1-t)*P0 + t*P1;
var m2 = (1-t)*P1 + t*P2;
v.p5 = (1-t)*P2 + t*P3;

v.p2  = (1-t)*v.p1 + t*m2;
v.p4  = (1-t)*m2 + t*v.p5;
v.p3  = (1-t)*v.p2 + t*v.p4;        
v.p6  = P3;

return v;
```

### <a name="jsBezierCurve_step"></a>jsBezierCurve::step(t, dim)


```javascript

if(!this._coeffs) return;
var c = this._coeffs[dim];
if(!c) return;
var t2 = t*t, t3 = t2*t;
return c[2] * t3 + c[1] * t2 + c[0] *t + c[3];
    
```

### <a name="jsBezierCurve_tangent"></a>jsBezierCurve::tangent(t, bUnitVector)


```javascript

        // direction of the curve at certain point...
        var nv = {};
        nv.x = this.derivate(0,t);
        nv.y = this.derivate(1,t);
        if( bUnitVector) jsMath.normalize(nv);
        return nv;
    
```

### <a name="jsBezierCurve_x"></a>jsBezierCurve::x(t)


```javascript

        return this.step(t,0);
    
```

### <a name="jsBezierCurve_y"></a>jsBezierCurve::y(t)


```javascript

        return this.step(t,1);
    
```

### <a name="jsBezierCurve_z"></a>jsBezierCurve::z(t)


```javascript
return this.step(t,2);
```



   


   



      
    
      
            
# Class pathIterator


The class has following internal singleton variables:
        
        
### <a name="pathIterator_bezierSplit"></a>pathIterator::bezierSplit(P0, P1, P2, P3, t)


```javascript
var v = {};
v.p1 = (1-t)*P0 + t*P1;
var m2 = (1-t)*P1 + t*P2;
v.p5 = (1-t)*P2 + t*P3;

v.p2  = (1-t)*v.p1 + t*m2;
v.p4  = (1-t)*m2 + t*v.p5;
v.p3  = (1-t)*v.p2 + t*v.p4;        

return v;
```

### <a name="pathIterator_endPoint"></a>pathIterator::endPoint(pv, m, fn)


```javascript

if(!pv) {
    pv = {
        x : 0,
        y : 0,
        z : 0
    }
}
if(!m)  m = quaternion();

var me = this,
    cnt = 0;
    
if(!fn) {
    fn = function(q) {
        return q;
    }
}

this.list.forEach( function(c) {
    
    cnt++;
    if(c.cmd=="Q") {
    
        var ii=0;
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;    
            ii++;
        });
    }
    
    if(c.cmd=="M") {
    
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;         
        });
    }
    
    if(c.cmd=="L") {
    
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;         
        });
    }
    
    if(c.cmd=="C") {

        
        var ii=0;
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;    
            ii++;
        });
    }    
})

return pv;

```

### pathIterator::constructor( list )

```javascript

/*
  list of path iterators
 
   {
        q : quaternion,
        d : distance
   },
   {
        q : quaternion,
        d : distance
   },   
*/

this.list = list;

```
        
### <a name="pathIterator_partToSvgPath"></a>pathIterator::partToSvgPath(start, end, pv, m)


```javascript

var str = "";
if(!pv) {
    pv = {
        x : 0,
        y : 0,
        z : 0
    }
}
if(!m)  m = quaternion();

this.addedObjects = [];
var me = this,
    cnt = 0;

this.list.forEach( function(c) {
    
    cnt++;
    
    if(cnt < start) return;
    if(cnt > end ) return;
    
    var g = _e("g");
    g.circle().attr({
        fill : "#ffaa88",
        cx : pv.x,
        cy : pv.y,
        r : 10
    });
    g.svg_text().attr({
        x : pv.x,
        y : pv.y + 10,
        "font-size" : 20,
        "fill" : "black"
    }).text(cnt+"");
    me.addedObjects.push( g );

    if(c.cmd=="Q") {
    
        var ii=0;
        c.path.forEach( function(p) {
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;    
            if(ii==0) {
                str+="Q ";
            }
            str+=" "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
            ii++;
        });
    }
    
    if(c.cmd=="M") {
    
        c.path.forEach( function(p) {
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;         
            str+="M "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
        });
    }
    
    if(c.cmd=="L") {
    
        c.path.forEach( function(p) {
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;         
            str+="L "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
        });
    }
    
    if(c.cmd=="C") {

        
        var ii=0;
        c.path.forEach( function(p) {
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;    
            if(ii==0) {
                str+="C ";
            }
            str+=" "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
            ii++;
        });
        

    }    
    
    
    

    // no screen projection here...
    
    /*
    if(p.sub) {
        var ii = pathIterator( p.sub );
        var subQ = quaternion();
        subQ.copy( m );
        str+= ii.toSvgPath({
            x : pv.x,
            y : pv.y,
            z : pv.z
        }, subQ);
    }
    */
    
})

return str;

/*

var v = m.projectVector({
    x : 100,
    y : 0,
    z : 0
});

main.p().text(JSON.stringify(v));
var vLen = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
main.p().text("len = "+ vLen); 

m.multiply( step2 );

var v = m.projectVector({
    x : 100,
    y : 0,
    z : 0
});

main.p().text(JSON.stringify(v));
var vLen = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
main.p().text("len = "+ vLen);
*/
```

### <a name="pathIterator_pathFunction"></a>pathIterator::pathFunction(t)


```javascript
/*
        this.initBezier();
        var ntCnt = this.getSegmentCount();
        var t1 = ntCnt * t;
        var t_index = Math.floor( t1 );
        var seg = this.getSegmentNro(t_index);
        var sub_t = t1 - t_index;
        
        // for example ntCnt = 10
        // t = 9,5
        var stepLen = 1 / ntCnt,        // 0,1
            nowStep = t_index / ntCnt,  // 0,9
            totStep = t,                // 0,95
            remStep = totStep - nowStep, // 0,05
            relStep = remStep / stepLen; // 0,05 / 0,1 = 0,5
        
        var bez = seg.bezier();
        // console.log("Rel step "+relStep);
        pathFnData.x = bez.x(relStep);
        pathFnData.y = bez.y(relStep);
        var nn = bez.tangent(relStep, true);
        
        pathFnData.normal.x = nn.x;
        pathFnData.normal.y = nn.y;
        
        fn(pathFnData);
*/
```

### <a name="pathIterator_quadToCubic"></a>pathIterator::quadToCubic(P0, P1, P2)


```javascript
//CP1 = QP0 + 2/3 *(QP1-QP0)
//CP2 = QP2 + 2/3 *(QP1-QP2)

return {
    p0 : P0,
    p1 : P0 + 2/3 *(P1-P0),
    p2 : P2 + 2/3 *(P1-P2),
    p3 : P2
}

```

### <a name="pathIterator_toSvgCubicPath"></a>pathIterator::toSvgCubicPath(pv, m)


```javascript
var str = "";
if(!pv) {
    pv = {
        x : 0,
        y : 0,
        z : 0
    }
}
if(!m)  m = quaternion();

var ii = 0;
this.list.forEach( function(p) {
    var dv = { x : p.d, y : 0, z : 0 };
    m.multiply( p.q );
    var v = m.projectVector(dv);
    pv.x += v.x;
    pv.y += v.y;
    pv.z += v.z;
    // no screen projection here...
    if(ii==0) {
        str+="C "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
    } else {
        str+=" "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
    }
    ii++;

    
})

return str;
```

### <a name="pathIterator_toSvgPath"></a>pathIterator::toSvgPath(pv, m, fn)


```javascript

var str = "";
if(!pv) {
    pv = {
        x : 0,
        y : 0,
        z : 0
    }
}
if(!m)  m = quaternion();

this.addedObjects = [];
var me = this,
    cnt = 0;
    
if(!fn) {
    fn = function(q) {
        return q;
    }
}

this.list.forEach( function(c) {
    
    cnt++;
    /*
    var g = _e("g");
    g.circle().attr({
        fill : "#ffaa77",
        cx : pv.x,
        cy : pv.y,
        r : 10
    });
    g.svg_text().attr({
        x : pv.x,
        y : pv.y + 10,
        "font-size" : 20,
        "fill" : "#222222"
    }).text(cnt+"");
    me.addedObjects.push( g ); */

    if(c.cmd=="Q") {
    
        var ii=0;
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;    
            if(ii==0) {
                str+="Q ";
            }
            str+=" "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
            ii++;
        });
    }
    
    if(c.cmd=="M") {
    
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;         
            str+="M "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
        });
    }
    
    if(c.cmd=="L") {
    
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;         
            str+="L "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
        });
    }
    
    if(c.cmd=="C") {

        
        var ii=0;
        c.path.forEach( function(p) {
            p = fn(p);
            var dv = { x : p.d, y : 0, z : 0 };
            m.multiply( p.q );
            var v = m.projectVector(dv);
            pv.x += v.x;
            pv.y += v.y;
            pv.z += v.z;    
            if(ii==0) {
                str+="C ";
            }
            str+=" "+pv.x.toFixed(3)+", "+pv.y.toFixed(3);
            ii++;
        });
        

    }    
    
    
    

    // no screen projection here...
    
    /*
    if(p.sub) {
        var ii = pathIterator( p.sub );
        var subQ = quaternion();
        subQ.copy( m );
        str+= ii.toSvgPath({
            x : pv.x,
            y : pv.y,
            z : pv.z
        }, subQ);
    }
    */
    
})

return str;

/*

var v = m.projectVector({
    x : 100,
    y : 0,
    z : 0
});

main.p().text(JSON.stringify(v));
var vLen = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
main.p().text("len = "+ vLen); 

m.multiply( step2 );

var v = m.projectVector({
    x : 100,
    y : 0,
    z : 0
});

main.p().text(JSON.stringify(v));
var vLen = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
main.p().text("len = "+ vLen);
*/
```



   
    
    


   
      
            
# Class jsVectors


The class has following internal singleton variables:
        
* projectionMatrix
        
* jVect
        
* iVect
        
* pBase
        
* tn1
        
* nv1
        
* barCoeffs
        
* deVector
        
        
### <a name="jsVectors_add"></a>jsVectors::add(v1, v2)


```javascript

    v1.x = v1.x + v2.x;
    v1.y = v1.y + v2.y;
    
```

### <a name="jsVectors_angleBetween"></a>jsVectors::angleBetween(v1, v2)


```javascript

var n1 = this.normalize( { x : v1.x, y : v1.y } );
var n2 = this.normalize( { x : v2.x, y : v2.y } );

var cp = this.crossProd( n1, n2 );
var dp = this.dotProd(n1, n2 );

var a = Math.acos( dp );
if(cp<0) a = a*-1; // other side...
return a;
    
```

### <a name="jsVectors_calc_cat"></a>jsVectors::calc_cat(t, p0, p1, p2, p3)


```javascript

var t2 = t*t;
var t3 = t2 * t;
return (0.5 *(  (2 * p1) + (-p0 + p2) * t +(2*p0 - 5*p1 + 4*p2 - p3) * t2 +(-p0 + 3*p1- 3*p2 + p3) * t3));

```

### <a name="jsVectors_crossProd"></a>jsVectors::crossProd(v1, v2)


```javascript

        // U x V = Ux*Vy-Uy*Vx
        return v1.x*v2.y - v1.y*v2.x;
    
```

### <a name="jsVectors_diff"></a>jsVectors::diff(p1, p2)


```javascript

return { x : p2.x - p1.x,
         y : p2.y - p1.y };
    
```

### <a name="jsVectors_dist"></a>jsVectors::dist(p1, p2)


```javascript
                    
var dx = p1.x - p2.x;
var dy = p1.y - p2.y;
return Math.sqrt( dx*dx + dy*dy );
    
```

### <a name="jsVectors_dotProd"></a>jsVectors::dotProd(v1, v2)


```javascript

return v1.x*v2.x + v1.y*v2.y;
    
```

### <a name="jsVectors_getBarCoeffs"></a>jsVectors::getBarCoeffs(p0, p1, p2)


```javascript

var bb = barCoeffs;
bb.A = 1/2 * (-p1.y * p2.x + p0.y * (-p1.x + p2.x) + p0.x * (p1.y - p2.y) + p1.x * p2.y);
bb.sign = bb.A < 0 ? -1 : 1;
bb.s1 = (p0.y * p2.x - p0.x * p2.y + (p2.y - p0.y) ) *bb.sign;
bb.s2 = (p2.y - p0.y) * bb.sign;
bb.s3 = (p0.x - p2.x) * bb.sign;
bb.t1 = (p0.x * p1.y - p0.y * p1.x)*bb.sign;
bb.t2 = (p0.y - p1.y) * bb.sign;
bb.t3 = (p1.x - p0.x) * bb.sign;
return bb;
    
```

### jsVectors::constructor( t )

```javascript

if(!tn1) { 
    
   tn1 = { x: 0, y : 0};
   nv1 = { x: 0, y : 0};
   
   projectionMatrix = [0,0,0,0];
   
   jVect = { x:0, y:0 };
   iVect = { x:0, y:0 };
   pBase = { x:0, y:0 }; 
   
   barCoeffs = { Area : 0, s1 : 0, s2 : 0, s3 : 0, t1:0, t2:0, t3:0, sign : 0 };   
   deVector = { x:0, y:0};
   
}
```
        
### <a name="jsVectors_initProjection"></a>jsVectors::initProjection(p1, p2)


```javascript

iVect.y = p2.y - p1.y;
iVect.x = p2.x - p1.x;

jVect.y = iVect.y;
jVect.x = iVect.x;

this.normalize(iVect);
this.normalize(jVect);

this.rotate( jVect, Math.PI/2);

pBase.x = p1.x;
pBase.y = p1.y;
       
   
```

### <a name="jsVectors_length"></a>jsVectors::length(p1)


```javascript

var dx = p1.x;
var dy = p1.y;
return Math.sqrt( dx*dx + dy*dy );        
    
```

### <a name="jsVectors_linesIntersect"></a>jsVectors::linesIntersect(p0, p1, v0, v1)


```javascript

var x1 = p0.x,
    y1 = p0.y,
    x2 = p1.x,
    y2 = p1.y,
    x3 = v0.x,
    y3 = v0.y,
    x4 = v1.x,
    y4 = v1.y;

var x=((x1*y2-y1*x2)*(x3-x4)-(x1-x2)*(x3*y4-y3*x4))/((x1-x2)*(y3-y4)-(y1-y2)*(x3-x4));
var y=((x1*y2-y1*x2)*(y3-y4)-(y1-y2)*(x3*y4-y3*x4))/((x1-x2)*(y3-y4)-(y1-y2)*(x3-x4));
if (isNaN(x)||isNaN(y)) {
    return false;
} else {
    if (x1>=x2) {
        if (!(x2<=x&&x<=x1)) {return false;}
    } else {
        if (!(x1<=x&&x<=x2)) {return false;}
    }
    if (y1>=y2) {
        if (!(y2<=y&&y<=y1)) {return false;}
    } else {
        if (!(y1<=y&&y<=y2)) {return false;}
    }
    if (x3>=x4) {
        if (!(x4<=x&&x<=x3)) {return false;}
    } else {
        if (!(x3<=x&&x<=x4)) {return false;}
    }
    if (y3>=y4) {
        if (!(y4<=y&&y<=y3)) {return false;}
    } else {
        if (!(y3<=y&&y<=y4)) {return false;}
    }
}
return true;
    
```

### <a name="jsVectors_mirrorVector"></a>jsVectors::mirrorVector(v1, along, base)


```javascript

// the direction tangent and normal are normalized and the vector is projected into it            
tn1.x = along.x - base.x;   
tn1.y = along.y - base.y;
nv1.x = -tn1.y;
nv1.y = tn1.x;

v1.x = v1.x - base.x;
v1.y = v1.y - base.y;

// if the 'j' or normal projection is positive, turn around
if( this.dotProd(v1,nv1) > 0) 
    this.rotate(nv1, Math.PI);        

this.normalize(tn1);
this.normalize(nv1);

// Create positive coordinates of the projection of the vector to the 'base' cordinates
var nvProd = Math.abs( this.dotProd(v1,nv1) );
//             tnProd = Math.abs( this.dotProd(v1,tn1) );
    
var tnProd = this.dotProd(v1,tn1);
// then, project the length of the base vectors to get the new vector space
v1.x = nv1.x * nvProd + tn1.x *tnProd,
v1.y = nv1.y * nvProd + tn1.y *tnProd;   

v1.x += base.x;
v1.y += base.y;

return v1;        
    
```

### <a name="jsVectors_normalize"></a>jsVectors::normalize(v)


```javascript

var len = Math.sqrt( v.x*v.x + v.y*v.y);

if(len==0) {
    throw "Error normalizing vector: the length of the vector was zero";
}

v.x = v.x/len;
v.y = v.y/len;
return v;
    
```

### <a name="jsVectors_opposeVector"></a>jsVectors::opposeVector(v1, along)


```javascript


// the direction tangent and normal are normalized and the vector is projected into it            
tn1.x = along,x;   
tn1.y = along.y;
nv1.x = -tn1.y;
nv1.y = tn1.x;

this.normalize(tn1);
this.normalize(nv1);

// Important: turn the tangent to opposing direction...
this.rotate(tn1, Math.PI);

// Create the projection of the vector to the 'base' cordinates
var nvProd = Math.abs( jsMath.dotProd(v1,nv1) ),
    tnProd = Math.abs( jsMath.dotProd(v1,tn1) );
    
// if the 'j' or normal projection is negative, turn around
if( this.dotProd(v1,nv1) < 0) 
    this.rotate(nv1, Math.PI);
    
// then, project the length of the vector to get the new vector
v1.x = nv1.x * nvProd + tn1.x *tnProd,
v1.y = nv1.y * nvProd + tn1.y *tnProd;        

return v1;
    
```

### <a name="jsVectors_pointInTriangle"></a>jsVectors::pointInTriangle(p, p0, p1, p2)


```javascript


var A = 1/2 * (-p1.y * p2.x + p0.y * (-p1.x + p2.x) + p0.x * (p1.y - p2.y) + p1.x * p2.y);
var sign = A < 0 ? -1 : 1;
var s = (p0.y * p2.x - p0.x * p2.y + (p2.y - p0.y) * p.x + (p0.x - p2.x) * p.y) * sign;
var t = (p0.x * p1.y - p0.y * p1.x + (p0.y - p1.y) * p.x + (p1.x - p0.x) * p.y) * sign;

return s > 0 && t > 0 && (s + t) < 2 * A * sign;
        
    
```

### <a name="jsVectors_pointInTriangleBc"></a>jsVectors::pointInTriangleBc(p, bb)


```javascript

var A = bb.A;
var sign = bb.sign;
var s = (bb.s1 +  bb.s2 * p.x + bb.s3 * p.y);
var t = (bb.t1 +  bb.t2 * p.x + bb.t3 * p.y);

return s > 0 && t > 0 && (s + t) < 2 * A * sign;
        
    
```

### <a name="jsVectors_project"></a>jsVectors::project(vectorToProject)


```javascript


var p = vectorToProject;

pVector.x = p.x - pBase.x;
pVector.y = p.y - pBase.y;

prodResult.i = this.dotProd( pVector, iVect);
prodResult.j = this.dotProd( pVector, jVect);

return prodResult;

```

### <a name="jsVectors_rotate"></a>jsVectors::rotate(v, angle)


```javascript


var s = Math.sin(angle);
var c = Math.cos(angle);

var x = v.x,
    y = v.y;

v.x = x * c + y * s;
v.y = -x * s + y * c;

return v;
    
```

### <a name="jsVectors_rotateAround"></a>jsVectors::rotateAround(angle, v, around)


```javascript

this.sub(v, around);
this.rotate(v,angle);
this.add(v,around);
    
```

### <a name="jsVectors_sub"></a>jsVectors::sub(v1, v2)


```javascript

v1.x = v1.x - v2.x;
v1.y = v1.y - v2.y;
    
```

### <a name="jsVectors_tangentNormal"></a>jsVectors::tangentNormal(v1, v2, v3)


```javascript


var t1 = {};
t1.x = v2.x - v1.x;
t1.y = v2.y - v1.y;
var t2 = {};
t2.x = v3.x - v2.x;
t2.y = v3.y - v2.y;

var p = { x : t1.x+t2.x,
          y : t1.y+t2.y
        };
return this.normalize(p);
    
```

### <a name="jsVectors_triangleArea"></a>jsVectors::triangleArea(A, B, C)


```javascript

        
var area = A.x * ( B.y - C.y ) +
           B.x * ( C.y - A.y ) +
           C.x * ( A.y - B.y );
        
return Math.abs( area / 2);        
    
```

### <a name="jsVectors_triangleInTriangle"></a>jsVectors::triangleInTriangle(p0, p1, p2, q0, q1, q2)


```javascript

        
var bb = this.getBarCoeffs(p0,p1,p2);

if(this.pointInTriangleBc( q0, bb) ) return true;
if(this.pointInTriangleBc( q1, bb) ) return true;
if(this.pointInTriangleBc( q2, bb) ) return true;

var bb = this.getBarCoeffs(q0, q1, q2 );

if(this.pointInTriangleBc( p0, bb) ) return true;
if(this.pointInTriangleBc( p1, bb) ) return true;
if(this.pointInTriangleBc( p2, bb) ) return true;


if(this.linesIntersect( p0,p1, q0,q1)) return true;
if(this.linesIntersect( p1,p2, q0,q1)) return true;
if(this.linesIntersect( p2,p0, q0,q1)) return true;

if(this.linesIntersect( p0,p1, q1,q2)) return true;
if(this.linesIntersect( p1,p2, q1,q2)) return true;
if(this.linesIntersect( p2,p0, q1,q2)) return true;        

if(this.linesIntersect( p0,p1, q2,q0)) return true;
if(this.linesIntersect( p1,p2, q2,q0)) return true;
if(this.linesIntersect( p2,p0, q2,q0)) return true;             

return false;
    
```

### <a name="jsVectors_unProject"></a>jsVectors::unProject(projectedVector)


```javascript

var p = projectedVector;
deVector.x = p.i * iVect.x + p.j * jVect.x;
deVector.y = p.i * iVect.y + p.j * jVect.y;

deVector.x += pBase.x;
deVector.y += pBase.y;
return deVector;
   
```



   


   



      
    



      
    




