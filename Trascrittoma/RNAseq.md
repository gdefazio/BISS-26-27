RNAseq
======

# Introduzione

L' identificazione dei trascritti e la quantificazione dell' espressione genica sono due attività fondamentali della biologia molecolare sin
dalla scoperta dell'RNA e della sua funzione d' intermediario tra il custode dell' informazione, _il genoma_, e l' applicazione delle specifiche
funzioni codificate all' interno di ciascun trascritto prodotto da ciascun gene [1].

L' avvento delle tecnologie di sequenziamento di nuova generazione ha permesso di mettere a punto delle metodiche per l'investigazione del
trascrittoma.

**NB: parte degli step presentati nella nostra procedura sono già stati effettuati. Inoltre, più che dell' analisi bioinformatica ci focalizzeremo
sull' analisi differenziale statistica dei dati di trascrittomica.**

L' analisi statistica dei dati che andremo ad analizzare sarà effettuata utilizzando R, un ambiente sviluppato appositamente per lo sviluppo e l' applicazione di pacchetti statistici.
Per semplicità utilizzeremo la versione di R già installata sulle macchine virtuali.  

# Caso Studio

Analizzeremo una parte dei dati discussi nel paper [Annese et al. 2018, Scientific Reports](https://www.nature.com/articles/s41598-018-22701-2).
Lo studio ha riguardato l' applicazione di metodologie NGS sia per l' analisi del trascrittoma che del _mirnoma_.  
Come potrete leggere il lavoro è molto complesso ed ha interessato diversi approcci sperimentali e bioinformatici. Noi ci focalizzeremo sull'analisi di una parte dei dati di trascrittomica.  
In generale, lo scopo del lavoro è stato quello di caratterizzare il profilo trascrittomico di tessuto celebrale di soggetti affetti da **Late Onset Alzheimer Disease (LOAD)**.  
L' AD è la maggiore forma di demenza senile progressiva cronica nel mondo. La neuropatologia della malattia è caratterizzata da perdita di neuroni associata a un diffuso stato infiammatorio e stress ossidativo. 
I marcatori per eccellenza sono gli aggregati intra-neuronali (NFT intraneural fibrillary tangles) della proteina associata ai microtubili **Tau**, che risulta essere iperfosforilata, e la deposizione di placche di
**B-Amiloide** extracellulari, dovute al taglio proteolitico della proteina transmembrana **Amyloid Precursor Protein, APP**.  

Nel lavoro è stato analizzato il profilo trascrittomico di 6 pazienti affetti da LOAD e 6 soggetti sani di sesso maschile e di comparabile età di morte. Inoltre, sono stati inclusi anche 6 campioni di soggetti affetti da *Parkinson Disease (PD)*, 
come una sorta di controllo di patologia neurodegenerativa e per capire quali sono le modificazioni specifiche dell' AD. I campioni utilizzati, ottenuti da una biobanca, riguardano la regione dell'Ippocampo CA1.  
![](./memoria_fig_vol1_006500_004.jpg)
_[](https://www.treccani.it/enciclopedia/memoria_%28Dizionario-di-Medicina%29/)_

Noi ci soffermeremo sulla comparazione dei dati di RNA-seq tra soggetti sani e affetti da Alzheimer.  
Analizzeremo 12 campioni:  

|Sample|Condition|  
|:---:|:----:|  
|SRR-10H_HD|HC|
|SRR-11H_HD|HC|
|SRR-6H_HD|HC|
|SRR-7H_HD|HC|
|SRR-8H_HD|HC|
|SRR-9H_HD|HC|
|SRR-1H_AD|AD|
|SRR-2H_AD|AD|
|SRR-32H_AD|AD|
|SRR-3H_AD|AD|
|SRR-4H_AD|AD|
|SRR-5H_AD|AD|  

La procedura di preparazione delle librerie di sequenziamento ha previsto l' utilizzo del kit **TruSeq Stranded Total RNA** dell'Illumina ed il sucessivo sequenziamento con piattaforma NextSeq 500 con layout 2x100.  
  
# Valutazione della qualità delle sequenze prodotte
Prima di procedere con l' analisi del trascrittoma dobbiamo valutare la qualità delle sequenze ed eventualmente optare per una procedura di trimming.  
Considerato che abbiamo sequenziato 12 campioni e che quindi abbiamo un totale di 24 file fastq da valutare, utilizzeremo, oltre al **FastQC**, un tool chiamato [**MultiQC**](https://multiqc.info).  

**Per questioni di spazio e tempi vedremo direttamente come generare il report prodotto da MultiQC**.  
:bangbang: Quello che è riportato nel Box1 non va eseguito!!! :bangbang:    

:heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign:  
**BOX 1**  
Esecuzione del FastQC:
1. ``mkdir fastqc_output``
2. `fastqc input/*fastq.gz --noextract -o fastqc_output`  

:heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign:  

Adesso possiamo procedere all' esecuzione di MultiQC:  
```
    multiqc /home/share/RNAseq/fastqc_output/
```

Nonostante siamo ampiamente soddisfatti della qualità dei dati effettuiamo comunque il trimming.  
:bangbang: Quello che è riportato nel Box2 non va eseguito!!! :bangbang:  

:heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign:  
**BOX 2**  
Effettuiamo il trimming:  

```
cd input_data

mkdir ../trimmed

for sample in $(cat ../sample_list)
do
  echo $sample
  shopt -s nullglob
  array=($sample*)
  shopt -u nullglob
  echo "${array[@]}"
  sickle pe -f ${array[0]} -r ${array[1]} -o ../trimmed/${sample}_R1_trimmed.fastq.gz -p ../trimmed/${sample}_R2_trimmed.fastq.gz -s ../trimmed/${sample}_unpaired.fastq.gz -q 30 -l 50 -t sanger -g
  unset array
done
```

:heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign: :heavy_minus_sign:  


# Caratterizzazione dei trascritti espressi 
Nel lavoro da cui abbiamo preso i dati che stiamo analizzando è stato utilizzato un approccio bassato sull' allineamento delle reads sul genoma di riferimento.  
Successivamente è stato dedotto il livello di espressione a livello di trascritti e geni.  

Per questa esercitazione utilizzeremo un approccio basato sugli pseudo-allineamenti, con un tool chiamto [**Kallisto**](https://www.nature.com/articles/nbt.3519).  

# Analisi statistica

Eseguiti tutte le applicazioni troverete nella cartella in cui avete
eseguito tutte le analisi il file gene_list.txt che contiene i dati che
analizzeremo utilizzando [AMIGO](http://amigo.geneontology.org/amigo),
per valutare l'arricchimento di specifici GO nei geni che risultano
variati in modo statisticamente significativo.

# Bibliografia

1\. Conesa, A. et al. A survey of best practices for RNA-seq data
analysis. Genome Biol. **17,** (2016).2. Li, H. & Durbin, R. Fast and
accurate short read alignment with Burrows--Wheeler transform.
Bioinformatics **25,** 1754--1760 (2009).3. Dobin, A. et al. STAR:
ultrafast universal RNA-seq aligner. Bioinformatics **29 %6,** 15-21 %&
(2013).4. Li, H. et al. The Sequence Alignment/Map format and SAMtools.
Bioinformatics **25,** 2078--9 (2009).5. HTSeq: Analysing
high-throughput sequencing data with Python --- HTSeq 0.9.1
documentation. Available at:
https://htseq.readthedocs.io/en/release_0.9.1/. (Accessed: 23rd January
2018)6. Anders, S. & Huber, W. Differential expression analysis for
sequence count data. Genome Biol **11 %6,** R106 %& (2010).
