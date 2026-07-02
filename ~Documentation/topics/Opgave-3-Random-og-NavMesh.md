# Del 3 (Random og NavMesh)

## NavMesh

### Navmesh Surface

For at kunne skabe nogle mere spændende fjender, vil vi gerne have de kan bevæge sig. 
Til det bruger vi NavMesh. Først skal vi fortælle unity hvorhenne vores enemy må og kan gå. 
Til det formål giver unity os komponentet `NavMeshSurface`. Lad os tilføje den til vores plane.

![navmeshsurface.png](navmeshsurface.png)

Her er der en del indstillinger at lege rundt med, men for nu trykker vi på Bake knappen.

![baked.png](baked.png)

Det blå område der tegner sig er vores navmeshsurface. Det er det område vores enemy kan gå på.
Desværre er det sådan at ikke alt er helt blå, det skyldes at den prøver at undgå potentielle obstacles. 
Den letteste måde at fikse det her er at vælge `CollectObjects > Current Object Hierarchy`. Som set herunder:

![fixbakednavmesh.gif](fixbakednavmesh.gif)

### Navmesh Agent
Men før vores enemy kan finde rundt skal vi også lige fortælle vores enemy object at den kan gå.
Her giver vi den komponetet `Nav Mesh Agent`. Den fotæller unity at vores enemy object skal kunne navigere på en navmesh surface,
som den vi lige har lavet.

![navagent.png](navagent.png)

{id = "findwithtag"}
Vi skal dog stadig fortælle den hvor den skal gå hen. Det kan vi heldigvis nemt gøre med `SetDestination()` funktionen.
SetDestination tager imod en Vector3 position, som for eksempel vores spillers position. 
I vores enemy script skal vi hive fat i vores `Nav Mesh Agent`, brug enten `GetComponent<NavMeshAgent>()`,
eller lav en public NavMeshAgent og drag and drop den i Unity. 
Vi skal have en reference til vores player, her skal vi igen gøre brug af `Tags`, heldigvis har unity allerede et player tag.
Giv vores playerobject player tagget og brug `FindWithTag("Player")`.

![playertag.gif](playertag.gif)

```c#
public NavMeshAgent agent;
GameObject player;

void Start(){
    player = GameObject.FindWithTag("Player");
}

void Update(){
    agent.SetDestination(player.transform.position);
}
```

### Enemy Spawner

![WalkTowardPlayer.gif](WalkTowardPlayer.gif)

<tip>
Bemærk at fjenden går meget hurtig. 
Det kan fikses ved at enten gøre spileren hurtigere eller fjenden langsommere.
Til spileren har I selv allerede lavet en speed variable. 
Men til Nav Agent har i ikke selv valgt speeden. Det gør i istedet ved at sætte <code>Steering > Speed</code>. 

![SteeringSpeedNavAgent.png](SteeringSpeedNavAgent.png)
</tip>

## Random
Det er jo ikke så spændende at der kun er en fjende.
Til det laver vi et enemySpawner object. Siden det ikke er noget vi skal kunne se, giver det mening at lave et empty object. 

![ObjectField.png](ObjectField.png)

Så laver vi et `EnemySpawnerScript` på vores `EnemySpawner`.
I det skal vi have en reference til det object vi gerne vil spawne, altså vores enemyobject.
Som med vores bullet kan vi spawne flere med `Instantiate()`.

```c#
public GameObject spawnObject

void Update(){
    Instantiate(spawnObject, transform.position, Quaternion.identity);
}
```

![Unity_nQmMxE5WQX.gif](Unity_nQmMxE5WQX.gif)

Ligenu spawner der måske lidt for mange enemies på få frames. Dette problem kan løses ret hurtigt ved at bruge samme cooldown pattern som vi
lavede til vores `ShootingScript`. Vi skal lave to nye variabler, begge variabler skal være af typen `float`. Den ene variable skal hedde `spawnCooldown` og den anden 
skal hedde `currentSpawnTime`.


```c#
public GameObject spawnObject;
public float spawnCooldown = 2f;
float currentSpawnTime;

void Update(){
    
    currentSpawnTime -= Time.deltaTime;
    if(currentSpawnTime <= 0)
    {
        Instantiate(spawnObject, transform.position, Quaternion.identity);
        currentSpawnTime = spawnCooldown;
        
    }
}
```
{id = "random"}
Det ville dog være kedeligt hvis de alle spawnede det sammes sted hver gang. 
Så hvad nu hvis vi generede nogle tilfælge positioner til vores fjender. 
Her kan vi bruge `Random.Range` der giver os et tilfældigt tal mellem 2 tal vi vælger. 
Vi starter småt med et tal mellem -5 og 5.
```c#
Vector3 spawnPosition = transform.position;
spawnPosition.x = spawnPosition.x + Random.Range(-5, 5);
spawnPosition.z = spawnPosition.z + Random.Range(-5, 5);
Instantiate(spawnObject, spawnPosition, Quaternion.identity);
```
![Unity_NrfFgqXym5.gif](Unity_NrfFgqXym5.gif)


## Opgave
1. Få mønter til at spawne på tilfældige steder
2. Få mønter til at rotere
3. Få mønter til at have en spawn timer

![Unity_InlU28VqFn.gif](Unity_InlU28VqFn.gif)
