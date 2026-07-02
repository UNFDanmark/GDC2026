# Del 1 (3D og Lyd)

## Download Assets
Alle resourcer som vi skal bruge i denne undervisning kan findes her: [Direct Download](https://raw.githubusercontent.com/UNFDanmark/GDC2026/main/%7EDocumentation/resources/ContentGDC2026.zip)

## Opsætning af Model på Spiller

Når vi sætter en model på en spiller, så skal vi først importere modellen. Dette gøres ved at trække modellen ind i `Assets` mappen i Unity.
Her tager vi og importer alle assets fra `ContentGDC2026.zip` til en mappe `/Content`.

![Unity_2SdPWbnbKh.gif](Unity_2SdPWbnbKh.gif)

Når modellen er importeret, så kan vi trække modellen ind i scenen. For at gøre dette skal vi først finde vores spiller GameObject, og derefter trække modellen ind i dette GameObject.

![Unity_jFKcQ1ewee.gif](Unity_jFKcQ1ewee.gif)

I kan passende også her vælge at slette den del af modellen som I ikke har brug for.
<tabs>
<tab title="Før">
<img src="ModelBefore.png" alt=""/>
</tab>
<tab title="Efter">
<img src="ModelAfter.png" alt=""/>
</tab>
</tabs>

## Idle Animation

For at sætte en idle animation ind på spilleren skal vi blot trække animationen ind i vores `Rogue` GameObject.

![InsertAnimation.gif](InsertAnimation.gif)

Når det er gjort skulle i gerne kunne double klikke på `Controller` (som ligger under det `Animator` component der ligger på `Rogue` GameObject).

![AnimatorWindow.png](AnimatorWindow.png)

Men bemærk at den ikke gentager animationen. Det skyldes at vi ikke har sat den til at loope. Dette kan gøres ved at finde animationen på modellen og vælge `Loop Time`.
Dette skal gøres for alle animationer I vil have til at loope.



![LoopAnAnimation.gif](LoopAnAnimation.gif)

Så skulle idle gerne virke 🕺💃

![IdleAnimation.gif](IdleAnimation.gif)

## Opgave A
- Gør det samme for fjender men med skelet modellen.

![SkeletonIdle.gif](SkeletonIdle.gif)

## Animator Window

Som vi tidligere så så var der et **Animator** Window. Dette vindue er hvor vi kan lave animationer og transitions mellem dem.
Når I åbner den ville I se nogle tabs i toppen. Disse tabs er:
- **Parameters**: Her kan vi lave parametre som vi kan bruge til at skifte mellem animationer.
- **Layers**: Her kan vi lave flere lag (noget vi ikke skal bruge på denne camp).

For at lave en parameter skal vi trykke på `+` knappen og vælge hvilken type parameter vi vil have.
De vigstigste typer for os er:
- **Float**: En float er et decimaltal. Dette kan bruges til at skifte mellem animationer baseret på en værdi.
- **Trigger**: En trigger er en bool der bliver sat til `true` en enkelt gang når den bliver kaldt. Men så snart der sker en transition bliver den `false`. Dette kan bruges til at skifte mellem animationer baseret på en handling.

![AnimatorControllerParams.gif](AnimatorControllerParams.gif)

Tilføj nogle flere animationer (en for at gå/at løbe og en for at skyde). Vi valgte `Running_B` og `1H_Ranged_Shoot` til dette.

![AnimatorControllerNodes.png](AnimatorControllerNodes.png)

Nu mangler vi blot at lave transitions mellem animationerne. Dette gøres ved at trække en linje fra en animation til en anden.

Derudover er det også vigtig at definere hvad der skal til for at skifte mellem animationerne. Dette gøres ved at klikke på en transition og kigge på `Conditions` i inspektoren. I den nedstående gif ser vi hvordan vi sætter transitions og hvordan man sætter conditions op for `Shoot`:

![AnimationTransitionA.gif](AnimationTransitionA.gif)

Og her er så det samme men for walking `Speed`.

![AnimationTransitionB.gif](AnimationTransitionB.gif)

## Animator kode

Parameterne er klar men koden mangler stadig.
For at få animationen til at virke i koden, skal vi først have en reference til `Animator` componentet. Dette gøres ved at skrive `public Animator animator;` inde i scriptet der skal bruge det.
(Hvilke er `PlayerMovement` i dette tilfælde).

```C#
public Animator animator;

void Update()
{
    // ...

    // Animation kode går under her (efter movement kode)
    animator.SetFloat("Speed", rb.velocity.magnitude);
}
```

```C#
void Update()
{
    if (...) // Dette er det eksisterende if statement i Shooting
    // scriptet der styrer om spilleren skyder
    {   
        animator.SetTrigger("Shoot");
    }
}
```

Men åh nej, der er jo stadig et problem! Vores transitions er for langsomme:

![AnimatorProblemTransTime.gif](AnimatorProblemTransTime.gif)

For at fikse det skal i fjerne `Has Exit Time` fra alle transitions.
Derudover skal i også fjerne `Transition Duration` fra alle transitions. (kan gøres ved at slide timelinen)

![Unity_L5hnkcZ1dv.gif](Unity_L5hnkcZ1dv.gif)

## Opgave B
- Gør det samme for fjender men med skelet modellen.

![SkeltonAComming.gif](SkeltonAComming.gif)

## Bonus opgave
Find ud af hvordan Textures kan bruges ved at trække `grass.png` texture-et ind i `Assets` mappen og derefter trække den ind på planet.

![GrassInserted.png](GrassInserted.png)

## Lyd

![DragDropAudioToAudioSource.gif](DragDropAudioToAudioSource.gif)

Bemærk at der blev sat en `AudioSource` og ikke et `AudioClip`. Dette er fordi `AudioSource` er det objekt der afspiller lyden, mens `AudioClip` er selve lyden.
Denne `AudioSource` har en masse indstillinger som vi kan ændre på. Eksempelvis satte den `AudioClip` for os til at være vores reele lyd klip.

![AudioSourceSettings.png](AudioSourceSettings.png)

`Play On Awake` betyder at lyden spiller når scenen starter. `Loop` betyder at lyden spiller igen og igen.
Vi ønsker at lyden skal spille når vi skyder, så vi fjerner `Play On Awake` og sikrer os at `Loop` er `false` da, den jo heller ikke skal loope.

## Lyd Kode

```C#
AudioSource audioSource;

void Start()
{
    audioSource = GetComponent<AudioSource>();
}

void Update()
{
    if (...) // Dette er det eksisterende if statement i Shooting
    // scriptet der styrer om spilleren skyder
    {   
        audioSource.Play();
    }
}
```

<note>
Bemærk at lyden altså ikke får en GIF. Lidt svært at vise lyd i en GIF xD.. I har forresten samme problem i undervisningen da vi foretrækker at ikke have alle til at afspille lyd, det kan hurtigt blive meget træls for ørene o.O
</note>
