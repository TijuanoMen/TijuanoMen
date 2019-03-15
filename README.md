<!DOCTYPE html> 
<html> 
 
<head> 
 <meta name="viewport" content="width=device-width, initial-scale=1"> 
 
 <style> 
  html, 
  body, 
  #viewport { 
   margin: 0; 
   background: #171717; 
   height: 100%; 
  } 
   
  .pjs-meta { 
   color: #fff; 
  } 
   
  canvas { 
   position: absolute; 
   top: 0; 
   left: 0; 
   right: 0; 
   bottom: 0; 
  } 
 </style> 
 
 <script src="js/physicsjs-full.js"></script> 
 
</head> 
 
<body> 
 
 <canvas id="viewport" width="500" height="500"></canvas> 
 <script> 
  Physics(function(world) 
  { 
 
   // bounds of the window 
   var renderer = Physics.renderer( 
    'canvas', 
    { 
     el: 'viewport', // id of the canvas element 
     width: 500, 
     height: 500 
    }); 
   world.add(renderer); 
 
   var circle = Physics.body( 
    'circle', 
    { 
     x: 250, 
     y: 250, 
     vx: 0.10, 
     radius: 20 
     //width: 50, 
     //height: 50 
    }); 
   world.add(circle); 
   world.render(); 
 
   Physics.util.ticker.on(function(time, dt) 
   { 
    world.step(time); 
   }); 
 
   world.on('step', function(event) 
   { 
    world.render(); 
   }); 
 
   //Let’s add some constant acceleration downwards (gravity)  
   world.add(Physics.behavior('constant-acceleration')); 
 
   var bounds = Physics.aabb(0, 0, 500, 500); 
   world.add(Physics.behavior('edge-collision-detection', 
   { 
    aabb: bounds, 
    restitution: 0.9 
   })); 
 
   // ensure objects bounce when edge collision is detected 
   world.add(Physics.behavior('body-impulse-response')); 
 
  }); 
 </script> 
</body> 
 
</html>
