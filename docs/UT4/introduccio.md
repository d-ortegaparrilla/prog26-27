# Introducció

Fins ara, en els programes desenvolupats només hem treballat amb un nombre reduït de variables independents per a emmagatzemar valors concrets. No obstant això, en el desenvolupament d'aplicacions reals és molt freqüent haver de manipular conjunts nombrosos de dades relacionades entre si.

Imaginem, per exemple, que volem calcular la temperatura mitjana del mes d'agost i conéixer quins dies s'ha superat aquesta mitjana. Per a fer-ho, necessitem registrar els 31 valors de temperatura diaris. Podríem pensar a utilitzar una única variable per a anar llegint cada temperatura i acumular la suma en una altra variable; però en fer-ho, cada nou valor sobreescriu l'anterior i es perden les temperatures individuals. Quan acabe el mes podrem calcular la mitjana, però ja no podrem saber quins dies concrets van estar per damunt o per davall de la mitjana. 

Una altra opció seria declarar 31 variables diferents (`temp1`, `temp2`, ..., `temp31`), però aquesta solució resulta inviable, repetitiva i totalment inescalable si en compte de 31 dies hem de gestionar 1.000, 10.000 o un nombre indeterminat de dades introduïdes per l'usuari en temps d'execució.

Per a resoldre aquesta necessitat sorgeixen els **arrays** (també anomenats **vectors**, **taules** o **matrius**): estructures de dades que permeten emmagatzemar un conjunt finit d'elements del mateix tipus en posicions consecutives de memòria sota un únic nom comú. Així mateix, aprofundirem en el tractament de cadenes de caràcters (`String`), la seua relació directa amb els vectors de tipus `char` i l'ús potent de les **expressions regulars** (*regex*) per al reconeixement i validació de patrons textuals.

!!! info "Objectius de la Unitat Temàtica 4 (RA6)"
    * **Concepte d'estructura estàtica:** Comprendre la representació en memòria dels arrays com a blocs contigus d'elements homogenis.
    * **Arrays unidimensionals (vectors):** Dominar la declaració, instanciació, inicialització (per defecte i explícita), accés indexat i l'ús de l'atribut `length`.
    * **Recorregut d'arrays:** Implementar recorreguts seqüencials complets i parcials emprant tant el bucle clàssic `for` com el bucle millorat per a col·leccions (`for-each`).
    * **La classe `Arrays`:** Aprofitar les eines estàndard de `java.util.Arrays` per a visualització (`toString`), inicialització (`fill`), ordenació (`sort`), cerca dicotòmica (`binarySearch`), còpia (`copyOf`, `copyOfRange`) i comparació (`equals`).
    * **Arrays de caràcters:** Manipular vectors de tipus `char`, entendre la funció del caràcter nul (`\0`) i les conversions entre cadenes i arrays de caràcters.
    * **Classe `String`:** Comprendre la immutabilitat dels objectes `String`, la gestió de memòria (*String Pool*) i emprar eficaçment els seus mètodes per a cerca, extracció, divisió i comparació de text.
    * **Expressions regulars (*regex*):** Dissenyar patrons de cerca i validació textual mitjançant classes de caràcters, quantificadors, ancoratges i les eines de `java.util.regex` (`Pattern` i `Matcher`).
    * **Matrius bidimensionals:** Declarar, inicialitzar i recórrer taules bidimensionals i matrius irregulars (*ragged arrays*) emprant estructures repetitives niades.
    * **Algorísmica sobre arrays:** Implementar algorismes fonamentals de processament: cerca de màxims i mínims, filtrat, inserció d'elements amb desplaçament i fusió de vectors ordenats.
