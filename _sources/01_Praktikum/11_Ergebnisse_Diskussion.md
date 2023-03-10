# Ergebnisse und Diskussion

Temperaturen im gesamten Modell

![Abbildungen/Temperatur_Modell.png](Abbildungen/Temperatur_Modell.png)

Temperaturverlauf und Wärmeströmdichte entland des Pfades.

![Abbildungen/Ergebnis_Pfad.png](Abbildungen/Ergebnis_Pfad.png)

## Diskussion

Im stationären Fall kann die Wärmeleitung bei einem definierten Temperaturgradienten zwischen dem Anfangs- und Endpunkt wie folgt beschrieben werden:

````{margin}
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
````

```{math}
:label: waermestromdichte
\dot{q}=\frac{\lambda}{{\Delta L}}(T_E - T_A)
```

Über die bekannten Temperaturen der Stirnflächen kann die Wärmestromdichte für das Modell berechnet werden:

$$
\begin{align}
\dot q & =\frac{60,5\,\mathrm{W}}{0{,}1\,\mathrm{m} \, \mathrm{m} \, \mathrm{K}}\mathrm{(100-20)\,K} \\
\dot q & =48.400\,\mathrm{\frac{W}{m^2}}
\end{align}
$$

Durch Umstellung der Gleichung {eq}`waermestromdichte` kann nach dem linearen Zusammenhang die Temperatur an jedem Punkt zwischen den beiden Stirnseiten ermittelt werden:

```{math}
:label: endtemperatur_diskussion
T_E=\frac{{\Delta L}}{\lambda}\,\dot q+T_A
```

![Abbildungen/Analytisch.png](Abbildungen/Analytisch.png)

Die numerischen Ergebnisse der FEM sind mit der analytischen Gleichung identisch.
