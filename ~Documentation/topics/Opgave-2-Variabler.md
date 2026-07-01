# Del 2 (Variabler)

## Variabler og typer

{id="variables"}

Når man skriver kode får man ofte brug for at gemme nogle værdier. Disse gemmepladser kalder vi variabler.
I C# ville en variabel kunne se sådan ud:
```C#
int health = 10;
```
I koden ovenfor har vi lavet en variabel `health` som er af typen `int` (integer) og sat den til at være 10.
Man skal altså læse det som "health er lig med 10". Eller:
```
type variabelNavn = værdi;
```

Men der findes mange flere typer end `int`. Her er nogle af de mest brugte:
- `int` er heltal (f.eks. kan man skrive `int health = 10;`)
- `float` er kommatal (f.eks. kan man skrive `float vægt = 13.7f;`)
- `string` er tekst (f.eks. kan man skrive `string navn = "Mikkel";`)
- `bool` er sandt/falsk (f.eks. kan man skrive `bool erVoksen = true;`)

Der er også nogle specielle typer, som der kun findes i Unity:
- `Vector3` er en 3D vektor
- `GameObject` er et Unity objekt
- `Transform` er en position, rotation og skalering

Disse typer kommer vi snart til at bruge. Men vi kommer ikke selv til at fokusere på at lave vores egne typer endnu. Men det er vigtigt at huske at det er en mulighed.
En anden vigtig detalje er at man ikke behøver at sætte en værdi. Man kalder dette for en variabel deklaration.
```C#
int health;
```
Men det er jo ikke så sjovt at have en variabel uden at vide hvad den indeholder. Det er dog en god ide at sætte en værdi med det samme når det er muligt. 

## Men hvor skal variablerne være?
{id="scoping"}
Variabler kan være i mange forskellig steder. Hvis vi husker første lektion, så har vi en `Start` og en `Update` metode.
- Hvis vi placerer en variabel i `Start` metoden, så vil den kun være tilgængelig i `Start` metoden. 
- Hvis vi placerer den i `Update` metoden, så vil den kun være tilgængelig i `Update` metoden.
- Hvis vi placerer den udenfor begge metoder, så vil den være tilgængelig i begge metoder.

```C#
public class PlayerScript : MonoBehaviour
{
    int health = 10;
    
    // Start is called before the first frame update
    void Start()
    {
        int jegVirkerKunIStart = 20;
        print(health + jegVirkerKunIStart); // Skriver 30 i konsollen
    }

    // Update is called once per frame
    void Update()
    {
        int jegVirkerKunIUpdate = 42;
        print(health + jegVirkerKunIUpdate); // Skriver 52 i konsollen
    }
}
```

Hvis i bemærker, så kan i se at reglen er at variablerne er tilgængelige inde mellem hver `{}`. Så fordi `JegVirkerKunIStart` er inde i `Start` metodens `{}`, så kan den ikke tilgås i `Update` metoden.

## Tilgængelighed i editoren
{id="public"}

I C# kan man definere en variabel der lever udenfor en metode som `public`. Det betyder at andre steder kan tilgå den. Se for eksempel koden herunder:
```C#
public class PlayerScript : MonoBehaviour
{
    public int health = 10;
}
```
Her har vi lavet variablen `health` så den er `public` hvilket betyder at andre kan få værdien. I Unity betyder det også at den kan fås fat i fra Editoren så vi kan justere den ude fra vores script.

![VariableIInspector.gif](VariableIInspector.gif)

## Lave sine egne typer?

Jamen i har faktisk allerede skabt 2 af dem!
Da i skrev:
```C#
public class PlayerScript : MonoBehavoiur 
{
    // Kode her
}

public class EnemyScript : MonoBehavoiur 
{
    // Kode her
}
```

Lavede I faktisk typerne `PlayerScript` og `EnemyScript`, som begge er `MonoBehaviour`. 
Det at det er et `MonoBehaviour` betyder at man kan smide dem på et GameObjekt som et component:

![MonoBehaviour.gif](MonoBehaviour.gif)

Som eksempel betyder det at man også kan lave en variabel med en af de typer vi har lavet, altså:
```C#
public PlayerScript myPlayer;
```
Og fordi vi har skrevet `public` kan den også tilgås i vores editor:

![UnityTypeInInspector.gif](UnityTypeInInspector.gif)

## Opgave 2
1. Lav en variabel til at styre spillerens hastighed og gør så man kan tilgå den i editoren
2. Lav en variabel til at håndtere cooldown af skud og gør så man kan tilgå den i editoren

Når i er færdige med at gentage hvad vi har lavet og lave opgaven, bør det se ud som under.

![Unity_52PI0yyFzy.gif](Unity_52PI0yyFzy.gif)

<note>
Bemærk at variabler ikke bliver gemt når i stopper spillet. Hvis i vil gemme en variabel, så husk at ændre den i editoren før i trykker på 'Play' knappen.
</note>
