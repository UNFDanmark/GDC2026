# Cheatsheet

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
- [`NavMeshSurface`](Opgave-3-Random-og-NavMesh.md#navmesh-surface)
  - Et komponent, som tillader et objekt at agere som et navigerbart området.
- [`NavMeshAgent`](Opgave-3-Random-og-NavMesh.md#navmesh-agent)
  - Et komponent, som tillader et objekt at bevæge sig på et `NavMeshSurface`.
- Arrays er en række af konstant størrelse af elementer af en specifik type, så man kan f.eks. have
  - `int[]` hvilket er en rækken af hel tals værdier.
  - `GameObject[]` hvilket er en række af `GameObjects` 

## C# Konstruktioner
- [Variabler](Opgave-2-Variabler.md#variables)
  - Vi bruger variabler til at opbevare data for eksempel <code><span class="token keyword">int</span> <span class="token plain">health</span> <span class="token operator">=</span> <span class="token number">100</span><span class="token punctuation">;</span></code>
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
  - If-statements bruges til at tage beslutninger i kode. De består af en condition, then og muligvis else blok: 
```c# 
if (time > doneTime) {
    print("Done");
} else {
    print("Not Done");
}
```
- Arrays
  - Vi kan initialisere et array på følgende måde 
  - `int[] numbers = new int[2];` - en række med to elementer
  - Vi kan tilgå det i'te element på følgende måde.
  - `numbers[0]` - her tilgår vi det første element, da arrays er 0-indekseret.

## Felt Variabler
- [`Time.deltaTime`](Opgave-1-Instantiate.md#cooldown)
  - Indeholder en `float` værdi svarende til tiden der gik imellem sidste frame og forrige frame. Bruges ofte til at lave stop-watches eller lignende
  - `cooldown -= Time.deltaTime`
- [`transform.forward`](Opgave-1-Instantiate.md#shooting-point)
  - Kan bruges til at finde den retningsvektor som transform'en peger i langs z-aksen. Tilsvarende findes der `transform.up` til y-aksen og `transform.right` til x-aksen. 
- `Vector3.up` - Konstant som altid evaluerer til en `Vector3` med værdierne `(0,1,0)`
- `Vector3.foward` - Konstant som altid evaluerer til en `Vector3` med værdierne `(0,0,1)`
- `Vector3.right` - Konstant som altid evaluerer til en `Vector3` med værdierne `(1,0,0)`

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
- [`NavMeshAgent.SetDestination`](Opgave-3-Random-og-NavMesh.md#navmesh-agent)
  - Kan bruges til at opdatere destinationen af en `NavMeshAgent`
  - `agent.SetDestination(player.position)`
- [`GameObject.FindWithTag`](Opgave-3-Random-og-NavMesh.md#findwithtag)
  - Kan bruges til at finde et `GameObject` med det tag specificeret.
  - `GameObject player = GameObject.FindWithTag("Player");`
- [`Random.Range`](Opgave-3-Random-og-NavMesh.md#random-range)
  - Kan bruges til at generere et tilfældigt tal på to forskellige måder.
  - `Random.Range(0.0f, 1.0f)` hvis argumenterne er `float`, så returneres der en værdi i intervallet udspændet af de to floats.
  - `Random.Range(1,6)` hvis argumenterne er `int`, så returneres der en heltals-værdi i intervallet `[min, max - 1]`. Altså i eksemplet så vil det være intervallet `[1,5]`
- [`Physics.Raycast`](Del-4-Raycasting.md#raycasting)
  - Raycast skyder en linje ud i rummet og fortæller om det ramte en collider på vejen. Det giver mulighed for at få en masse information.
  - `Physics.Raycast(position, direction)` returnere true eller falsk hvis den rammer noget fra start position i retningen givet.
  - `Physics.Raycast(position, direction, out RaycastHit hit)` returnere true eller falsk hvis den rammer noget og giver information om hvad der blev ramt i variablen hit. 
  - `Physics.Raycast(position, direction, out RaycastHit hit, sightDistance)` gør det samme som før, men nu rammer den kun ting som er inde for afstanden `sightDistance`
  - `Physics.Raycast(position, direction, out RaycastHit hit, sightDistance, sightMask)` gør det samme som før, men nu rammer den kun objekter, hvis lag er i `sightMask`.
- [`SceneManager.LoadScene`](Opgave-2-UI.md#reload-scene)
  - Kan bruges til at load en scene, f.eks.
  - `SceneManager.LoadScene("GameScene");` - vil begynde at load scene.



## Animation
Vi laver en `public Animator animator`. Og referer til den relevante animator i Unity editoren.

Funktioner:
- `SetFloat(id, value)` kan bruges til at sætte float værdier i animatoren, f.eks. 
  - `animator.SetFloat("Speed", rb.velocity.magnitude)` 
- `SetTrigger(id)` kan bruges til at starte en trigger, som er sand i en frame.
  - `animator.SetTrigger("Shoot")`
- `SetBool(id, value)` kan bruges til at sætte en bool, som har den valgte værdi indtil ændret. 
  - `animator.SetBool("IsGrounded", true)` 

## Lyd
Vi bruger `AudioSource` til at afspille lyd filer. Så i koden, skal vi have:
`public AudioSource audioSource`.

- `audioSource.Play()` spiller den tilknyttet lydfil, som er på sourcen lige nu.
- `audioSource.Stop()` stopper audio sourcen fra spille den nuværende lyd.
- `audioSource.PlayOneShot(audioClip)` her kan man spille en ny lydfil på et eksisterende audiosource, det gør at de settings som sourcen har (volume, pitch etc.) bliver brugt på lyden. Bemærk at at `audioSource.Stop()` ikke stopper de lyde som er spillet af `PlayOneShot`.


## Input
- [`InputAction`](Opgave-3-If-s-og-input.md#input)
  - For at få input fra spilleren bruger vi `InputAction` som gør vi kan tilgå nogle funktioner der relaterer sig til en "Action"
  - Vi definerer `public InputAction xAction;` så kommer der en action i editoren, hvor man kan definere hvilken type og hvad for nogle knapper, som skal gøre medføre aktionen.
  - Det er essentielt 
- [`Up\Down\Left\Right Composite`](Opgave-3-If-s-og-input.md#input)
  - Kan bruges til skabe en aktion der kan læse input fra to akser defineret ud fra fire forskellige input e.g. (W/S/A/D)
  - Her kan vi læse inputtet some en `Vector2` via `moveAction.ReadValue<Vector2>();`
- [`Binding`](Opgave-1-Instantiate.md#single-button-input)
  - Kan bruges til en trigger action, som kan læse inputtet fra en knap og bestemme om aktionen er i gang eller ej e.g. (mellemrum eller enter)
  - Her kan vi læse inputtet some en `bool` på to måder
    - `inputAction.IsPressed()` som returnerer `true` så længe knappen er holdt nede
    - `inputAction.WasPressedThisFrame()` som returnerer `true` den første frame 

## UI
Man kan ændre UI gennem kode på flere måder. En af dem er at bruge `GameObject.SetActive(true)` til at fjerne/vise visuelle elementer.

Hvis det er tekst man vil bruge, så anvendes `TextMeshProUGUI`. Vi vil gerne have en public reference: `public TextMeshProUGUI uiText;` så kan vi opdatere teksten på følgende måde: `uiText.text = "Ny værdi";`

## Debugging

Hvis man oplever fejl i sin kode, så kan det være nice at debugge. Her er nogle gode metoder til det.

- `print(msg)` printer en besked i konsollen kan bruges til at printe forskellige værdier, og så kan du tjekke hvad værdien er.
- `Debug.LogError(msg)` printer også i konsollen men giver 
- `void OnDrawGizmos()` er en funktion, som man kan tilføje til sine komponenter, den bliver kaldet hver gang unity-editoren vil tegne "Gizmos" som er visuelle elementer der kun eksisterer i editoren.
- `Gizmos.color = Color.red` ændrer farven på den næste Gizmo som bliver tegnet.
- `Gizmos.DrawRay(position, direction)` tegner en linje fra en start position mod en retning 

## Typiske faldgruber
Der er mange forskellige slags fejl, man kan begå når man programmere i Unity. Her er nogle typiske.
-`NullReferenceException` - betyder at man prøver at røre et objekt, som ikke eksisterer.
-`IndexOutOfRangeException` - betyder at man prøver at røre et index, som ikke eksistere i et array. f.eks. at skrive `numbers[2]` når `numbers` kun har 2 elementer. 

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

