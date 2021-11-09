# Other

•	Log: essex genera un log su file specificato da parametro da riga di comando. In pratica logga una riga per ogni richiesta che gli arriva, in formato classico da log http (tipo <timestamp> <path> HTTP  1.0 <http_status> <dimensione_request> <dimensione_response>, o qualcosa del genere…). Niente di che, niente errori, diciamo che secondo me il log è uno dei punti dolenti. Fra l’altro non è configurabile, non rolla, niente è il minimo sindacale.
•	Update CPK: sì, in sostanza si fa come dici tu, ma la cosa migliore sarebbe gestirlo con una cosa tipo versioni. Nella vecchia tecnologia ogni LPK che pubblicavi aveva un nome tipo <nomeprogetto>_<timestamp>.lpk, ora invece è solo <nomeprogetto>.cpk. Con il timestamp tu dovevi solo cambiare il nome che mettevi nella request con quello nuovo, e essex aggiornava le sue istanze, magari anche scaricandosi il nuovo pacchetto se gli davi l’URL e non l’avevi in locale. Diciamo che la gestione delle versioni è un punto aperto.
•	Per usare essex sotto linux nella vecchia versione avevamo un installer che installava script di gestione servizi per Redhat/centos, e includeva nel pacchetto anche l’eseguibile “daemon” per gestire il riavvio automatico e cose del genere. In pratica l’installer Linux copiava binari in una cartella e configurava i servizi per esecuzione automatica, ecc. La cosa andrebbe rifatta, magari in modo diverso perché la vecchia andava solo su distribuzioni con servizi tipo SysV (RedHat, CentOS, Fedora) e non su quelli tipo BSD (Debian, Ubuntu, ecc.) che sono quelli che usiamo di più adesso.

Una cosa da capire è anche questa: oltre alle installazioni “tradizionali” avrebbe senso distribuire essex come immagine Docker, visto che sembra il modello “quasi standard” ultimamente? Sarebbe facile da fare (anzi, c’è già) in questo modo:
-	L’immagine funziona in modalità “risorsa”, quindi ogni immagine è a singola istanza (singolo processo), se vuoi parallelizzare moltiplichi i container (*)
-	La licenza e anche il CPK non stanno nell’immagine ma su folder esterne mappate come volumi all’avvio del container, così parte e si vede la sua licenza specifica e il suo pacchetto specifico, e con un build unico di essex gestiamo la cosa.
-	Questa immagine Docker l’avevamo già fatta e pubblicata su Docker Hub per Edge (forse senza la gestione della licenza che non serviva). L’abbiamo tirata giù quando si è deciso di ammazzare Edge, ma abbiamo già tutto.

(*) Questa cosa del “processo singolo” si presta molto all’uso in immagini Docker, ma solo in apparenza. Di solito i server http in Docker (Apache http, nginx, ecc. ecc.) è vero che sono processo singolo, ma è anche vero che non gestiscono certo una sola richiesta alla volta, come faremmo noi in questa modalità.

From: Andrea Varone <avarone@expert.ai> 
Sent: martedì 19 ottobre 2021 18:46
To: Nico Lavarini <nlavarini@expert.ai>
Cc: Francesco Baldassarri <fbaldassarri@expert.ai>
Subject: RE: essex/Documentazione/Domande!

Ammazza Nico, ricopio in bella e ho fatto il manuale dell'amministratore :-)
Beh, forse no, però grazie tante.
Ho altre domande, altre ancora verranno:
•	essex genera dei log? Se sì, di che tipo?, dove?, si auto-rollano?, si configurano?
•	l'update di un CPK come funziona? Spengo, sostituisco e riaccendo? Oppure?
•	se volessi usare essex come demone sotto Linux come devo fare?
