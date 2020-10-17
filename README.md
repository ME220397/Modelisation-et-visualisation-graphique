
## Polygones planaires et simple-convexes

### 1. Vecteurs: produit scalaire, produit vectoriel


```python
matrice_de_vecteurs = matrix([[3, 0, 4, 0]])
matrice_de_vecteurs = matrice_de_vecteurs.transpose()
matrice_de_vecteurs
```




    [3]
    [0]
    [4]
    [0]




```python
vecteur_u = matrice_de_vecteurs.column(0)
vecteur_u
```




    (3, 0, 4, 0)




```python
def norme(u):
    return norm(u)

def vecteur_unitaire(u):
    return u/norm(u)

def produit_scalaire(u,v):
    return u.dot_product(v)

def cosinus_angle_forme_par(u,v):
    return produit_scalaire(u,v)/(norme(u)*norme(v))

def produit_vectoriel(u,v):
    uXv = u[0:3].cross_product(v[0:3])
    uXv = vector([uXv[0],uXv[1],uXv[2],0])
    return uXv
```

Exemple: Avec les vecteurs suivant: $u = \left(\begin{array}{c}3\\0\\4\\0\end{array}\right)$
y $v = \left(\begin{array}{c}2\\4\\-4\\0\end{array}\right)$, se pide:

a) Calculer la norme de chaque vecteur

b) Calculer le produit scalaire et le cosinus de l'angle formé

c) Calculer le vecteur unitaire perpendiculaire à u et v.


```python
vecteurs = matrix([[3, 0, 4, 0],[2, 4, -4, 0]])
vecteurs = vecteurs.transpose()
vecteurs
```




    [ 3  2]
    [ 0  4]
    [ 4 -4]
    [ 0  0]




```python
u = vecteurs.column(0)
u
```




    (3, 0, 4, 0)




```python
v = vecteurs.column(1)
v
```




    (2, 4, -4, 0)




```python
norme_u = norme(u)
norme_u
```




    5




```python
norme_v = norme(v)
norme_v
```




    6




```python
prod_scalaire_u_v = produit_scalaire(u,v)
prod_scalaire_u_v
```




    -10




```python
cos = cosinus_angle_forme_par(u,v)
cos
```




    -1/3




```python
produit_vect_u_v = produit_vectoriel(u,v)
produit_vect_u_v
```




    (-16, 20, 12, 0)




```python
vec_perpend = vecteur_unitaire(produit_vect_u_v)
vec_perpend
```




    (-2/5*sqrt(2), 1/2*sqrt(2), 3/10*sqrt(2), 0)



### 2. Matrices


```python
A = matrix([[1,2],[3,4]])
A
```




    [1 2]
    [3 4]




```python
B = matrix([[2,1],[1,-1]])
B
```




    [ 2  1]
    [ 1 -1]




```python
A+B
```




    [3 3]
    [4 3]




```python
A*B
```




    [ 4 -1]
    [10 -1]




```python
2*A
```




    [2 4]
    [6 8]




```python
A.transpose()
```




    [1 3]
    [2 4]




```python
A.det()
```




    -2




```python
A.inverse()
```




    [  -2    1]
    [ 3/2 -1/2]



### 3. Affichage de points, lignes et polygones


```python
pts = matrix([[0,0,0,1],[1,1,1,1]])
pts = pts.transpose()
pts
```




    [0 1]
    [0 1]
    [0 1]
    [1 1]




```python
origin = pts.column(0)
origin = origin[0:3]
origin
```




    (0, 0, 0)




```python
P = pts.column(1)
P = P[0:3]
P
```




    (1, 1, 1)




```python
u = P - origin
show(u/sqrt(3))
show(norme(u))
u = vecteur_unitaire(u)
u
```


<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\left(\frac{1}{3} \, \sqrt{3},\,\frac{1}{3} \, \sqrt{3},\,\frac{1}{3} \, \sqrt{3}\right)</script></html>



<html><script type="math/tex; mode=display">\newcommand{\Bold}[1]{\mathbf{#1}}\sqrt{3}</script></html>





    (1/3*sqrt(3), 1/3*sqrt(3), 1/3*sqrt(3))




```python
graphe = points(origin, color='red',size=20) + points(P, color='green',size=30) + points(u, color='blue', size=30) + line3d([origin,P], color='yellow',thickness=5)
graphe
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:1.0, &quot;y&quot;:1.0, &quot;z&quot;:1.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [{&quot;opacity&quot;: 1.0, &quot;color&quot;: &quot;#ff0000&quot;, &quot;size&quot;: 20.0, &quot;point&quot;: [0.0, 0.0, 0.0]}, {&quot;opacity&quot;: 1.0, &quot;color&quot;: &quot;#008000&quot;, &quot;size&quot;: 30.0, &quot;point&quot;: [1.0, 1.0, 1.0]}, {&quot;opacity&quot;: 1.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;size&quot;: 30.0, &quot;point&quot;: [0.5773502691896257, 0.5773502691896257, 0.5773502691896257]}];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [{&quot;opacity&quot;: 1.0, &quot;color&quot;: &quot;#ffff00&quot;, &quot;linewidth&quot;: 5.0, &quot;points&quot;: [[0.0, 0.0, 0.0], [1.0, 1.0, 1.0]]}];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>





```python
V = matrix([[0,0,0,1],[2,0,0,1],[1,2,0,1]])
V = V.transpose()
V
```




    [0 2 1]
    [0 0 2]
    [0 0 0]
    [1 1 1]




```python
V[0:3] #coords cartesiennes
```




    [0 2 1]
    [0 0 2]
    [0 0 0]




```python
tuple(V[0:3].transpose())
```




    ((0, 0, 0), (2, 0, 0), (1, 2, 0))




```python
P1 = polygon(tuple(V[0:3].transpose()))
P1
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:2.0, &quot;y&quot;:2.0, &quot;z&quot;:0.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 2.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}], &quot;faces&quot;: [[0, 1, 2]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>





```python
P1.set_texture(color='green')
P1
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:2.0, &quot;y&quot;:2.0, &quot;z&quot;:0.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#008000&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 2.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}], &quot;faces&quot;: [[0, 1, 2]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>





```python
def afficher_polygone(V):
    return polygon(tuple(V[0:3].transpose()))
```


```python
V2 = matrix([[0,0,0,1],[1,2,0,1],[1,2,2,1]])
V2 = V2.transpose()
P2 = afficher_polygone(V2)
P2.set_texture(color='magenta')
P2
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:1.0, &quot;y&quot;:2.0, &quot;z&quot;:2.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#ff00ff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}], &quot;faces&quot;: [[0, 1, 2]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>





```python
P1 + P2
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:2.0, &quot;y&quot;:2.0, &quot;z&quot;:2.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#008000&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 2.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}], &quot;faces&quot;: [[0, 1, 2]]}, {&quot;color&quot;: &quot;#ff00ff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}], &quot;faces&quot;: [[0, 1, 2]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>




### 4. Mallaige polygonal


```python
def afficher_mallaige_polygonal(V,F):
    P = 0
    for f in F:
        sommets = []
        for n in f:
            if n > -1:
                sommets.append(V.column(n)[0:3])
                sommets
        P = P + polygon(sommets)
    return P
```

EXEMPLE:


```python
V = matrix([[1,0,0,1],[1,3,0,1],[1,3,1,1],[1,2,1,1],[1,1,2,1],[1,0,2,1],[0,0,0,1],[0,3,0,1],[0,3,1,1],[0,2,1,1],[0,1,2,1],[0,0,2,1]])
V = V.transpose()
V
```




    [1 1 1 1 1 1 0 0 0 0 0 0]
    [0 3 3 2 1 0 0 3 3 2 1 0]
    [0 0 1 1 2 2 0 0 1 1 2 2]
    [1 1 1 1 1 1 1 1 1 1 1 1]




```python
F = matrix([[0,1,2,3,4,5],[6,11,10,9,8,7],[0,6,7,1,-1,-1],[0,5,11,6,-1,-1],[1,7,8,2,-1,-1],[2,8,9,3,-1,-1],[3,9,10,4,-1,-1],[4,10,11,5,-1,-1]])
F
```




    [ 0  1  2  3  4  5]
    [ 6 11 10  9  8  7]
    [ 0  6  7  1 -1 -1]
    [ 0  5 11  6 -1 -1]
    [ 1  7  8  2 -1 -1]
    [ 2  8  9  3 -1 -1]
    [ 3  9 10  4 -1 -1]
    [ 4 10 11  5 -1 -1]




```python
mesh = afficher_mallaige_polygonal(V,F)
mesh.set_texture(color='cyan')
mesh
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:1.0, &quot;y&quot;:3.0, &quot;z&quot;:2.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}], &quot;faces&quot;: [[0, 1, 2, 3, 4, 5]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 0.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}], &quot;faces&quot;: [[0, 1, 2, 3, 4, 5]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 3.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 3.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 2.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 0.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}, {&quot;color&quot;: &quot;#00ffff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 1.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 0.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 2.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 2.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>




### 4.1. Maillage polygonal consistant: polygone planaire


```python
def transformation_de_coordonnees(V):

    V1 = V.column(0)
    V2 = V.column(1)
    Vn = V.column(-1)
    up = V2-V1
    vp = Vn-V1
    upXvp = produit_vectoriel(up,vp)     # vecteur w = u x v

    u = vecteur_unitaire(up)                   # vecteur u normalisé
    w = vecteur_unitaire(upXvp)            # vecteur w = u x v normalisé
    v = produit_vectoriel(w,u)               # vecteur v = w x u

    a = produit_scalaire(V1,u)
    b = produit_scalaire(V1,v)
    c = produit_scalaire(V1,w)

    return matrix([[u[0],u[1],u[2],-a],[v[0],v[1],v[2],-b],[w[0],w[1],w[2],-c],[0,0,0,1]])
```


```python
def est_planaire(V):

    Vt = transformation_de_coordonnees(V)*V     # sommets transformés
    if Vt[2]==0:                                # si la troisieme ligne est null -> planaire
        print('Le polygone est planaire')
        return True
    else:
        print('Polygone non planaire')
        return False
```

EXEMPLE: $V=\left(\begin{array}{cccc}1 & 1 & 2& 2\\ 2 &0& 1& 3\\ 3& 1&1 &3\\ 1& 1& 1& 1\end{array}\right)$.


```python
V = matrix([[1,2,3,1],[1,0,1,1],[2,1,1,1],[2,3,3,1]])
V = V.transpose()
V
```




    [1 1 2 2]
    [2 0 1 3]
    [3 1 1 3]
    [1 1 1 1]




```python
est_planaire(V)
```

    Le polygone est planaire





    True




```python
afficher_polygone(V)
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:1.0, &quot;y&quot;:0.0, &quot;z&quot;:1.0}, {&quot;x&quot;:2.0, &quot;y&quot;:3.0, &quot;z&quot;:3.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 2.0, &quot;x&quot;: 1.0, &quot;z&quot;: 3.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 2.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 3.0, &quot;x&quot;: 2.0, &quot;z&quot;: 3.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>




EXEMPLE: $V=\left(\begin{array}{cccc}1 & 0 & 0& 0\\ 0 &1& 1& 0\\ 0& 0&1 &1\\ 1& 1& 1& 1\end{array}\right)$.


```python
V2 = matrix([[1,0,0,1],[0,1,0,1],[0,1,1,1],[0,0,1,1]])
V2 = V2.transpose()
V2
```




    [1 0 0 0]
    [0 1 1 0]
    [0 0 1 1]
    [1 1 1 1]




```python
est_planaire(V2)
```

    Polygone non planaire





    False




```python
afficher_polygone(V2)
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:0.0, &quot;z&quot;:0.0}, {&quot;x&quot;:1.0, &quot;y&quot;:1.0, &quot;z&quot;:1.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 1.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 0.0, &quot;z&quot;: 0.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>




### 4.2. Maillage polygonal consistant: polygones simple-convexe


```python
def equations_implicites(V2D):
    
    #Input:  V2D = Matrices de sommets par colonnes et coords homogènes 2D.
    #Output: Lista avec pour chaque ligne l'equation Ax+By+C=0.
    
    M = matrix(V2D.ncols(),3)       
    
    for i in range(V2D.ncols()-1):
        P = V2D.column(i)
        Q = V2D.column(i+1)
        v = Q - P                    
        M[i] = [-v[1], v[0], -(-v[1]*P[0]+v[0]*P[1])]
        
    # La derniere equation du dernier sommets au premier
    P = V2D.column(V2D.ncols()-1)
    Q = V2D.column(0)
    v = Q - P
    M[V2D.ncols()-1] = [-v[1], v[0], -(-v[1]*P[0]+v[0]*P[1])]
    
    return M
```

EXEMPLE:  $V=\left(\begin{array}{cccc}0 & 0 & 3& 4\\ 0 &-2& 1& 0\\ 1& 1& 1& 1\end{array}\right)$.



```python
V2D = matrix([[0,0,1],[0,-2,1],[3,1,1],[4,0,1]])
V2D = V2D.transpose()
V2D
```




    [ 0  0  3  4]
    [ 0 -2  1  0]
    [ 1  1  1  1]




```python
M = equations_implicites(V2D)
M
```




    [ 2  0  0]
    [-3  3  6]
    [ 1  1 -4]
    [ 0 -4  0]




```python
def est_simple_convexe(V2D):
    
    b = 1
    M = equations_implicites(V2D)
    
    for i in range(M.nrows()):
        signes = []
        for j in range(V2D.ncols()):
            signes.append(sign(produit_scalaire(M[i],V2D.column(j))))
        x = signes.count(1)
        y = signes.count(-1)
        if not(x==V2D.ncols()-2) and not(y==V2D.ncols()-2):
            b = 0
            
    if b==0:
        print('Polygone non simple-convexe')
    else:
        print('Polygone simple-convexe')    
    return b
```


```python
est_simple_convexe(V2D)
```

    Polygone non simple-convexe





    0




```python
afficher_polygone(V2D)
```





<iframe srcdoc="<!DOCTYPE html>
<html>
<head>
<title></title>
<meta charset=&quot;utf-8&quot;>
<meta name=viewport content=&quot;width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0&quot;>
<style>

    body { margin: 0px; overflow: hidden; }

    #menu-container { position: absolute; bottom: 30px; right: 40px; cursor: default; }

    #menu-message { position: absolute; bottom: 0px; right: 0px; white-space: nowrap;
                    display: none; background-color: #F5F5F5; padding: 10px; }

    #menu-content { position: absolute; bottom: 0px; right: 0px;
                    display: none; background-color: #F5F5F5; border-bottom: 1px solid black;
                    border-right: 1px solid black; border-left: 1px solid black; }

    #menu-content div { border-top: 1px solid black; padding: 10px; white-space: nowrap; }

    #menu-content div:hover { background-color: #FEFEFE;; }
  
</style>
</head>

<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script src=&quot;/nbextensions/threejs/examples/js/controls/OrbitControls.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/build/three.min.js&quot;><\/script> \
<script src=&quot;https://cdn.jsdelivr.net/gh/mrdoob/three.js@r110/examples/js/controls/OrbitControls.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;projection&quot;: &quot;perspective&quot;, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;frame&quot;: true, &quot;axes&quot;: false, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;decimals&quot;: 2};

    // When animations are supported by the viewer, the value 'false'
    // will be replaced with an option set in Python by the user
    var animate = false; // options.animate;

    var b = [{&quot;x&quot;:0.0, &quot;y&quot;:-2.0, &quot;z&quot;:1.0}, {&quot;x&quot;:4.0, &quot;y&quot;:1.0, &quot;z&quot;:1.0}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontsize=14  ) {

        var canvas = document.createElement( 'canvas' );
        var pixelRatio = Math.round( window.devicePixelRatio );
        canvas.width = 128 * pixelRatio;
        canvas.height = 32 * pixelRatio; // powers of two
        canvas.style.width = '128px';
        canvas.style.height = '32px';

        var context = canvas.getContext( '2d' );
        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = fontsize + 'px monospace';
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, canvas.width/2/pixelRatio, canvas.height/2/pixelRatio );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( { map: texture } ) );
        sprite.position.set( x, y, z );

        // Set the initial scale based on plot size to accomodate orthographic projection.
        // For other projections, the scale will get reset each frame based on camera distance.
        var scale = midToCorner/2;
        sprite.scale.set( scale, scale*.25, 1 ); // ratio of canvas width to height

        scene.add( sprite );

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*(xMid+xRange), a[1]*(yMid+yRange), a[2]*(zMid+zRange) );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {
        
        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();
        
    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ )
        addLabel( texts[i].text, a[0]*texts[i].x, a[1]*texts[i].y, a[2]*texts[i].z, texts[i].color );

    var points = [];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var lines = [];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        scene.add( mesh );

    }

    var surfaces = [{&quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;vertices&quot;: [{&quot;y&quot;: 0.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: -2.0, &quot;x&quot;: 0.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 1.0, &quot;x&quot;: 3.0, &quot;z&quot;: 1.0}, {&quot;y&quot;: 0.0, &quot;x&quot;: 4.0, &quot;z&quot;: 1.0}], &quot;faces&quot;: [[0, 1, 2, 3]]}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: json.useFlatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            scene.add( mesh );

        }

    }

    var scratch = new THREE.Vector3();

    function render() {

        if ( animate ) requestAnimationFrame( render );
        renderer.render( scene, camera );

        // Resize text based on distance from camera.
        // Not neccessary for orthographic due to the nature of the projection (preserves sizes).
        if ( !camera.isOrthographicCamera ) {
            for ( var i=0 ; i < scene.children.length ; i++ ) {
                if ( scene.children[i].type === 'Sprite' ) {
                    var sprite = scene.children[i];
                    var adjust = scratch.addVectors( sprite.position, scene.position )
                                    .sub( camera.position ).length() / 5;
                    sprite.scale.set( adjust, .25*adjust, 1 ); // ratio of canvas width to height
                }
            }
        }
    }
    
    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>

</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>




### 4.3. Mallaige polygonal consistant: Formule de Euler-Poincaré


```python
def aretes(F):
    
    A = []
    for f in F:
        n = 0
        for j in range(f.length()):
            if f[j]>-1:
                n = n+1
        f = f[0:n]
        i = 0
        while i < f.length()-1:
            if [f[i],f[i+1]] not in A and [f[i+1],f[i]] not in A:
                A.append([f[i],f[i+1]])
                i = i+1
            else:
                i = i+1
        if [f[f.length()-1],f[0]] not in A and [f[0],f[f.length()-1]] not in A:
            A.append([f[f.length()-1],f[0]])
            
    return A
```

EXEMPLES:


```python
F = matrix([[1,2,3,4],[2,3,5,6]])
F
```




    [1 2 3 4]
    [2 3 5 6]




```python
aretes(F)
```




    [[1, 2], [2, 3], [3, 4], [4, 1], [3, 5], [5, 6], [6, 2]]




```python
F2 = matrix([[0,3,2,1],[1,2,6,5],[0,4,7,3],[0,1,5,4],[2,3,7,6]])
F2
```




    [0 3 2 1]
    [1 2 6 5]
    [0 4 7 3]
    [0 1 5 4]
    [2 3 7 6]




```python
aretes(F2)
```




    [[0, 3],
     [3, 2],
     [2, 1],
     [1, 0],
     [2, 6],
     [6, 5],
     [5, 1],
     [0, 4],
     [4, 7],
     [7, 3],
     [5, 4],
     [7, 6]]




```python
F3 = matrix([[0,1,2,3,4,5],[6,11,10,9,8,7],[0,6,7,1,-1,-1],[0,5,11,6,-1,-1],[1,7,8,2,-1,-1],[2,8,9,3,-1,-1],[3,9,10,4,-1,-1],[4,10,11,5,-1,-1]])
F3
```




    [ 0  1  2  3  4  5]
    [ 6 11 10  9  8  7]
    [ 0  6  7  1 -1 -1]
    [ 0  5 11  6 -1 -1]
    [ 1  7  8  2 -1 -1]
    [ 2  8  9  3 -1 -1]
    [ 3  9 10  4 -1 -1]
    [ 4 10 11  5 -1 -1]




```python
aretes(F3)
```




    [[0, 1],
     [1, 2],
     [2, 3],
     [3, 4],
     [4, 5],
     [5, 0],
     [6, 11],
     [11, 10],
     [10, 9],
     [9, 8],
     [8, 7],
     [7, 6],
     [0, 6],
     [7, 1],
     [5, 11],
     [8, 2],
     [9, 3],
     [10, 4]]




```python
def euler_poincare(V,F,g):
    
    num_sommets = V.ncols()
    num_faces = F.nrows()
    num_aretes = len(aretes(F))  
    
    print ('Nombre de sommets:')
    print (num_sommets)
    print ('Nombre de aretes:') 
    print (num_aretes)
    print ('Nombre de faces:') 
    print (num_faces)
    
    if num_sommets-num_aretes+num_faces==2*(1-g):        
        print('Formule de Euler-Poincaré -> correct')
        return True
    else:        
        print('Formule de Euler-Poincaré -> incorrect')
        return False
```

EXEMPLE: 


```python
V = matrix([[2,-2,-2,1],[2,2,-2,1],[-2,2,-2,1],[-2,-2,-2,1],[2,-2,2,1],[2,2,2,1],[-2,2,2,1],[-2,-2,2,1]])
V = V.transpose()
V
```




    [ 2  2 -2 -2  2  2 -2 -2]
    [-2  2  2 -2 -2  2  2 -2]
    [-2 -2 -2 -2  2  2  2  2]
    [ 1  1  1  1  1  1  1  1]




```python
F = matrix([[0, 3, 2, 1],[4, 5, 6, 7],[2 ,6 ,5 ,1],[0, 4 ,7, 3],[0 ,1, 5,4],[3 ,7, 6 ,2]])
F
```




    [0 3 2 1]
    [4 5 6 7]
    [2 6 5 1]
    [0 4 7 3]
    [0 1 5 4]
    [3 7 6 2]




```python
euler_poincare(V,F,0)
```

    Nombre de sommets:
    8
    Nombre de aretes:
    12
    Nombre de faces:
    6
    Formule de Euler-Poincaré -> correct





    True



### 4.4. Mallaige polygonal consistant: ordres des sommets


```python
def ordre_sommets(F):
    
    L = []
    
    for f in F:
        n = 0
        for j in range(f.length()):
            if f[j]>-1:
                n = n+1
        f = f[0:n]
        
        for i in range(f.length()-1):
            if [f[i+1],f[i]] not in L:
                L.append([f[i],f[i+1]])
        if [f[0],f[f.length()-1]] not in L:
            L.append([f[f.length()-1],f[0]])     
    
    if len(L) > len(aretes(F)):
        print('ordre des sommets non consistant')
        return False
    else:
        print('ordre des sommets consistant')
        return True
```

EXEMPLE:


```python
F
```




    [0 3 2 1]
    [4 5 6 7]
    [2 6 5 1]
    [0 4 7 3]
    [0 1 5 4]
    [3 7 6 2]




```python
ordre_sommets(F)

```

    ordre des sommets consistant





    True




```python
F2
```




    [0 3 2 1]
    [1 2 6 5]
    [0 4 7 3]
    [0 1 5 4]
    [2 3 7 6]




```python
ordre_sommets(F2)
```

    ordre des sommets consistant





    True




```python
F3 = matrix([[1,2,3,4],[1,2,6,5]])
F3
```




    [1 2 3 4]
    [1 2 6 5]




```python
ordre_sommets(F3)
```

    ordre des sommets non consistant





    False


