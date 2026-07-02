# Del 4 (Simpel raycasting)

I denne sektion vil vi prøve at lave et simpel AI, hvor når fjenden kan se spilleren, så skyder den.
## Raycasting
For at finde ud af om fjenden kan se spilleren, så tager vi brug af `RayCast`. Vi kan forstille os en raycast, som en linje vi skyder ud i rummet og, hvis vi rammer noget, så kan vi få noget information om hvad.

Vi laver et nyt script på Fjenden som hedder `EnemyVision`. 

For at tjekke om vi rammer noget foran os, så kan vi gøre det følgende:
```c#
bool hitSomething;
void Update() 
{
    hitSomething = Physics.Raycast(transform.position, transform.forward);
    
    print(hitSomething);
    
}
```
Det første argument til `hitSomething` er start positionen af linjen, det andet er retningen som vi vil skyde mod.



Det er dog ofte ikke så spændende bare at vide om man har ramt noget, så hvis vi gerne vil have noget information om objektet vi har ramt, så kan vi gøre det følgende:

```c#
RaycastHit hit;
bool hitSomething;

void Update() {
    hitSomething = Physics.Raycast(transform.position, transform.forward, out hit);
    
    if(hitSomething) 
    {
        if(hit.transform.CompareTag("Player")) 
        {
            print("Fjenden kan se spilleren");
        }
    }
}
```



## OnDrawGizmos
Når vi arbejder med `Raycast` så er den en god ide for programmøren, at kunne visualisere, hvad vi rammer og hvordan vi skyder i Unity Editoren. Det kan vi opnå med Gizmos.


```c#
void OnDrawGizmos()
{
    if (hitSomething && hit.transform.CompareTag("Player"))
    {
        Gizmos.color = Color.green;
        
    }
    else
    {
        Gizmos.color = Color.red;
    }
    Gizmos.DrawRay(transform.position, transform.forward * 100f);
}
```
`OnDrawGizmos` er en funktion som bliver kaldt af Unity Editoren, hver gang den gerne vil tegne nye Gizmos. 
`Gizmos.DrawRay` tager to argumenter, en start position og en retningsvektor.

I Unity kan det nu ses, at vi skyder ud fra centrum af fjenden, dette er ikke hvad vi ønsker. 
Det kan også ses, at vi kan se uendeligt langt, hvilket er urealistisk.

## Fix af småfejl
For at fixe de to fejl, så skal vi tilføje to variabler til vores script.

```c#
public float sightDistance = 8f;
public Transform eyes;
```

Vi opdaterer nu `Raycast` til at tage højde for de nye variabler.

```c#
hitSomething = Physics.Raycast(eyes.position, eyes.forward, out hit, sightDistance);
```
Vi skal selvfølgelig også opdaterer Gizmos til at bruge den rigtige position:
```c#
Gizmos.DrawRay(eyes.position, eyes.forward * sightDistance);
```

Inde i Unity så skal vi tilføje et nyt tomt `GameObject` som barn af fjenden, som hedder "Eyes".

![fjende-eyes.png](fjende-eyes.png)

Vi skal huske at sørge for at vores `EnemyVision` script på fjenden har en reference til "Eyes"


## Opgave 4
I denne opgave, vil vi gerne bruge den nye mekanik med, at fjenden kan se spilleren, til at få fjenden til at skyde efter spilleren.

<deflist collapsible="true">
<def title="Hint 1" default-state="collapsed">
Lav et "ShootingPoint" på fjenden ligesom der blev gjort i del 1 (Instantiate).
</def>
<def title="Hint 2" default-state="collapsed">
Lav et Script på "ShootingPoint", som har en offentlig funktion 
<code-block lang="C#">
public void Shoot() {
    // Skyd en kugle
}
</code-block>
Kald funktionen fra jeres `AIEyes` script, når i kan se spilleren.
</def>
<def title="Hint 3" default-state="collapsed">
For at kalde funktionen, så kan i lave en variabel i `AIEyes` scriptet.

<code-block lang="C#"> 
public EnemyShoot enemyShoot;
</code-block>

Vi kan nu kalde funktionen ved, at skrive følgende:
<code-block lang="C#">
enemyShoot.Shoot();
</code-block>

Inde i Unity Editoren, så skal vi trække `EnemyShoot` scriptet fra shootingPoint hen i det tomme felt.

![drag-shooting-point-to-enemy.gif](drag-shooting-point-to-enemy.gif)

</def>
<def title="Hint 4" default-state="collapsed">
Få det nye script til at instantiere en ny kugle ligesom der blev gjort i del 1. Og få den til at bevæge sig ligesom i del 2. Det er også vigtigt, at i laver en ny `Layer` og `Tag` som hedder "EnemyBullet". Vi vil nemlig ikke have, at en fjendes bullet kan skade en anden fjende. 
</def>
<def title="Ekstra ting" default-state="collapsed">
I kan måske se, at den enten spawner rigtige mange bullets eller knap så mange. Der er to ting fixes. Først og fremmest så skal i tilføje, at der en cooldown når den skyder ligesom der blev gjort ved Spilleren.

Det andet som er problematisk lige nu er at når der blive skudt en ray ud fra fjenden, så er der en risiko for at den rammer en bullet. Det giver ikke så meget mening at en bullet kan fjerne synsfeltet fra fjenden. Så vi vil gerne ignorere dem, når vi skyder en ray. 

For at opnå det så tilføjer vi en ny variabel til `AIEyes`

<code-block lang="C#">
public LayerMask sightMask;
</code-block>

Det her er en maske, hvor vi kan vælge hvilke `layer` som kan rammes af vores `Raycast`.

<code-block lang="C#">
hitSomething = Physics.Raycast(eyes.position, eyes.forward, out hit, sightDistance, sightMask);
</code-block>

Vi skal huske at tilføje en værdi til `sightMask` i Unity Editor. 

![sight-mask.png](sight-mask.png)

</def>


</deflist>
