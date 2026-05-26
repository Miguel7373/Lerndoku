Controller injects can't be Immutable so they won't change after it starts
that's why you normally use controller injections 



Field injection wird jedes Mal neu injected wenn es benutzt wird was heißt, das während dem Ablauf des Programmes sich das injectete Objekt verändert, sich auch das aus der field injection ändert, was nur in ganz speziellen fällen benutzt wird. Controller injects sind einmal am Anfang injected und sind dann statisch durch die ganze Runtime.



