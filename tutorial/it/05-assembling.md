## Costruzione
La costruzione è talmente semplice che mi sembra inutile andare step-by-step sulle saldature dei singoli
componenti.  
La scelta dei pin è stata assolutamente personale. Ovviamente non vuol dire che potete scegliere dei pin a caso.

#### Circuito relè
La scheda o circuito relè è una scheda preassemblata con uno o più relè (dipende da cosa avete acquistato).
Il circuito include alcuni componenti di supporto necessari a rendere controllabile il relé
(il rettangolino blu con le viti) dalla vostra Rasp.
Su questo punto vorrei soffermarmi visto che qui ho fatto il mio primo errore. Ma partiamo con una piccola introduzione.

Un relè è un componente che, se opportunamente alimentato, chiude o apre un circuito sotto il suo controllo
a seconda della tensione applicata sul relé stesso. Quando si acquista un relé bisogna tenere conto di tre cose:

* la corrente e la tensione massime per il circuito controllato dal relè
* la tensione di alimentazione
* la tensione di attivazione

Per il carico massimo sul circuito controllato di solito i relè arrivano tutti a 250 V/10 A per cui direi che,
a meno che avete una centrale nucleare, dovrebbe andar bene.

La tensione di alimentazione di solito è 5 V. Accertatevene all'acquisto. L'alimentazione andrà collegata
ad [un pin 5 V](https://pinout.xyz/pinout/pin2_5v_power).

La tensione di attivazione è quella necessaria per comunicare al relè di aprire o chiudere il circuito
dall'altra parte (il circuito ON/OFF della caldaia). La tensione in questione è quella fornita dal pin
dati digitale a cui collegherete il pin dati della scheda relè (cavo giallo nello schema). Quando il pin
è impostato ad un valore alto (1 - HIGH), la Rasp emette una tensione di 3.3 V. A quel punto il relè chiude
il circuito sul contatto "NC" (normally closed) e lo apre nel contatto "NO" (normally open).
Abbassando il pin (0 - LOW), il relè invertirà la situazione: NC aperto, NO chiuso.

(schema o animazione funzionamento relè)

Peccando di disattenzione, ho acquistato per errore un relè che si attiva a 5 V. Me la sono cavata con un "magheggio" lato software, ma ve lo sconsiglio (onestamente non ho capito come abbia fatto a funzionare).
**Accertatevi che il relè si attivi a 3.3 V.**

Alla fine dovreste avere un risultato simile a questo:

(foto assemblaggio completo)

... TODO ...
