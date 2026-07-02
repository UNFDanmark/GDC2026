# Del 2 (Kollision)

## Physics Layer
Som man kan se når man starter spillet, så støder de patroner som man skyder ind i spilleren selv. Til at løse det problem
gør vi brug af det som Unity kalder Physics layers. Disse layers dikterer hvad der kan kollidere med hvad, så vi skal bruge
nogle layers til at repræsentere vores spiller og patroner. Man kan tilføje nye physics layers ved at vælge et objekt og
klikke på "Add layer..." knappen i Layer dropdown menuen under objektets navn.

![create-layers.png](create-layers.png)

<tip>
Husk at, efter du har tilføjet layer's, skal du også gå tilbage til <b>spilleren</b> og <b>bullet</b> og vælge de nye layers.
</tip>

Når man har lavet lagene skal man huske at tildele dem til ens `gameObjects`, det gør man samme sted som hvis man skulle lave nye lag.

Som vist herunder kan vi i project managerens Physics sektion deaktivere kollisioner mellem Player og Bullet lagende.

![collisionLayerMatch.gif](collisionLayerMatch.gif)

## Påvirk andre objekter
Nu hvor vi kan lave patroner vil vi gerne have at patronerne også flyver frem så man rigtig skyder. Istedet for at lave et 
script til patronen så kan vi istedet gøre det fra spilleren af. Når man kalder `Instantiate` får man faktisk også det objekt man laver tilbage som en værdi der kan gemmes.
Vi gemmer den nye bullet i en variabel `bullet`, så henter vi ´bullet´s rigidbody komponent og sætter dens hastighed lig med `transform.forward`, som svarer til det vores spiller anser som fremad, ganget med en variabel ´bulletSpeed´.
```C#
if (shoot.WasPerformedThisFrame() && cooldownLeft <= 0)
{
    GameObject bullet = Instantiate(bulletPrefab, shootingPoint.transform.postition, Quaternion.identity);
    Rigidbody bulletRb = bullet.GetComponent<Rigidbody>();
    bulletRb.linearVelocity = transform.forward * bulletSpeed;
    cooldownLeft = cooldownTime;
}
```

## OnCollisionEnter
Når nu vi faktisk kan skyde, så vil vi gerne have noget at skyde efter. Lidt ligesom da vi lavede spilleren laver vi en simpel kapsel
som vi kan kalde "Enemy". Fjenderne skal naturligvis dø når de
rammes af en patron. Unity har defineret funktionen `OnCollisionEnter` som kaldes automatisk når to objekter koliderer.
Det er nemmest hvis fjenderne selv holder styr på hvornår de bliver ramt, så vi laver et script til dem, og tilføjer den nedenstående kode.

```C#
void OnCollisionEnter (Collision other)
{
    //Code here
}
```

I denne funktion får man information om det andet objekt i kollisionen gennem variablen `other`. Vi er kun interesserede i 
kollisioner der involverer patroner, så vi benytter en `if`-statement. I den statements betingelse kan vi benytte det der 
hedder tags til at kende forskel på patroner og andre typer af objekter. Som vist nedenunder laver vi et tag "Bullet" og 
tildeler det til vores prefab af patronen.

![PrefabBulletTag.gif](PrefabBulletTag.gif)

For at sikre at `other` er koblet til et `gameObject` med tagget "Bullet" bruger vi funtionen `CompareTag` som vist nedenunder.

```C#
if (other.gameObject.CompareTag("Bulllet")){
    
}
```

## GameObject.Destroy
Når man gerne vil fjerne `gameObjects` kan man med fordel bruge funktionen `Destroy`, som tager det `gameObject` som skal
fjernes som parameter.
Eksempelvis kan vi, når vi har sikret at fjenden er ramt af en patron, fjerne fjenden med `Destroy` som vist nedenunder.

```C#
if (other.gameObject.CompareTag("Bulllet")){
    Destroy(gameObject);
}
```

## Opgave 
1. Slå “OnTriggerEnter” op i Unity's dokumentation 
2. Anvend funktionen til at lave en mønt der forsvinder når spilleren rammer den

![CoinsCollect.gif](CoinsCollect.gif)
