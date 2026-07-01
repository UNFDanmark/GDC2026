# Cheatsheet

TODO:
- [ x ] Dag1
- [  ] Dag2 
- [ ] Dag3
- [ ] Kort cheatsheet til at bevæge sig i unity


- [Variabler](Opgave-2-Variabler.md#variables)
  - Vi bruger variabler til at opbevare data for eksempel `int health = 0;`
  - `int` erklærer typen af variablen som en hel-tals
  - `health` er variablens navn, som kan henvises til senere
  - højre-siden's værdi er hvad variablen opbevarer
- [Scoping](Opgave-2-Variabler.md#scoping)
  - Ideen om at et program's "scopes" (`{}`) specificerer hvor forskellige variabler kan leve.
- [Public](Opgave-2-Variabler.md#public)
  - Vi kan erklære en felt-variabel offentlig, hvilket gør det muligt at ændre værdien i editoren 
  - `public int speed = 100;`
- [If-Else](Opgave-3-If-s-og-input.md#if-statements)
  - If-statements bruges til at tage beslutninger i kode formen er
```c# 
if (time > doneTime) {
    print("Done");
} else {
    print("Not Done");
}
```
- [Components](Opgave-3-If-s-og-input.md#components)
  - Components er måden vi giver funktionalitet til vores objekter. Man kan finde reference til et component på et objekt med `getComponent<T>` her er `T` typen man gerne vil finde for eksempel:
  - `Rigidbody rb = GetComponent<RigidBody>();`
- [Move Input](Opgave-3-If-s-og-input.md#input)
  - For at få input fra spilleren så bruger vi Unitys InputSystem. Her laver vi først en offentlig variabel
  - `public InputAction moveAction;`
  - I editoren så tilføjer vi en `Up/Down/Left/Right Composite` til aktionen med relevante knapper til hver retning 
  - I koden så skal man huske at kalde `moveAction.enable()` ellers virker den ikke
  - Vi kan nu læse inputtet ved at kalde `moveAction.ReadValue<Vector2>();`
- [Transform Rotate](Opgave-3-If-s-og-input.md#transform-rotate)
  - For at roterer et objekt kan man bruge `Rotate` metoden som alle variabler der referer til en `Transform` kan bruge.
  - `transform.Rotate(0, 5, 0)`, roterer 5 grader om y-aksen hver gang den er kaldt.


## Funktioner

## Typer
- `Int` - heltals-værdi
- `Float` - decimaltal-værdi
- `String` - tekst-værdi
- `GameObject` - et Unity objekt, den typiske måde at referere til andre objekter i spillet
- `Transform`
  - Et Transform er et objekts position, rotation og skalering i universet af spillet.
  - Man kan altid tilgå det lokale objekts `Transform` ved bare at skrive `transform`
- `Vector3`
  - En tuple af 3 tal (x, y, z). Brugt til at repræsentere en vektor altså 
- `RigidBody`
  - Et komponent som får et objekt til at interagere med Unity's fysiksystem
- `Collider`
  - Et komponent, som fortæller fysiksystemet at rigidbody's kan kollidere med objektet

## Bevægelse i Unity

## GameView
| ---- | ----|
| Taster | Effekt|
| Ctrl+P | Start og stop spil |
| Ctrl+Shift+P | Pause spil |


### SceneView

| ---- | ---- |
| Taster | Effekt | 
| Højreklik og træk | Roterer kameraet |
| Højreklik og tryk på WASD | bevæg frem/venstre/tilbage/højre |
| Højreklik og tryk på EQ | bevæg op/ned |
| Vælg objekt i hierakiet og tryk F | Fokuser kamera på objekt |
| Hold V nede | Snapper til vertices |
| Ctrl+C | kopier valgte objekt |
| Ctrl+V | indsætter kopieret objekt |
| Ctrl+D | dupliker objekt | 
| Ctrl+Alt+F | Flytter valgte objekt til kamera position |
| Ctrl+Shift+F | Flytter valgte objekt til kamera position og rotation (brugbar til at flytte kamera) |

