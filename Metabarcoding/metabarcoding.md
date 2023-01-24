Metabarcoding
==============
- [Introduzione](#introduzione)
- [Metabarcoding approach](#metabarcoding-approach)
- [Analisi di dati reali](#analisi-di-dati-reali)
  - [Preparazione dell'area di lavoro](#preparazione-dellarea-di-lavoro)
  - [Importazione dei dati](#importazione-dei-dati)
  - [Denoising](#denoising)
  - [Classificazione tassonomica](#classificazione-tassonomica)
  - [Alpha e Beta Diversità](#alpha-e-beta-diversita)
  - [Analisi comparativa tra le due tipologie tumorali](#analisi-comparativa-tra-le-due-tipologie-tumorali)


# Introduzione
L'approccio metagenomico si basa sull'analisi del materiale genetico totale (**metagenoma**) direttamente estratto da un 
campione ambientale (Kunin et al., 2008; Wooley et al., 2010).  
Anche se il metagenoma consiste nell'intero contenuto genetico delle specie viventi in un determinato habitat, questo 
nuovo approccio è applicato principalmente per indagare sulle comunità microbiche.  
Considerando che circa il **99%** delle specie batteriche non possono essere isolate e coltivate mediante tecniche 
standard di laboratorio (Staley and Konopka, 1985), l'approccio metagenomico, che non prevede alcuna procedura di 
coltivazione, offre uno strumento senza precedenti per allargare la conoscenza del mondo microbico. L’importanza di 
poter di poter accedere alla porzione microbica “nascosta” risiede nel fatto che circa i due terzi della biodiversità 
presente sulla terra siano composti da microorganismi (Singh et al., 2009).  
I microorganismi, i loro genomi e le iterazioni che tra loro stabiliscono in ogni ambiente che colonizzano sono definiti con il termine **microbiota**.  
Il grande interesse verso le comunità microbiche è dato dal fatto che esse sono capaci di colonizzare qualsiasi habitat, dal terreno alle acque oceaniche, compreso il corpo umano.  
Proprio considerando il corpo umano, la composizione del microbioma cambia a seconda del sito anatomico o dell’età del soggetto (Turnbaugh et al., 2013), ma anche in base allo stile di vita.   
Inoltre, l’avvento delle tecnologie di sequenziamento di nuova generazione a elevato throughput (**Next-Generation Sequencing, NGS**) (Nowrousian, 2010) ha sostenuto lo studio di tutti i possibili habitat.  
La metagenomica può effettuare il profiling del microbioma mediante due approcci:  
1.	**Classificazione tassonomica**: in questo caso l'obiettivo principale è quello d' identificare gli organismi viventi nell' ambiente (Simon and Daniel, 2011), possibilmente a livello di specie. Questa metodologia richiede, dopo il sequenziamento, una fase di classificazione per assegnare le read ai rispettivi gruppi tassonomici;  
2.	**Caratterizzazione funzionale**: l'obbiettivo principale è quello di rivelare il repertorio di funzioni genetiche della comunità in oggetto d’indagine mediante analisi del DNA o RNA totale o sistemi di espressione eterologhi (solitamente E. coli) (Prakash and Taylor, 2012; Simon and Daniel, 2011).  
  
Quanto al metodo di sequenziamento, sono utilizzati due approcci principali:  
•	L’analisi dell’intero metagenoma/metatranscrittoma basata sul sequenziamento **shotgun** del DNA/RNA totale estratto dal campione. Quest’approccio consente di ottenere sia informazioni tassonomiche che funzionali ma è notevolmente costoso in termini di sequenziamento e analisi computazionale.  
•	La strategia **amplicon-based** o **metabarcoding** che si basa sull' amplificazione selettiva di specifici marcatori tassonomici utilizzando coppie di **primer universali** capaci di essere efficienti su grandi gruppi tassonomici (ad esempio batteri, funghi, ecc) ed il successivo sequenziamento high-throughput delle librerie di ampliconi ottenute.  
    Quest’approccio può fornire informazioni solo sulla composizione tassonomica del campione ma con superiore capacità d’identificazione e risoluzione a livello di specie.  
    Inoltre, risulta meno costoso in termini di sequenziamento e analisi computazionale.  
    Le regioni marker più utilizzate includono:  
    * diverse combinazioni delle regioni iper-variabili del gene del **rRNA 16S (nei batteri)**;  
    * gli **spaziatori interni trascritti (ITS) dei geni del cluster degli RNA ribosomiali (nei funghi)**;  
    * specifiche porzioni del gene della Citocromo c ossidasi 1 mitocondriale (nei Metazoa).  
    
## Metabarcoding approach
[Giusto un po' di teoria](https://docs.google.com/presentation/d/1fP-sWpi_G3dnXOL_VB-ohXLCiaspA-NLwcgfB1BRckM/edit?usp=sharing).  
Scopo dell’esercitazione odierna è l’analisi del microbioma umano attraverso l’approccio di metabarconding, che possiamo idealmente suddividere in 5 step principali:  
1.	Raccolta dei campioni;  
2.	Estrazione del metagenoma (insieme dei genomi degli \[micro\]organismi che condividono lo stesso ambiente);  
3.	Amplificazione del marker tassonomico;  
4.	Sequenziamento;  
5.	Analisi bioinformatica dei dati.  
![picture1](Picture1.png)  
**Figura 1: rappresentazione schematica degli step che caratterizzano l’approccio metabarcoding.**

Un marcatore genetico di specie ideale dovrebbe avere le seguenti caratteristiche:  
1.	essere ubiquitario, o almeno largamente condiviso nel range tassonomico di interesse;  
2.	essere abbastanza variabile da consentire la discriminazione ai più profondi livelli tassonomici;  
3.	essere affiancato per regioni altamente conservate adatte per il disegno primer universali;  
4.	avere una dimensione paragonabile ai limiti di lunghezza delle piattaforme NGS attuali.  
![picture2](Picture2.png)  
*Figura 2: rappresentazione della variabilità del gene per l’rRNA 16S nei procarioti.*

# Analisi di dati reali
Per questa esercitazioni utilizzeremo dei dati di ricente pubblicazione [Ravegnini et al. 2020](https://www.mdpi.com/1422-0067/21/24/9735).  
Lo scopo dello studio riguadava la caratterizzazione del microbioma gastrico in soggetti affetti tumore (*Gastric cancer, GC*).  
I GC sono la quinta forma tumorale per incidenza nel monda e la terza causa di morte per tumore.  L'avvento della genomica ha permesso di capire come in realtà si tratti di una complessa rappresentazione di patologie, dove differenti mutazioni danno origine a diverse forme tumorali.  
Noi studieremo i dati di soggetti affetti da:  
    - **ADC**: Adenocarcinoma. E' la forma più comune e rappresenta il 95% dei GC. Ha solitamente origine nella mucosa  
    - **SRCC**: Single-ring Cell Carcinoma. Forma più rara che si origine nelle cellule ghiandolari.  
Per i nostri scopi analizzeremo 20 campioni:
* 10 campioni ADC;  
* 10 campioni SRCC.  


***Lo scopo di questa esercitazione è capire se via siano differenze tra il microbioma gastrico dei soggetti affetti da ADC e SRCC.***  
 
I dati sono stati ottenuti amplificando la regione iper-variabile V3-V4 del rRNA 16S e successivamente sequenziando gli ampliconi in modalità paired-end (PE) 2x300 con piattaforma Illumina MiSeq®.  
Effettueremo tutte le analisi utilizzando il tool [**QIIME2**](https://qiime2.org/).  
Questo tool implementa sia un sistema che traccia l'orgine dei dati e la loro elaborazione che uno per la loro visuallizzazione, chiamato [**QIIME 2 View**](https://view.qiime2.org/).  

### Preparazione dell'area di lavoro
* Come prima operazione occorre accedere al server con le credenziali che vi sono state assegnate;
* Successivamente va create la cartella `Ravegnini_et_al` e bisogna posizionarsi al suo interno:  
    `mkdir Ravegnini_et_al && cd Ravegnini_et_al`
* Adesso va attivato l'ambiente virtuale in cui è installato **QIIME2**:  
    `source /opt/miniconda3/bin/activate qiime2-2020.11` 
* Creiamo una cartella che mantenga i dati temporanei e indichiamo al sistema operativo di utilizzarla:  
    ```
    mkdir tmp
    export TMPDIR="$PWD/tmp"
    ```  
* Copiamo i dati all'interno della nostra cartella:  
    `cp /home/share/microbiome_analysis/metadata.tsv .`               
A questo punto abbiamo completato tutte le operazioni preliminari necessarie per preparare l'ambiente di lavoro.  
Possiamo procedere con le analisi.  

### Importazione dei dati
* Importiamo i dati in QIIME2. _Al fine di limitare la quantità di disco occupato non importerete i dati nella vostra cartella_:  
    
    > qiime tools import \
       --type 'SampleData[PairedEndSequencesWithQuality]' \
       --input-path /home/share/microbiome_analysis/input_data \
       --input-format CasavaOneEightSingleLanePerSampleDirFmt \
       --output-path demux-paired-end.qza
      
* Creiamo un file di visualizzazione (estensione *qzv*) per valutare la qualità dei nostri dati:  
    ```
    qiime demux summarize \
    --i-data  /home/share/microbiome_analysis/demux-paired-end.qza \
    --o-visualization demux-paired_end.qzv
    ```
* Scarichiamo il file `demux-paired_end.qzv` e visualizziamolo con QIIME2 view.  
    * Come valutiamo la qualità del sequenziamento?  

### Denoising
* Effettuiamo il **Denoising** dei dati:  
    Il **Denoising** (letteralmente eliminazione del rumore di fondo (*noise*)) è una procedura che permette di riconoscere il rumore introdotto dalla PCR e dal sequenziamento.  
      
    Il trimming delle sequenze PE: 
    ![read](read.png)  
    
    Prima di decidere se trimmare le sequenze al 3' e di quanto trimmare dobbiamo valutare quanto le due read si sovrappongono. Per farlo possiamo tenere conto della formula:  
    ![sovrapposizione](sovrapposizione.png)  
    Dove:  
        - R è la lunghezza nominale delle read;
        - L è la lunghezza media dell'amplicone.  
    Nel nostro caso l'amplicone ha una lunghezza media di 560 nt, per cui: **S = 2*300 - 500 = 600 - 500 = 100**.  
    
    <details><summary></summary>
    <p>
    <b>In considerazione della qualità delle sequenze e della possibile regione di sovrapposizione conviene limitare il trimming alle ultime posizioni delle reads.</b>
    </p>
    </details>
    
     >nohup qiime dada2 denoise-paired \
          --i-demultiplexed-seqs demux-paired-end.qza \
          --p-trunc-len-f 270 \
          --p-trunc-len-r 260 \
          --p-trim-left-f 20 \
          --p-trim-left-r 20 \
          --p-max-ee-f 4 \
          --p-max-ee-r 5 \
          --p-n-threads 20 \
          --o-table table_16S.qza \
          --o-representative-sequences rep-seqs_16S.qza \
          --o-denoising-stats denoising-stats_16S.qza &  
 
     Essendo una operazione molto lunga abbiamo già effettuato il denoising. Dovete solo copiare i file:  
    `cp -r /home/share/microbiome_analysis/{rep-seqs_16S.qza,denoising-stats_16S.qza,table_16S.qza} .`   

* Andiamo a creare dei file di visualizzazione per verificare come sia andata la procedura di **Denoising**:  
    ```
    qiime feature-table summarize \
       --i-table table_16S.qza \
       --o-visualization table_16S.qzv \
       --m-sample-metadata-file metadata.tsv 
    ```
    ```
    qiime feature-table tabulate-seqs \
        --i-data rep-seqs_16S.qza \
        --o-visualization rep-seqs.qzv
    ```
    ```
    qiime metadata tabulate \
        --m-input-file denoising-stats_16S.qza \
        --o-visualization denoising-stats_16S.qzv
    ```
  
* Scarichiamo i file `table_16S.qzv`, `denoising-stats_16S.qzv` e `rep-seqs.qzv` e visualizziamoli con QIIME2 view.  

### Classificazione tassonomica  
* Effettuiamo la classificazione tassonomica:  
    >nohup qiime feature-classifier classify-sklearn \
      --i-classifier /home/share/microbiome_analysis/silva-138-99-515-806-nb-classifier.qza \
      --i-reads rep-seqs_16S.qza \
      --o-classification taxonomy_16S_SKLEARN.qza &
    
    Essendo una operazione molto lunga abbiamo già effettuato la classificazione tassonomica. Dovete solo copiare i file:  
    `cp -r /home/share/microbiome_analysis/taxonomy_16S_SKLEARN.qza .`
    
* Adesso andiamo a generare dei file *qzv* che ci permettano di valutare i risultati della classificazione tassonomica:  
    ```
    qiime metadata tabulate \
        --m-input-file taxonomy_16S_SKLEARN.qza \
        --o-visualization taxonomy_16S_SKLEARN.qzv
    ```
    ```
    qiime taxa barplot \
        --i-table table_16S.qza \
        --i-taxonomy taxonomy_16S_SKLEARN.qza \
        --m-metadata-file metadata.tsv \
        --o-visualization taxa-bar-plots_16S_SKLEARN.qzv
    ```

* Scarichiamo i file `taxonomy_16S_SKLEARN.qzv` e `taxa-bar-plots_16S_SKLEARN.qzv` e visualizziamoli con QIIME2 view.  

### Alpha e Beta Diversita'
La Diversità è una misura della complessità del sistema che stiamo osservando, in funzione del numero di oggetti e della loro abbondanza relativa.  
![diversità](diversita.png)

In particolare:  
- **alpha**: diversità intra-campione. Si possono utilizzare diverse metriche:- *Richness*: rappresenta il numero di specie differenti osservate in una comunità biologica;
  - *Eveness*: indica quanto sia uniforme la comunità osservata;
  - *Shannon Index*: è una misura quantitativa della richezza di specie;  
              ![shannon](shannon.gif)  
  - *Faith's Phylogenetic Diversity*: una misura qualitativa della richness della comunità in esame che tiene conto delle relazioni filogenetiche.  
- **beta**: diversità inter-campione: utilizziamo delle misure che indicano quanto differenti sono due comunità. Queste misure non fanno altro che andare a compare i campioni a coppie, per cui alla fine dell'analisi si ottiene una matrice che indica la dissimilarità tra ciascuna coppia di campioni. Esistono diverse tipologie di metriche per calcolare la Beta diversità:  
  - Distanza di **Jaccard**: una misura qualitativa della dissimilarità;  
              ![jaccard dissimilarity](Jaccard-Dissimilarity.gif)  
              ![jaccard similarity](Jaccard_similarity.gif)  
              X e Y rappresentano i campioni in analisi ed in particolare le specie osservate. Quindi la misura tiene conto solo del fatto che una specie sia osservata o meno e non della sua abbondanza.   
  - Distanza di **Bray-Curtis**: una misura quantitativa della dissimilarità;  
              ![bray curtis](bray_curtis.gif)  
              Dove:  
                  - *i* e *j* sono i due campioni in analisi;  
                  - S<sub>i</sub> e S<sub>j</sub> rappresentano la somma delle conte delle specie osservate nei siti *i* e *j*;  
                  - C<sub>ij</sub>: E' la somma delle conte più basse delle specie osservate in entrambe i siti.  
  - Distanza *unweighted UniFrac*: una misura qualitativa della dissimilarità che incorpora le relazioni filogenetiche tra le ASV;  
  - Distanza *weighted UniFrac*: una misura quantitativa della dissimilarità che incorpora le relazioni filogenetiche tra le ASV;  
- **gamma**: diversità totale.  
   
* Prima di procedere con le misure di diversità dobbiamo costruire un albero filogenetico a partire dalle ASV ottenute.  
    ```
    qiime phylogeny align-to-tree-mafft-fasttree \
      --i-sequences rep-seqs_16S.qza \
      --o-alignment aligned-rep-seqs_16S.qza \
      --o-masked-alignment masked-aligned-rep-seqs_16S.qza \
      --o-tree unrooted-tree_16S.qza \
      --p-n-threads 1 \
      --o-rooted-tree rooted-tree_16S.qza
    ```  
* Al fine di poter comparare i dati ottenuti li dobbiamo **normalizzare**. La procedura di Normalizzazione utilizzata per i dati del microbioma è la **Rarefazione**.  
  Questa procedura si basa sulla scelta di un valore di rarefazione (*sampling depth*) a cui tutti i campioni saranno ricondotti. In pratica, si effettua un campionamento senza reimmissione, fino a raggiungere il valore di rarefazione prescelto.  
  Tutti i campioni con conte al di sotto del sampling depth saranno scartati.  
  ```
  qiime diversity alpha-rarefaction \
      --i-table table_16S.qza \
      --i-phylogeny rooted-tree_16S.qza \
      --p-max-depth 50000 \
      --p-min-depth 1000\
      --m-metadata-file metadata.tsv \
      --o-visualization alpha-rarefaction.qzv
  ```  
  
* Passiamo alla stima degli indici di diversità
    ```
    qiime diversity core-metrics-phylogenetic \
      --i-phylogeny rooted-tree_16S.qza \
      --i-table table_16S.qza \
      --p-sampling-depth 15000 \
      --m-metadata-file metadata.tsv \
      --p-n-jobs-or-threads 1 \
      --output-dir core-metrics-results_16S
    ```  
  
* Verifichiamo se vi siano delle differenze significative tra gli indici di alpha diversità:  
    ```  
    qiime diversity alpha-group-significance \
      --i-alpha-diversity core-metrics-results_16S/shannon_vector.qza \
      --m-metadata-file metadata.tsv \
      --o-visualization core-metrics-results_16S/shannon-Condition-significance_16S.qzv
    ```
  
    ```
    qiime diversity alpha-group-significance \
      --i-alpha-diversity core-metrics-results_16S/faith_pd_vector.qza \
      --m-metadata-file metadata.tsv \
      --o-visualization core-metrics-results_16S/faith_pd-Condition-significance.qzv
    ```  
  
* Verifichiamo se vi siano delle differenze significative tra gli indici di beta diversità:  
    ```
    qiime diversity beta-group-significance \
      --i-distance-matrix core-metrics-results_16S/unweighted_unifrac_distance_matrix.qza \
      --m-metadata-file metadata.tsv \
      --m-metadata-column type \
      --o-visualization core-metrics-results_16S/unweighted-unifrac-Condition-significance.qzv \
      --p-pairwise
    ```
  
    ```
    qiime diversity beta-group-significance \
      --i-distance-matrix core-metrics-results_16S/weighted_unifrac_distance_matrix.qza \
      --m-metadata-file metadata.tsv \
      --m-metadata-column type \
      --o-visualization core-metrics-results_16S/weighted-unifrac-Condition-significance.qzv \
      --p-pairwise
    ```
    
    ```
    qiime diversity beta-group-significance \
      --i-distance-matrix core-metrics-results_16S/bray_curtis_distance_matrix.qza \
      --m-metadata-file metadata.tsv \
      --m-metadata-column type \
      --o-visualization core-metrics-results_16S/bray_curtis-Condition-significance.qzv \
      --p-pairwise
    ```  

### Analisi comparativa tra le due tipologie tumorali  
Utilizzeremo [**ANCOM (analysis of composition of microbiomes)**](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4450248/) per andare a effettuare una analisi comparativa tra le due tipologie tumorali analizzate.  
1. Abbiamo detto che la tabella delle ASV è ricca in zeri (**zero inflated**). Ancom aggiunge delle _pseudo-conte_ per eliminare gli zeri.  

    ```
    qiime composition add-pseudocount \
      --i-table table_16S.qza \
      --o-composition-table comp-table.qza
    ```
2. effettuiamo l'analisi comparativa:  
    ```
    qiime composition ancom \
      --i-table comp-table.qza \
      --m-metadata-file metadata.tsv \
      --m-metadata-column type \
      --o-visualization ancom-type.qzv
    ```
Abbiamo effettuato la comparazione a livello di ASV ma potremmo essere interessati a comparare a livelli tassonomici superiori.  
1. Dobbiamo raggruppare i dati al livello tassonomico d' interesse. In questo caso il 6 livello della tassonomia SILVA (genere).  
    ```
    qiime taxa collapse \
      --i-table table_16S.qza \
      --i-taxonomy taxonomy_16S_SKLEARN.qza \
      --p-level 6 \
      --o-collapsed-table table-l6.qza
    ```  
2. aggiungiamo le pseudoconte.  
    ```
    qiime composition add-pseudocount \
      --i-table table-l6.qza \
      --o-composition-table comp-table-l6.qza
    ```  
3. effettuiamo l' analisi comparativa
    ```
    qiime composition ancom \
      --i-table comp-table-l6.qza \
      --m-metadata-file metadata.tsv \
      --m-metadata-column type \
      --o-visualization ancom-type-l6.qzv
    ```

***Se volessimo effettuare la stessa analisi a livello di famiglia, cosa dovremmo fare?***  

A. Aggreghiamo le conte a livello di famiglia (5):  
   ```
    qiime taxa collapse --i-table table_16S.qza --i-taxonomy taxonomy_16S_SKLEARN.qza \
      --p-level 5 --o-collapsed-table table-l5.qza
   ```  
B. Aggiungiamo le pseudo-conte:  
   ```
   qiime composition add-pseudocount --i-table table-l5.qza --o-composition-table comp-table-l5.qza
   ```
C. Applichiamo ANCOM:  
   ```
    qiime composition ancom --i-table comp-table-l5.qza --m-metadata-file metadata.tsv \
      --m-metadata-column type --o-visualization ancom-type-l5.qzv
   ```


## Letture consigliate    
- Michael C. Whitlock, Dolph Schluter ANALISI STATISTICA DEI DATI BIOLOGICI - Capitolo 13  

[Programma Esercitazioni](../README.md) 