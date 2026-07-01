# Del 1 (Krop og kode)

Velkommen, dette er starten af jeres eventyr for at lære Unity!
Vi starter med åbne projektet og se på nogle af de grundlæggende ting i Unity.
I dette segment begynder vi også at se på, hvordan vi kan bruge kode til at interagere med vores spil.

<note>Nogle skærmbilleder viser Unity-version som andet end 6000.1.10f1 ignorer dette</note>

![unitybrugerflade](unitybrugerflade.png)


## Åbne projektet
For at starte skal i åbne Unity Hub og åbne projektet "TheUnityProject" som vi har gjort klar til jer.

![unityhub.png](unityhub.png)


Når I har åbnet projektet, er I klar til at begynde at arbejde i Unity.

## Unity brugerflade

Når I har åbnet projektet, vil i se Unity brugerfladen. Her er nogle af de vigtigste elementer i brugerfladen:

1. **Scene view**: Her kan i se jeres spil og redigere det.
2. **Game view**: Her kan i se jeres spil som det vil se ud for spilleren.
3. **Hierarchy**: Her kan i se alle objekter i jeres scene.
4. **Inspector**: Her kan i se og redigere egenskaberne for det valgte objekt.
5. **Project**: Her kan i se alle filer i jeres projekt.
6. **Console**: Her kan i se fejl og beskeder fra Unity.

## Projekt setup

Hvis vi kigger i projekt vinduet kan i se at vi allerede har tilføjet nogle filer for jer, deriblandt en scene for hver faggruppe, og en general GameScene hvor det endelige spil skal laves.

## Spiller Objektet

I jeres scene vil i kunne højre klikke og vælge `Create Capsule` for at lave et nyt objekt. Dette objekt vil være jeres spiller objekt. 
I kan flytte spilleren ved at klikke på objektet og trække det rundt i scenen.

![create-capsule.png](create-capsule.png)

## Kode

For at kunne skrive systemer, så skal man tilføje komponenter til sine GameObjects. Vi senere gerne have vores spiller til at interagerer med fysik, så vi tilføjer en `RigidBody` til et objekt, ved at trykke på `Add Component` og herefter søge efter `RigidBody`.

Lav et script til spilleren ved at klikke på spilleren i hierarkiet og derefter klikke på `Add Component` i inspektoren.
Vælg "New Script" og kald det "PlayerScript". Dobbeltklik på scriptet for at åbne det i Rider.

![create-script.gif](create-script.gif)

I bør se en stump kode der ser sådan ud:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

Her er der to metoder, `Start` og `Update`. 
- `Start` bliver kaldt når spillet starter.
- `Update` bliver kaldt en gang hver gang der tegnes et billede på skærmen. (en gang per frame).


## Start
Hvis vi skriver `print("Jeg er kaldt en gang")` i `Start` metoden, vil vi se "Jeg er kaldt en gang" i konsollen når spillet starter.
```C#
// Start is called before the first frame update
void Start()
{
    print("Jeg er kaldt en gang");
}
```


## Update
Hvis vi skriver `print("Jeg er kaldt meget")` i `Update` metoden, vil vi se "Jeg er kaldt meget" i konsollen en masse gange. En gang per frame for at være nøjagtig.
```C#
// Update is called once per frame
void Update()
{
    print("Jeg er kaldt meget");
}
```

## Kommentarer
I koden ovenfor har vi også brugt noget der hedder kommentarer. Kommentarer er tekst i koden som ikke bliver kørt. De er der for at forklare hvad koden gør.
I C# skriver man `//` for at lave en kommentar, hvor alt efter `//` vil blive ignoreret af computeren.
```C#
// Dette er en kommentar
```

## Opgave 1
Her er jeres første opgave:
1. Lav endnu et objekt, der kan bruges som fjende, med samme komponenter som spilleren (foruden PlayerScript)
2. Få fjenden til at skrive “Hej jeg er ond” en gang i konsollen

Når i er færdige med at gentage hvad vi har lavet og lave opgaven, bør det se ud som under. 
I er velkommen til at læse forud men så kan det hurtig blive kedeligt.

![opgave1-1.gif](opgave1-1.gif)
