# Finite-Elemente Methode

## Anwendungsfälle

Mit Hilfe der Finite-Elemente Methode (FEM) können wir Temperaturfeldberechnung in Festkörpern für den **stationären** und **instationären Fall** berechnen. Schauen wir uns dafür zunächst ein einfaches Beispiel analytisch an und vergleichen es mit einer FEM Simulation

## Beispiel 1: Wärmeleitung durch eine Wand

Mit der folgenden analytischen Gleichung können wir die Wärmeleitung in einer Wand berechnen:

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
			var deltaL = board0.create('slider', [[0.1, 0.6], [0.6, 0.6], [0.1, 0.1, 0.8]], {name:'deltaL', snapWidth: 0.02, postLabel: ' m'});
			var lambda_max = 200
			var lambda = board0.create('slider', [[0.1, 0.4], [0.6, 0.4], [10, 60.5, lambda_max]], {name:'lambda', snapWidth: 10, postLabel: 'W/mK'});
			var qdot_max = 100000
			var qdot = board0.create('slider', [[0.1, 0.2], [0.6, 0.2], [10000, 48400, qdot_max]], {name:'qdot', snapWidth: 1000, postLabel: 'W/m^2'});

			var p1 = board.create('point',[0,0], {name:'A', size:4, fixed:true, visible:false});
			var p2 = board.create('point',[0,110], {name:'B', size:4, fixed:true, visible:false});
			var p3 = board.create('point',[function(){return deltaL.Value();},110], {name:'C', size:4, fixed:true, visible:false});
			var p4 = board.create('point',[function(){return deltaL.Value();},0], {name:'D', size:4, fixed:true, visible:false});
			var poly = board.create('polygon',["A","B","C","D"], {
				fillColor:"#AAAAAA" , 
				fillOpacity: function(){return lambda.Value()/lambda_max;},
				borders:{strokeColor:'black'}});
			
			var p5 = board.create('point', [0, 55], {visible:false});
			var p6 = board.create('point', [function(){return deltaL.Value();}, 55], {visible:false});
			var arrow1 = board.create('arrow', [p5, p6], {
				strokeWidth:function(){return 3*qdot.Value()/qdot_max+1;}, 
				strokeColor:'red', label:{label: 'test', autoPosition: false, offset:[10, 0], position: 'rt'}
			},
			);
			arrow1.setLabel('Wärmestrom')
			arrow1.labelColor('red')
			
	
			
			var graph = board.create('functiongraph', [function(x){return qdot.Value()*x/lambda.Value()+TA.Value();}, 0, function(){return deltaL.Value();}],   {name:'Temperaturverlauf', withLabel:false, strokeColor:'black', strokeWidth: 3});
			

			var t1 = board.create('text',[0, -1,function(){return 'T_E='+(qdot.Value()*deltaL.Value()/lambda.Value()+TA.Value()).toFixed(1)+'°C';}], {
				anchor: p3, 
				anchorY: 'top',
				anchorX: 'left'});

			
			var reset = board0.create('button',[-0.05, 0.5,'Reset', function(){
				TA.setValue(20),
				deltaL.setValue(0.1),
				lambda.setValue(60.5),
				qdot.setValue(48400)
			}]);
    </script>
  </body>
</html>
<br>

### Umsetzung in FEM

**Um dies in der FEM zu lösen brauchen wir folgenden Informationen:**

1. Materialparameter:

- $\lambda$ (Wärmeleitfähigkeit)

2. Geometrie:

- $\Delta L$ (Dicke der Wand)

3. Randbedingungen:

- $\dot{q}$ (Wärmestromdichte)
- $T_A$ (Temperatur auf der Innenseite)

**Was können wir nun mit der FEM bestimmen:**

- Temperaturverlauf innerhalb der Wand und damit auch die Temperatur auf der Aussenseite ($T_E$)

.. Bild FEM

### Veränderung der Wandgeometrie

In der FEM können wir nun die Geometrie der Wand mit einem weiteren Material ergänzen und somit deutlich komplizierte Fälle relativ schnell berechnen:

.. Bild FEM

## Beispiel 2: Scheibenbremse

Nun erhöhen wir die Komplexität und betrachten die Temperaturverteilung beim Bremsvorgang mit einer Scheibenbremse beim Fahrrad.

Die Wärmestromdichte im Abstand $r$ von der Drehachse für die Zeit $t$ kann nach {cite}`comsol_multiphysics_43a_heat_nodate` dabei wie folge berechnet werden:

```{math}
:label: waermestromdichte_scheibenbremse
\dot{q}(r, t)=-\frac{m R^2 \alpha}{8 r_{\mathrm{m}} A} r\left(\omega_0+\alpha t\right)
```

```{list-table}
* - $\alpha$
  - Winkelbeschleunigung [$\mathrm{rad/s^2}$]
* - $\omega_0$
  - initiale Winkelgeschwindigkeit [$\mathrm{rad/s}$]
* - $A$
  - Fläche des Bremsbelags  [$\mathrm{m^2}$]
* - $m$
  - Masse des zu bremsenden Körpers [$\mathrm{kg}$]
* - $R$
  - Radius des Rades [$\mathrm{m}$]
* - $r_m$
  - Abstand Achse Scheibenbremse bis Mitte Bremsbelag  [$\mathrm{m}$]
* - $t$
  - Zeit [$\mathrm{s}$]
* - $\dot{q}$
  - Wärmestromdichte [$\mathrm{W/m^2}$]
```

**Literaturverzeichnis**

```{bibliography}

```
