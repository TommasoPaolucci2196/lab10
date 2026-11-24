# Lavorare con MVC

Questa applicazione è la stessa vista nelle slide del corso principale, con piccoli miglioramenti (il codice qui non deve necessariamente stare in poche slide). Fai riferimento alle slide per capire come funziona l'applicazione.
Arricchiremo l'esempio aggiungendo l'I/O.

## Preparare la UI a mostrare gli errori

L'accesso all'I/O è fonte di nuove possibili situazioni impreviste, che dovrebbero essere segnalate all'utente come errori tramite la UI. Come primo passo, aggiungeremo alla view la capacità di mostrare gli errori generati nel controller.

* Aggiungi un metodo `void displayError(String message)` in `DrawNumberView`
* Implementa il metodo in `DrawNumberViewImpl`, usando `JOptionPane.showMessageDialog()` per mostrare l'errore

## File di configurazione

Attualmente le impostazioni del gioco (minimo, massimo e numero di tentativi consentiti) sono scritte direttamente nel codice (hard-coded).
Modifica l'applicazione in modo che tali impostazioni vengano lette dal file di configurazione fornito.
Il file di configurazione predefinito si trova nel percorso `src/main/resources/config.yml`.

### Suggerimenti

* Usa il resource loader per caricare il file fornito in res.
  Puoi avvolgere lo stream con uno `StreamReader` e un `BufferedReader` per ottenere il contenuto e procedere riga per riga.
* Il file (vedi l'esempio nella cartella "res") è un [file YAML standard](https://en.wikipedia.org/wiki/YAML).
  Esistono librerie che permettono di fare il parsing di YML facilmente, ma questo file è così semplice che non serve nessuna strategia particolare:
  basta filtrare ciò che sta prima e dopo i due punti.
* Non fare in modo che la View operi sul file system.
  Più precisamente, il controller nel suo costruttore deve essere in grado di leggere il file di configurazione fornito
  e di importare le tre costanti.
  Ancora meglio,
  un'utility esterna (un metodo o un'altra classe) potrebbe occuparsi di questo.
  Il motivo è che l'interazione con il file system non fa parte del modello di dominio e, in questo caso, nemmeno della view.
* Puoi usare `StringTokenizer` per dividere una `String` in parti.
  Un'altra opzione, disponibile proprio per questo caso, è `String.split()`, passando `":"` come argomento.
  Attenzione a `split()`: la `String` in input è in realtà un'espressione regolare.
  Le espressioni regolari (regex) sono uno strumento molto potente, ma non possiamo trattarle in questo corso:
  si raccomanda ``StringTokenizer``, a meno che tu non conosca già le espressioni regolari e sappia come usarle.

## Viste multiple

* Nota che l'architettura permette di collegare più viste a runtime.
* Collega contemporaneamente due viste grafiche, il file logger e la vista console, e verifica che l'applicazione funzioni come previsto.
