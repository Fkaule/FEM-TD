# Vorzeigebeispiel Fall a)

Stationäre Temperaturfeldverteilung mit 1D-Änderung

Es soll mit einem einfachen Beispiel begonnen werden, das den Temperaturverlauf durch eine Wand mit verschiedenen Randbedingungen abbildet. Die Vorgehensweise die zur Lösung der Aufgabe führt wird im folgenden beschrieben.

Fügen Sie eine "Steady-State Thermal" Analyse in ANSYS Workbench 2019 R2 hinzu und erstellen Sie unter Berücksichtigung der gegebenen Geometrien, Materialien und Randbedingungen ein Finite-Elemente Modell.

![](Abbildungen/Rastergrafik.png)

## Gegeben:

**Material**

**Baustahl**

- isotrope Wärmeleitfähigkeit
  (_Isotropic Thermal Conductivity_)

$$
\lambda=60,5 \mathrm{\frac{W}{K\,m}}
$$

**Geometrie**

**Balken mit rechteckigem Querschnitt**

- Länge (x): 0,1m
- Breite (z): 0,01m
- Höhe (y): 0,01m

  **Randbedingungen**

**Stirnseite 1**:

$$
T_1=20\mathrm{°C}
$$

**Stirnseite 2**:

Fall a) **konstante Temperatur** auf Stirnseite 2

$$
T_2=100\mathrm{°C}
$$

## Gesucht:

Bestimmten Sie den **Temperaturverlauf und die Wärmestromdichte von der Stirnseite 1 bis zur Stirnseite 2** für. Prüfen Sie die Ergebnisse auf Plausibilität z.B. durch den Abgleich mit analytischen Gleichungen.

⏹️ Fügen Sie eine neue "Steady-State Thermal" Analyse hinzu.
