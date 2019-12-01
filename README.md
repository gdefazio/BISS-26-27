# **ESERCITAZIONI PRATICHE DEL CORSO DI BIOINFORMATICA ED ANALISI FUNZIONALE DEL GENOMA**  

## ***Introduzione alla Bioinformativa***
Prima di addentrarci nello studio di questa disciplina è opportuno soffermarsi su quale sia la definizione più appropriata e delinearne i principali ambiti di ricerca e applicazione.  
Nel corso degli anni sono state proposte numerose definizioni che possono essere così sintetizzate:  

***La Bioinformatica si occupa della ricerca, dello sviluppo e dell’applicazione di approcci computazionali per l’interpretazione di dati biologici.***  
**Questi includono l’informazione genetica racchiusa nei genomi e le modalità della loro espressione (trascrittoma, proteoma, microbioma, pathways metabolici, ecc.).**   
La ricerca nel settore della Bioinformatica si occupa quindi di sviluppare gli approcci più appropriati per collezionare i dati biologici in apposite banche dati, di mettere a punto gli strumenti più idonei per la loro interrogazione e di sviluppare metodologie per la loro analisi con l’obiettivo di contribuire alla comprensione dei meccanismi molecolari alla base della vita.   

La Bioinformatica è per sua natura **multidisciplinare** richiedendo il concorso di competenze diverse (Biologia Molecolare, Biochimica, Fisiologia, Genetica, Informatica, Matematica, Statistica, Chimica, Fisica, Ingegneria, ecc.) ed ha applicazioni pratiche in vasti settori della scienza.   

L’aumento esponenziale dei dati biologici, cui assistiamo in questi anni a seguito del completamento di numerosi progetti di sequenziamento genomico (incluso il genoma umano) e dell’avvio di numerosi progetti su larga scala per lo studio del trascrittoma, del proteoma e del microbioma di numerosi organismi, comporta una crescente importanza della Bioinformatica in tutti i settori della ricerca a livello biomolecolare. [](https://www.ncbi.nlm.nih.gov/genbank/statistics/)
  
I principali tipi di dati biologici sono:  
•	Sequenze nucleotidiche (vedi [](https://www.ncbi.nlm.nih.gov/guide/dna-rna/) per una lista delle risorse di sequenze di DNA o RNA oppure [](http://www.ebi.ac.uk/ena) per un archivio di informazioni sul sequenziamento nucleotidico nel mondo);  
•	Sequenze proteiche (vedi https://www.ncbi.nlm.nih.gov/guide/proteins/ per un elenco di risorse proteiche oppure http://us.expasy.org/sprot/ per informazioni su una delle più importanti risorse di sequenze proteiche, la UniProtKB/Swiss-Prot) 
•	Strutture tridimensionali di proteine ed altre macromolecole (vedi https://www.ncbi.nlm.nih.gov/guide/domains-structures/ per le risorse di domini e strutture molecolari oppure http://www.rcsb.org/pdb/ per la risorsa di macromolecole biologiche PDB) 
•	Dati di espressione (https://www.ncbi.nlm.nih.gov/guide/genes-expression/ per le risorse relative all’espressione dei geni e ai fenotipi correlati)
•	Dati metabolici (http://www.genome.jp/kegg/ per una risorsa sulle relazioni metaboliche tra i geni e i loro prodotti) 
•	Letteratura scientifica (per accedere ad un’importante risorsa di letteratura biomedica https://www.ncbi.nlm.nih.gov/pubmed/) 
  
Una buona conoscenza di base della Biologia Molecolare ed in generale delle discipline biologiche di base(e.g. Fisiologia, Biochimica e Genetica) è fondamentale per comprendere e utilizzare al meglio gli strumenti che la Bioinformatica mette a disposizione della nostra attività di ricerca. 

Uno dei principali compito affidati alla Bioinformatica è archiviare i dati sopra citati, con tutte le informazioni ad essi correlate, in apposite “Banche Dati” o Database in modo da potervi accedere con opportuni programmi di interrogazione (retrieval). 

La consultazione di una banca dati consiste quindi nel formulare una richiesta volta a selezionare un insieme di voci (entries) della stessa che soddisfino i nostri criteri di selezione (query). Ad esempio possiamo essere interessati a tutte le proteine codificate dal genoma umano (criterio 1), più lunghe di 1,000 amminoacidi (criterio 2) e che contengano uno specifico dominio catalitico (criterio 3), quindi in questo esempio i tre criteri riportati saranno combinati per intersezione. I sistemi di retrieval consentono appunto di effettuare queries combinando diversi criteri tra loro utilizzando una serie di operatori logici quali intersezione (AND), unione (OR) o esclusione (BUT NOT).
  
Lo sviluppo della Bioinformatica ed in generale degli strumenti bioinformatici è stato affiancato da un enorme sviluppo della rete internet (o world wide web). Lo sviluppo della rete internet ha reso possibile la “globalizzazione” delle informazioni. E’ sufficiente avere un computer connesso alla rete per accedere, da una qualunque località, a tutte le informazioni archiviate in qualunque altro computer in rete sulla terra. 
Gli indirizzi internet sopra riportati (noti come URL o uniform resource locators) consentono l’accesso, utilizzando un Browser come Safari, Chrome o Firefox a documenti elettronici attraverso il protocollo http (HyperText Transfer Protocol). La maggior parte delle risorse bioinformatiche, sia banche dati che programmi di analisi, sono disponibili ai ricercatori – normalmente in forma gratuita - sulla rete internet. 
  
Prima di iniziare questo Corso è opportuno ricordare alcuni concetti base di biologia molecolare riguardanti: 
  
•	la struttura di un gene (promotore, ORF, esone, introne, siti di splicing, segnale di poliadenilazione, etc), 
•	la struttura di un trascritto (UTR, ORF, sequenza di Shine e Dalgarno, sito di poliadenilazione, etc) 
•	gli elementi di una proteina (peptide segnale, segmenti transmembrana, siti di fosforilazione, domini), 
•	le differenze di funzione e struttura tra un gene e uno pseudogene, 
•	la differenza tra sequenze genomiche e Expressed Sequence Tag (EST). 
  
Letture consigliate: 
  
Valle G. et al. Introduzione alla Bioinformatica (Zanichelli Ed.) – pag. 1-6.
Citterich M. et al. Fondamenti di Bioinformatica (Zanichelli)



## Programma
## Esercitazione 1
### Morning
- [x] [Introduction to the course idea and Instructors](https://drive.google.com/open?id=1oLH_W-5IMYIHZoe9Kr7kPdYyK4PaAy0r3YMB_7d5nEY):
    - [Anna Sandionigi](https://scholar.google.it/citations?hl=it&user=Kotdy6kAAAAJ)
    - [Bruno Fosso](https://scholar.google.it/citations?user=TBeT9pIAAAAJ&hl=it)
    - []()

- [x] [**Brief introduction** about __Metagenomics__ concepts. *What are we going to talk about?*](https://docs.google.com/presentation/d/1JafDY-zalbqZkEA83MLhLHNrCJZ_aqDlfzt22FNKadw/edit?usp=sharing)
- [x] [**Illumina sequencing technology** and how the sequences are obtained;](https://drive.google.com/open?id=1duo88-s5jdFg_dPnaXAsa6-c9YpeSpYhVbpRw1K0M3g)
- [x] [How to connect to the Amazon EC2 service](unix_short_tutorial/how_to_connect.md)  
- [x] [A brief introduction about **Anaconda** and the **BASH** environment;](https://docs.google.com/presentation/d/1OlNpcup5JsqLR0-DX9q0tG-GFBEIvNgDCKD3BVSfung/edit?usp=sharing)


### Afternoon
- [x] Laptop setting;
- [x] [Introduction to the **BASH** shell and **FASTQ** format](unix_short_tutorial/Readme.md)
- [x] [Introduction to the **QIIME2** objects, Importing and visualizing raw data](unix_short_tutorial/Readme.md)


## Day 2
### Morning
- [x] [Experimental Design](https://drive.google.com/open?id=1tD3j6U2lBpnC87F9L4lgtcHxOa-cpfTNM1L6s75YwKA)
- [x] [**Key concept: OTU or ASV**;](https://docs.google.com/presentation/d/1X8s-J-gOjWvXYDAnRh39_nwKuLJtU0l0fG2MrLXyUpo/edit?usp=sharing)

### Afternoon
- [x] [ Denoising and **DADA2**](16S_ITS_tutorial/readme.md);
- [x] [Taxonomic assignment](https://drive.google.com/open?id=1oHTCBiJ1HoHAREZIN2NVSHnC63QphDUJr_cPbgqgDs4)
- [x] [ITS group](ITS/readme.md)


## Day 3
### Morning

- [x] [Taxonomy assignment: **VSEARCH** vs **classify-sklearn**](16S_ITS_tutorial/readme.md#step-3-summarizing-feature-table-and-feature-data);
- [x] [Diversity Analysis](https://drive.google.com/open?id=1aT_z18Iv8X1V0pv--9GqA1kacQl4NSWWH0_Z0LkBgRE)
- [x] [Alpha and Beta Diversity in QIIME2](16S_ITS_tutorial/readme.md#step-6-analyzing-alpha-and-beta-diversities)

### Afternoon
- [x] [R tutorial](https://www.datacamp.com/courses/free-introduction-to-r)
- [x] [Downstream Analysis - presentation](https://drive.google.com/open?id=1EgfBma7D2i7zZrEbKBJluEKXt0eHzmV4)
- [x] [Downstream Analysis - hands-on](DownstreamAnalyses/README.md)

## Day 4
### Morning
- [x] [Please answer to this survey](https://docs.google.com/forms/d/e/1FAIpQLSepDw5g--_pqdqH4BjUU5XNdr6i9kDh08zAxmgZB00Q8EvWcg/viewform)
- [x] [Downstream Analysis - hands-on...Again using R](DownstreamAnalyses/README.md) :fearful:


### Afternoon
- [x] [Downstream Analysis - hands-on...Again using R](DownstreamAnalyses/README.md) 

## Day 5
### Morning
- [x] []()
- [x] [Contamination](https://drive.google.com/open?id=1MQHnrjpFXBbaLYbRzD-KEJ3l6HnPSg6h) 
