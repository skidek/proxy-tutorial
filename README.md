# lúzer tutoriál
## Kellékek:
- [Java 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- [Proxy*](https://github.com/marvintheskid/mc-reverse-proxy)
- [Kotlin Script Engine*](https://github.com/marvintheskid/reverse-proxy-kotlin-scripting)
- [Kotlin Scriptek](https://github.com/skidek/kotlin-scriptek)
- [Token Scanner*](https://github.com/skidek/scan-ffi)

\**buildelni kell*  
  
Ahhoz, hogy buildelni és használni tudd a proxy-t, Java 17-re lesz szükséged (linkelve).  
A fent lévő projekteket vagy lehúzod gittel, vagy letöltöd simán a GitHub webes felületének használatával. (zip-elt fájlok, ki kell csomagolni mindet egyesével egy-egy mappába)  
![github](https://github.com/skidek/proxy-tutorial/blob/main/github.png?raw=true)


## Buildelés menete
### 1. - Proxy
A proxy-t különösebb trükközés nélkül le lehet buildelni a ```gradlew.bat build``` paranccsal.  
![output](https://github.com/skidek/proxy-tutorial/blob/main/gradle.png?raw=true)  
Ezek után a mappán belül a ```standalone/build/libs``` mappán belül meg kell jelennie egy ```standalone-all.jar``` fájlnak. Ez lesz a proxy, amit később futtatni fogunk.

### 2. - Kotlin Scripting
Ahhoz hogy a script engine lebuildeljen, kell egy proxy build (a fent említett ```standalone-all.jar```). A buildelt proxy-t csak be kell húzni a ```deps``` nevű mappába.  
![folder](https://github.com/skidek/proxy-tutorial/blob/main/scripting_dep.png?raw=true)  
Ezután simán megismételhető az előbb elvégzett művelet (```gradlew.bat build```). Ha sikeres a művelet, akkor a ```build/libs``` mappában megjelenik egy ~70MB-os ```kotlin-scripting-1.0-SNAPSHOT-all.jar``` nevű fájl. Ez lesz az addonunk.
### 3. - Token scanning
Ez se igényel semmi plusz törődést, le lehet buildelni a ```gradlew.bat build``` paranccsal.  
Ennek a futtatásához magán a mappán belül lesz egy ```launch.bat```


## Futtatás
A ```standalone-all.jar```-t egy üres mappába húzzuk bele, majd csináljunk egy helper .bat fájlt a könnyebb indításért.  
```batch
java -jar standalone-all.jar
PAUSE
```
Indítás után állítsuk le a proxyt a ```stop``` parancs segítségével. Az első indításkor a proxy generál egy ```addons``` nevű mappát, ide kell behúzni a ```kotlin-scripting-1.0-SNAPSHOT-all.jar```-t.  
Ha ezután elindítjuk a proxyt, akkor a következőt kell látnunk:  
![command line](https://github.com/skidek/proxy-tutorial/blob/main/cmd.png?raw=true)  
Az ```addons``` mappán belül ilyenkor már lennie kell egy ```scripts``` nevű mappának. Ebbe a mappába lehet belemásolni a ```proxy.kts``` kiterjesztésű proxy scripteket.


## Használat
### Alapvető parancsok
- setname - Beállítja a felhasználónevet
- setuuid - Beállítja a UUID-t (Fontos, hogy az UUID-t itt '-'-ek nélkül adjuk meg!)
- settoken - Beállítja a access tokent
- credentials - Kiírja a jelenleg megadott adatokat
- kts help - Scripteléssel kapcsolatos parancsok

### Fornetti MC dolgok
Ahhoz, hogy a fornetti szerverein játszhass, a fent leírt parancsokra van szükséged, illetve a ```fyre``` parancs futtatására. 
A szükséges adatokat a ```scan-ffi``` projekt segítségével tudod kinyerni a launcherükből loginolás után.
Fontos, hogy minél hamarabb futtassuk le a scannert login után, különben megeshet az, hogy a program nem talál semmit.
Ilyenkor csak annyi a teendő, hogy újra belépsz a launcheren belül, és újra lefuttatod a scannert.


## Extra infó
- [Videó, ahol az itt leírtakat láthatod](https://www.youtube.com/watch?v=kTgHIWe_Rh4)
