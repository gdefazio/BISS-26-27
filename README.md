# **ESERCITAZIONI PRATICHE DEL CORSO DI BIOINFORMATICA ED ANALISI FUNZIONALE DEL GENOMA**  

## ***Introduzione alla Bioinformatica***
Prima di addentrarci nello studio di questa disciplina è opportuno soffermarsi su quale sia la definizione più appropriata e delinearne i principali ambiti di ricerca e applicazione.  
Nel corso degli anni sono state proposte numerose definizioni che possono essere così sintetizzate:  

***La Bioinformatica si occupa della ricerca, dello sviluppo e dell’applicazione di approcci computazionali per l’interpretazione di dati biologici.***  

**Questi includono l’informazione genetica racchiusa nei genomi e le modalità della loro espressione (trascrittoma, proteoma, microbioma, pathways metabolici, ecc.).**  
 
La ricerca nel settore della Bioinformatica si occupa quindi di sviluppare gli approcci più appropriati per collezionare i dati biologici in apposite banche dati, di mettere a punto gli strumenti più idonei per la loro interrogazione e di sviluppare metodologie per la loro analisi con l’obiettivo di contribuire alla comprensione dei meccanismi molecolari alla base della vita.   

La Bioinformatica è per sua natura **multidisciplinare** richiedendo il concorso di competenze diverse (Biologia Molecolare, Biochimica, Fisiologia, Genetica, Informatica, Matematica, Statistica, Chimica, Fisica, Ingegneria, ecc.) ed ha applicazioni pratiche in vasti settori della scienza.   

L’aumento esponenziale dei dati biologici, cui assistiamo in questi anni a seguito del completamento di numerosi progetti di sequenziamento genomico (incluso il genoma umano) e dell’avvio di numerosi progetti su larga scala per lo studio del trascrittoma, del proteoma e del microbioma di numerosi organismi, comporta una crescente importanza della Bioinformatica in tutti i settori della ricerca a livello biomolecolare. [](https://www.ncbi.nlm.nih.gov/genbank/statistics/)
  
I principali tipi di dati biologici sono:  
    -	**Sequenze nucleotidiche** (vedi [https://www.ncbi.nlm.nih.gov/guide/dna-rna/](https://www.ncbi.nlm.nih.gov/guide/dna-rna/) per una lista delle risorse di sequenze di DNA o RNA oppure [http://www.ebi.ac.uk/ena](http://www.ebi.ac.uk/ena) per un archivio di informazioni sul sequenziamento nucleotidico nel mondo);  
    -	**Sequenze proteiche** (vedi [https://www.ncbi.nlm.nih.gov/guide/proteins/](https://www.ncbi.nlm.nih.gov/guide/proteins/) per un elenco di risorse proteiche oppure [http://us.expasy.org/sprot/](http://us.expasy.org/sprot/) per informazioni su una delle più importanti risorse di sequenze proteiche, la *UniProtKB/Swiss-Prot*);   
    -	**Strutture tridimensionali** di proteine ed altre macromolecole (vedi [https://www.ncbi.nlm.nih.gov/guide/domains-structures/](https://www.ncbi.nlm.nih.gov/guide/domains-structures/) per le risorse di domini e strutture molecolari oppure [http://www.rcsb.org/pdb/](http://www.rcsb.org/pdb/) per la risorsa di macromolecole biologiche *PDB*);     
    -	**Dati di espressione** ([https://www.ncbi.nlm.nih.gov/guide/genes-expression/](https://www.ncbi.nlm.nih.gov/guide/genes-expression/) per le risorse relative all’espressione dei geni e ai fenotipi correlati);   
    -	**Dati metabolici** ([http://www.genome.jp/kegg/](http://www.genome.jp/kegg/) per una risorsa sulle relazioni metaboliche tra i geni e i loro prodotti);  
    -	**Letteratura scientifica** (per accedere ad un’importante risorsa di letteratura biomedica [https://www.ncbi.nlm.nih.gov/pubmed/](https://www.ncbi.nlm.nih.gov/pubmed/)).   

Una buona conoscenza di base della __Biologia Molecolare__ ed in generale delle discipline biologiche di base(e.g. *Fisiologia*, *Biochimica* e *Genetica*) è fondamentale per comprendere e utilizzare al meglio gli strumenti che la Bioinformatica mette a disposizione della nostra attività di ricerca.   

Uno dei principali compiti affidati alla Bioinformatica è archiviare i dati sopra citati, con tutte le informazioni ad essi correlate, in apposite *Banche Dati* o Database in modo da potervi accedere con opportuni programmi di interrogazione (retrieval).  
La consultazione di una banca dati consiste quindi nel formulare una richiesta volta a selezionare un insieme di voci (*entries*) della stessa che soddisfino i nostri criteri di selezione (*query*). Ad esempio possiamo essere interessati a tutte le proteine codificate dal genoma umano (criterio 1), più lunghe di 1,000 amminoacidi (criterio 2) e che contengano uno specifico dominio catalitico (criterio 3), quindi in questo esempio i tre criteri riportati saranno combinati per intersezione.  
I sistemi di retrieval consentono appunto di effettuare queries combinando diversi criteri tra loro utilizzando una serie di operatori logici quali intersezione (**AND**), unione (**OR**) o esclusione (**BUT NOT**).  
  
Lo sviluppo della Bioinformatica ed in generale degli strumenti bioinformatici è stato affiancato da un enorme sviluppo della rete internet (o **world wide web**). Lo sviluppo della rete internet ha reso possibile la “globalizzazione” delle informazioni.  
E’ sufficiente avere un computer connesso alla rete per accedere, da una qualunque località, a tutte le informazioni archiviate in qualunque altro computer in rete sulla terra. 

Gli indirizzi internet sopra riportati (noti come *URL* o *uniform resource locators*) consentono l’accesso, utilizzando un Browser come *Safari*, *Chrome* o *Firefox* a documenti elettronici attraverso il protocollo *http/https* (*HyperText Transfer Protocol*).  
La maggior parte delle risorse bioinformatiche, sia banche dati che programmi di analisi, sono disponibili ai ricercatori – normalmente in forma gratuita - sulla rete internet.   
  
Prima di iniziare queste Esercitazioni è opportuno ricordare alcuni concetti base di biologia molecolare riguardanti:   
•	la struttura di un gene (promotore, ORF, esone, introne, siti di splicing, segnale di poliadenilazione, etc);  
•	la struttura di un trascritto (UTR, ORF, sequenza di Shine e Dalgarno, sito di poliadenilazione, etc);  
•	gli elementi di una proteina (peptide segnale, segmenti transmembrana, siti di fosforilazione, domini);   
•	le differenze di funzione e struttura tra un gene e uno pseudogene;  
•	la differenza tra sequenze genomiche e Expressed Sequence Tag (EST).  
  
Letture consigliate:  
- Valle G. et al. Introduzione alla Bioinformatica (Zanichelli Ed.) – pag. 1-6.  
- Citterich M. et al. Fondamenti di Bioinformatica (Zanichelli)


## Programma
### Esercitazione 1 (03-04/12/2019)
### Banche dati: definizioni generali e sistemi di retrieval
- [X] [Definizione di Database e struttura delle entry **GenBank**](Banche_dati/banche_dati.md)  
- [X] [Sistemi di retrieval](Banche_dati/retrieval.md)  
- [X] [PubMed](Banche_dati/pubmed.md)  
### Esercitazione 2 (17-18/12/2019)
### Allineamento tra sequenze
- [X] [Allineamento](./Allineamento_tra_sequenze/allineamento.md)
- [X] [Utilizzo di BLAST e BLAT per l'analisi genomica](./Allineamento_tra_sequenze/blast_genomico.md)
### Esercitazione 3 (07-08/12/2020)
### Genome Browser
- [ ] [ENSEMBL](./Genome_Browser/Ensembl.md)
- [ ] [Utilizzo di BLAST e BLAT per l'analisi genomica](./Genome_Browser/UCSC.md)


