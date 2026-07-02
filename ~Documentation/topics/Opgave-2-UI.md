# Del 2 (UI)

## Lav Game Over Canvas

For at lave UI i Unity, så skal man bruge et Canvas. Det kan laves som set herunder

![CanvasCreation.png](CanvasCreation.png)

I samme billede kan du også se hvordan man laver en tekst, som kan bruges til at vise Game Over. (hedder: `Text - TextMeshPro`)

Lad os bruge den viden til at lave denne skærm:

![GameOverScreen.png](GameOverScreen.png)

Dens struktur kan ses her:
* Canvas
  * Game Over (background)
    * GameOver Text
    * Reset Text

For at lave baggrunden, kan man bruge en `Image Raw` og vælge en farve.
Det er vigtigt at man ændrer mode til `stretch` for både x og y aksen, så det fylder hele skærmen.

![FitImageToScreen.png](FitImageToScreen.png)

Se hvordan det ser ud i spillet:

![FitBackgroundToScreen.gif](FitBackgroundToScreen.gif)

Værdier vi bruger:

![ValuesUsedByUI.png](ValuesUsedByUI.png)

Planen er at denne tekst skal være skjult indtil spilleren dør. Dette kan gøres ved at disable objektet i Unity:

![HiddenCanvas.gif](HiddenCanvas.gif)

## GameOver Implementation

Tilføj så at hvis spilleren rammer en fjende, så aktiveres GameOverScreen.
```C#
public GameObject gameOverScreen;

void OnCollisionEnter(Collision other)
{
    if (other.gameObject.CompareTag("EnemyBullet"))
    {
        gameOverScreen.SetActive(true);
    }
}
```

![GameOverWorks.gif](GameOverWorks.gif)

## Reload Scene

Ofte er det nice at kunne genstarte spillet, dette kan gøres ved at genindlæse scenen.

På klassen `SceneManager` i Unity er der en metode `LoadScene` som kan bruges til at genindlæse scenen.

```C#
void Update()
{
    if (restartAction.WasPressedThisFrame())
    {
        SceneManager.LoadScene("Programmering");
    }
}
```

## Opgave
* Tilføj liv variable til spilleren
* Opdater en tekst i UI'et til at matche antal liv

![Unity_DlfCdNGIvo.gif](Unity_DlfCdNGIvo.gif)
