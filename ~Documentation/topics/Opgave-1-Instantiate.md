# Del 1 (Instantiate)

## Prefabs
For at kunne skyde skal vi først lave en patron vi kan skyde med. Start med at lave en sphere og skalere den ned så den er en rimelig størrelse.
For at patronen senere kan skydes afsted får den også en `Rigidbody` component. Dernæst vil vi gerne sørge for at vi
kan genbruge det patron objekt som vi lige har lavet, det gør vi nemt ved at vælge patronen og drag-and-droppe den ned i vores project-vindue.
Ved at drag-and-droppe på denne måde laver man det man kalder et *prefab*, det er en kopi med alle de samme egenskaber
som det originale objekt som kan genbruges forskellige steder.
Hvis man ændrer på egenskaberne i prefabben så ændrer det også på alle steder hvor man bruger den.

Nu hvor vi har et prefab kan vi slette den originale patron uden at at få problemer senere.

![prefab.gif](prefab.gif)

## Shooting Point

![ShootingPoint.png](ShootingPoint.png)

Tilføj et nyt tomt gameobjekt ved navn `ShootingPoint` som en child objekt til `SpillerModel`. Lav en ny script ved navn `ShootingScript` og tilføj den til
`ShootingPoint` gameobjekt.

## Instantiering
{id = "instantiate"}

Vi åbner vores `ShootingScript`. For at kunne skyde skal vi kunne lave nye objekter mens spillet kører, det gør man med funktionen [`Instantiate`](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html).
`Instantiate` skal bruge en reference til det objekt man gerne vil lave, så vi laver en `public` variabel `bulletPrefab` af typen `GameObject` som 
kan indeholde referencen. Vi kan nu drag-and-droppe vores prefab af bullet over i feltet for `Bullet Prefab`. 

![PrefabDragInspector2.gif](PrefabDragInspector2.gif)

<note>
Vær obs på at hvis I glemmer dette step så får i understående fejl. Dette er en meget almindelig fejl man ofte kommer til at møde. Den kendes blandt andet også under navnet "Null Reference".
<img src="nullref.gif" alt="Dette er et eksempel på en null reference fejl"/>
</note>

Tilbage i vores script kan vi nu i `Update`-funktionen kalde `Instantiate` med `bulletPrefab` som parameter.
```C#
void Update()
{
    Instantiate(bulletPrefab);
}

```
Hvis vi nu starter spillet kan vi se at der kommer massere af patroner, men de starter alle der hvor den originale patron var sat.
Heldigvis kan man også fortælle `Instantiate` hvor den skal lave det nye objekt henne, når man gør dette skal man dog også give en rotation med således at det nye objekt er roteret som man vil have det. Tilføj
en ny variable af typen `Transform` med navn `shootingPoint`. For at kunne `Instantiate` fra vores `shootingPoint`, skal vi nu bruge `shootingPoint.transform.postition`.

```C#
void Update()
{
    Instantiate(bulletPrefab, shootingPoint.transform.postition, Quaternion.identity);
}
```
## Input Action
{id = "single-button-input"}

Først skal vi lave en ny variable med navn `shoot` af typen `InputAction` i vores `ShootingScript`


```C#
    public InputAction shoot;
```

Nu skal vi bruge `shoot` variablet, for at finde ud af, om spilleren trygger på det valgte knap. I vores tilfælde har vi valgt at knappen for at skyde skal være mellemrumstasten. Der er to måder man kan tjekke input fra spilleren.
Man kan enten bruge [`IsPressed`](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.14/api/UnityEngine.InputSystem.InputAction.html)
, her vil koden køre så længe spilleren holder knappen nede. 


```C#
if (shoot.IsPressed())
{
    print("Mellemrumstasten er holdt nede");
}
```
Ellers kan man bruge [`WasPerformedThisFrame`](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.14/api/UnityEngine.InputSystem.InputAction.html)
som kun returnerer `true` den første frame hvor tasten er trykket ned. Dvs. man kun vil køre koden en enkelt gang.
```C#
if (shoot.WasPerformedThisFrame())
{
    print("Mellemrumstasten er trykket en gang");
}
```
Vi kan sætte en `if`-statement rundt om kaldet til `Instantiate` således at man kun skydder når man trykker på mellemrumstasten.
```C#
if (shoot.WasPerformedThisFrame())
{
    Instantiate(bulletPrefab, shootingPoint.transform.postition, Quaternion.identity);
}
```

## Cooldown
Vi tilføjer en cooldown periode mellem vores skud, således at der skal være gået mindst en rum tid fra at man har skudt 
til at man kan skyde igen. Til vores cooldown skal vi bruge to variable til at at holde styr på værdier:
1. Definerer en konstant værdi for hvor lang tid den cooldown skal vare
2. Definerer en værdi for hvor mange sekunder der er tilbage før man må skyde igen.

```C#
public float cooldown = 0.2f;
float cooldownLeft;
```
Inde i den `if`-statement vi satte rundt om `Instantiate` kan vi nu sætte `cooldownLeft` til at være lig med `cooldown`
Desuden skal vi ændre på betinglesen for `if`-statementet således at vi kun kan skyde når `cooldownLeft` er mindre eller lig 0 som vist herunder.

```C#
if (shoot.WasPerformedThisFrame() && cooldownLeft <= 0) 
{
    Instantiate(bulletPrefab, shootingPoint.transform.postition, Quaternion.identity);
    cooldownLeft = cooldown;
}
```

Nu kan man, hvis man starter spillet, kun skyde en enkelt gang, fordi vi aldrig gør `cooldownLeft` mindre. Heldigvis 
kræver det kun en enkelt linje kode før `if`-statementet hvor vi gør variablen mindre.
```C#
cooldownLeft = cooldownLeft - Time.deltaTime;
```
`Time.deltaTime` er den mængde af tid der er gået siden sidste frame.

Det er vigtig at huske at højre side af `=` tegnet bliver kørt først. Så selvom:

```C#
val = val + 1;
```

Ikke giver mening i Matematik, så er det helt ok i programming.
Eksempelvis hvis `val` er `1` så når den linje er kørt ville `val` være `2` fordi:
1. Starter med: `val = val + 1`
2. Men vi ved at val var `1`, altså `val = 1 + 1`
3. Det på højre bliver kørt så `val = 2`
4. Det betyder altså at `val` er nu `2`


Noter at du kommer til at møde det her mønster ret meget I spil programmering:

```C#
// Værdi for cooldown tid i sekunder
public float cooldown = 0.2f;

// Værdi for cooldown tid tilbage i sekunder
float cooldownLeft;

void Update()
{
    // Tæl tiden ned
    cooldownLeft -= Time.deltaTime;
    if (cooldown <= 0) 
    {
        // Gør noget her 
        // ...
        
        // Reset hvor meget tid er tilbage
        cooldownLeft = cooldown;
    }
}
```


<tip>
Det kunne måske være at i skal bruge det meget snart ;)
</tip>

## Opgave 1
- Slå `GameObject.Destroy()` op i Unity's dokumentation
- Prøv at bruge `GameObject.Destroy()` til at fjerne bullets efter et stykke tid

<deflist collapsible="true">
<def title="Hint 1" default-state="collapsed">
    For at løse denne opgave skal I selv lave jeres egen MonoBehaviour script og tilføje det på et GameObject
</def>
<def title="Hint 2" default-state="collapsed">
    Det MonoBehaviour script skal tilføjes på Bullet prefab'et
<img src="EnemyScript.gif" alt="Viser hvordan enemy script kan tilføjes"/>
<def title="Hint 3" default-state="collapsed">
    Det er vigtigt at reset dine cooldown/lifetime til at starte ved det rigtige antal sekunder, og ikke 0.
<code-block lang="C#">
void Start()
{
    lifetimeLeft = lifetime;
}
</code-block>
</def>
</def>
</deflist>

Når opgaven er løst bør det gerne se sådan ud:

![InstantiateTimed.gif](InstantiateTimed.gif)



## Bonus Opgave
Tænk over hvordan man ville kunne blive ved med at skyde uden at give slip på skyde knappen
