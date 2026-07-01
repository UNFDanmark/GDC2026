# Cheatsheet

TODO:
- [ x ] Dag1
- [  ] Dag2 
- [ ] Dag3
- [ ] Kort cheatsheet til at bevæge sig i unity

## Typer
- `Int` - heltals-værdi
- `Float` - decimaltal-værdi
- `String` - tekst-værdi
- `GameObject` - et Unity objekt, den typiske måde at referere til andre objekter i spillet
- `Transform`
  - Et Transform er et objekts position, rotation og skalering i universet af spillet.
  - Man kan altid tilgå det lokale objekts `Transform` ved bare at skrive `transform`
- `Vector3`
  - En tuple af 3 tal (x, y, z). Brugt til at repræsentere en vektor altså en position eller retning.
- `RigidBody`
  - Et komponent som får et objekt til at interagere med Unity's fysiksystem
- `Collider`
  - Et komponent, som fortæller fysiksystemet at rigidbodys kan kollidere med objektet


## C# Konstruktioner
- [Variabler](Opgave-2-Variabler.md#variables)
  - Vi bruger variabler til at opbevare data for eksempel `int health = 0;`
  - `int` erklærer typen af variablen som en hel-tals
  - `health` er variablens navn, som kan henvises til senere
  - højre-siden's værdi er hvad variablen opbevarer
- Funktioner
  - Funktioner tager formen `Type funktionsNavn(params)`
  - Hvor `Type` er den type som et funktionskald returnere
  - `params` består af typer og navne af formen `Type paramNavn`
  - Et eksempel kunne være `int add (int a, int b)`, som tager to parametre `a` og `b` og returnere en værdi af typen `int`
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

## Felt Variabler
- [`Time.deltaTime`](Opgave-1-Instantiate.md#cooldown)
  - Indeholder en `float` værdi svarende til tiden der gik imellem sidste frame og forrige frame. Bruges ofte til at lave stop-watches eller lignende
  - `cooldown -= Time.deltaTime`
- [`transform.forward`](Opgave-1-Instantiate.md#shooting-point)
  - Kan bruges til at finde den retningsvektor som transform'en peger i langs z-aksen. Tilsvarende findes der `transform.up` til y-aksen og `transform.right` til x-aksen. 
- `Vector3.Up` - Konstant som altid evaluerer til en `Vector3` med værdierne `(0,1,0)`
- `Vector3.Foward` - Konstant som altid evaluerer til en `Vector3` med værdierne `(0,0,1)`
- `Vector3.` - Konstant som altid evaluerer til en `Vector3` med værdierne `(0,0,1)`

## Funktioner
- `void Start()` - bliver kaldet første frame hvor objektet eksisterer
- `void Update()` - bliver kaldet hver frame hvor objektet eksisterer.
- [`getComponent<T>()`](Opgave-3-If-s-og-input.md#components)
  - Components er måden vi giver funktionalitet til vores objekter. Man kan finde en  reference til et component på et objekt med `getComponent<T>` her er `T` typen man gerne vil finde for eksempel:
  - `Rigidbody rb = GetComponent<RigidBody>();`
- [`Transform.Rotate`](Opgave-3-If-s-og-input.md#transform-rotate)
  - For at roterer et objekt kan man bruge `Rotate` metoden som alle variabler der referer til en `Transform` kan bruge.
  - `transform.Rotate(0, 5, 0)`, roterer 5 grader om y-aksen hver gang den er kaldt.
- [`Instantiate`](Opgave-1-Instantiate.md#instantiate)
  -  Kan bruges til at skabe kopier af et Unity Objekt
  -  `Instantiate(obj)` spawner en kopi med samme transform som obj.
  -  `Instantiate(obj, position, rotation)` spawner en kopi med `position` og `rotation` givet
  -  `Instantiate(obj, transform)` spawner en kopi som et barn af `transform`
  -  Et kald til `Instantiate` returnere en reference til kopien, som bliver instantieret
- [`Destroy`](Opgave-2-Kollision.md#gameobject-destroy)
  - Kan bruges til at destruere objekter
  - `GameObject.Destroy(obj)` hvor `obj` er det objekt som der skal fjernes

## Input
- [`InputAction`](Opgave-3-If-s-og-input.md#input)
  - For at få input fra spilleren bruger vi `InputAction` som gør vi kan tilgå nogle funktioner der relaterer sig til en "Action"
  - Vi definerer `public InputAction xAction;` så kommer der en action i editoren, hvor man kan definere hvilken type og hvad for nogle knapper, som skal gøre medføre aktionen.
  - Det er essentielt 
- [`Up\Down\Left\Right Composite`](Opgave-3-If-s-og-input.md#input)
  - Kan bruges til skabe en aktion der kan læse input fra to akser defineret ud fra fire forskellige input e.g. (W/S/A/D)
  - Her kan vi læse inputtet some en `Vector2` via `moveAction.ReadValue<Vector2>();`
- [`Binding`](Opgave-1-Instantiate.md#single-button-input)
  - Kan bruges til en trigger action, som kan læse inputtet fra en knap og bestemme om aktionen er i gang eller ej e.g. (mellemrum, eller enter)
  - Her kan vi læses inputtet some en `bool` på to måde
    - `inputAction.IsPressed()` som returnerer `true` så længe knappen er holdt nede
    - `inputAction.WasPressedThisFrame()` som returnerer `true` den første frame 


## Bevægelse i Unity

### GameView
| ---- | ----|
| Taster | Effekt|
| Ctrl+P | Start og stop spil |
| Ctrl+Shift+P | Pause spil |
| Dobbelt Klik på "Game" | Toggle fullscreen af vinduet |

### SceneView
| ---- | ---- |
| Taster | Effekt | 
| Højreklik og træk | Roterer kameraet |
| Højreklik og tryk på WASD | bevæg frem/venstre/tilbage/højre |
| Højreklik og tryk på EQ | bevæg op/ned |
| Vælg objekt i hierarkiet og tryk F | Fokuser kamera på objekt |
| Hold V nede | Snapper til vertices |
| Ctrl+C | kopier valgte objekt |
| Ctrl+V | indsætter kopieret objekt |
| Ctrl+D | dupliker objekt | 
| Ctrl+Alt+F | Flytter valgte objekt til kameraets position |
| Ctrl+Shift+F | Flytter valgte objekt til kameraets position og rotation (brugbar til at flytte kamera) |
| Dobbelt Klik på "Scene" | Toggle fullscreen af vinduet |

