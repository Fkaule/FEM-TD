# Finite-Elemente Methode

## Anwendungsfälle

- Temperaturfeldberechnung in Festkörpern für den **stationären** und **instationären Fall**

## Was wird benötigt ?

1. Materialparameter
2. Geometrie
3. Randbedingungen

```{list-table}
* - $\dot{q}$
  - Wärmestromdichte [W/m^2]
* - $\lambda$
  - Wärmeleitfähigkeit des Materials  [W/mK]
* - $\Delta L$
  - Länge des Materials  [m]
* - $T_A$
  - Anfangstemperatur des Materials [K]
* - $T_E$
  - Endtemperatur des Materials [K]
```

```{math}
:label: endtemperatur
T_E=\frac{{\Delta L}}{\lambda}\,\dot q+T_A
```

<!DOCTYPE HTML>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type">
    <link rel="stylesheet" type="text/css" href="https://jsxgraph.uni-bayreuth.de/distrib/jsxgraph.css" />
    <script src="https://cdn.jsdelivr.net/npm/jsxgraph/distrib/jsxgraphcore.js" type="text/javascript" charset="UTF-8"></script>
  </head>
  <body>

  <div id="jxgbox0" class="jxgbox" style="width:500px; height:100px;"></div>
  <div id="jxgbox" class="jxgbox" style="width:500px; height:400px;"></div>

  <script>

    const board0 = JXG.JSXGraph.initBoard('jxgbox0', {
        boundingbox: [-0.1, 1, 1, -0.1],
        axis: false,
        showCopyright:false,
        showNavigation:false
    });

    var board = JXG.JSXGraph.initBoard('jxgbox', {
      boundingbox: [-0.1, 110, 1, -5],
      axis:true,
      showCopyright:false,
      showNavigation:false,
      defaultAxes:{
        x: {
          name: 'L [m]',
          withLabel: true,
          label: {
            position: 'rt',
            offset: [-15, 20]
          }
        },
        y: {
          withLabel: true,
          name: 'T [°C]',
          label: {
            position: 'rt',
            offset: [10, -10]
          }
        }
      }
    });

    board0.addChild(board);


    var TA = board0.create('slider', [[0.1, 0.8], [0.6, 0.8], [0, 20, 50]], {name:'TA', snapWidth: 1, postLabel: ' °C'});
    var deltaL = board0.create('slider', [[0.1, 0.6], [0.6, 0.6], [0.1, 0.1, 1]], {name:'deltaL', snapWidth: 0.02, postLabel: ' m'});
    var lambda = board0.create('slider', [[0.1, 0.4], [0.6, 0.4], [10, 60.5, 200]], {name:'lambda', snapWidth: 10, postLabel: 'W/mK'});
    var qdot = board0.create('slider', [[0.1, 0.2], [0.6, 0.2], [10000, 48400, 100000]], {name:'qdot', snapWidth: 1000, postLabel: 'W/m^2'});

    var graph = board.create('functiongraph', [function(x){return qdot.Value()*x/lambda.Value()+TA.Value();}, 0, function(){return deltaL.Value();}],   {name:'T(L)', withLabel:false, strokeColor:'red'});

    var reset = board0.create('button',[-0.05, 0.5,'Reset', function(){
      TA.setValue(20),
      deltaL.setValue(0.1),
      lambda.setValue(60.5),
      qdot.setValue(48400)
    }]);
  </script>
  </body>
</html>
