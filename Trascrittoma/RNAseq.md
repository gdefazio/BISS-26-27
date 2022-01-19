---
title: RNA SEQ
---

# Introduzione

L' identificazione dei trascritti e la quantificazione dell' espressione genica sono due attività fondamentali della biologia molecolare sin
dalla scoperta dell'RNA e della sua funzione d' intermediario tra il custode dell' informazione, _il genoma_, e l' applicazione delle specifiche
funzioni codificate all' interno di ciascun trascritto prodotto da ciascun gene [1].

L' avvento delle tecnologie di sequenziamento di nuova generazione ha  permesso di mettere a punto delle metodiche per l'investigazione del
trascrittoma.

**NB: parte degli step presentati nella nostra procedura sono già stati
effettuati. Inoltre, più che dell'analisi bioinformatica ci focalizzeremo
sull'analisi statistica dei dati di trascrittomica.**

L' analisi statistica dei dati che andremo ad analizzare sarà effettuata
utilizzando R, un ambiente sviluppato appositamente per lo sviluppo e
l' applicazione di pacchetti statistici. Iniziamo installando R sui
vostri computer. E' possibile scaricare la versione adatta al vostro
sistema operativo utilizzando il seguente
[link](http://cran.mirror.garr.it/mirrors/CRAN/).  
Per semplicità utilizzeremo la versione di R già installata sulle macchine virtuali.  

# Caso Studio

Analizzeremo una parte dei dati elaborati nel paper [Annese et al. 2018, Scientific Reports](https://www.nature.com/articles/s41598-018-22701-2).
Lo studio ha riguardato l' applicazione di metodologie NGS sia per l' analisi del trascrittoma che del mirnoma.    
Noi ci soffermeremo sulla comparazione dei dati di RNA-seq tra soggetti sani e affetti da Alzheimer.  
Analizzeremo 12 campioni:  

|Sample|Condition|
|:-:|:-:|


# Mapping su genoma di riferimento 

Durante l'esercitazione per il Variant Calling abbiamo parlato del
programma di mapping chiamato BWA (Burrows-Wheeler Alignment tool) , che
utilizza un approccio basato sulla combinazione della trasformata di
Burrows-Wheeler
([https://en.wikipedia.org/wiki/Burrows--Wheeler_transform](https://en.wikipedia.org/wiki/Burrows–Wheeler_transform))
e la costruzione di FM index (<https://en.wikipedia.org/wiki/FM-index>).
Abbiamo sottolineato come questo approccio permetta di velocizzare il
processo di mapping tanto da poter mappare milioni di reads in
pochissime ore.

Quando, però, dobbiamo procedere all'analisi di un trascrittoma si la
complessità del problema è incrementata dalla presenza di una ulteriore
difficoltà computazionale: le read posso mappare sulle giunzioni di
splicing e per questo vanno utilizzati degli accorgimenti per
considerare il fatto che un allineamento possa contenere una regione
genomica non rappresentata nelle nostre read (le regioni introniche). Un
programma che permette di ovviare a questa problematica e STAR ^3^
utilizzando un approccio chiamato Maximal Mappable Prefix MMP (figura2).

![](/Users/brunofosso/Documents/Lezioni_Universita'/import-resources/media/image2.jpeg){width="4.48125in"
height="3.3877121609798775in"}

Figura 2: Approccio MMP

STAR è un programma computazionalmente intensivo, che però permette di
pre-caricare il genoma di riferimento in memoria e poi condividerlo tra
più processi di mapping:

STAR \--genomeDir /home/bfosso/share/MetaShot_reference/Homo_sapiens
\--genomeLoad LoadAndExit

Possiamo procedure al mapping delle nostre read.

-   STAR \--runThreadN 10 \--genomeDir
    /home/bfosso/share/MetaShot_reference/Homo_sapiens \--genomeLoad
    LoadAndKeep \--readFilesIn SRR6458318_va1.fq SRR6458318_va2.fq
    \--outSAMattributes NM \--alignIntronMax 1000000 \--alignIntronMin 1
    \--outFileNamePrefix SRR6458318_data \--sjdbGTFfeatureExon
    /home/bfosso/share/MetaShot_reference/Homo_sapiens/gencode.v21.annotation.gtf.gz

-   STAR \--runThreadN 10 \--genomeDir
    /home/bfosso/share/MetaShot_reference/Homo_sapiens \--genomeLoad
    LoadAndKeep \--readFilesIn SRR6458317_va1.fq SRR6458317_va2.fq
    \--outSAMattributes NM \--alignIntronMax 1000000 \--alignIntronMin 1
    \--outFileNamePrefix SRR6458317_data \--sjdbGTFfeatureExon
    /home/bfosso/share/MetaShot_reference/Homo_sapiens/gencode.v21.annotation.gtf.gz

-   STAR \--runThreadN 10 \--genomeDir
    /home/bfosso/share/MetaShot_reference/Homo_sapiens \--genomeLoad
    LoadAndKeep \--readFilesIn SRR6458316_va1.fq SRR6458316_va2.fq
    \--outSAMattributes NM \--alignIntronMax 1000000 \--alignIntronMin 1
    \--outFileNamePrefix SRR6458316_data \--sjdbGTFfeatureExon
    /home/bfosso/share/MetaShot_reference/Homo_sapiens/gencode.v21.annotation.gtf.gz

Completato il mapping possiamo liberare la porzione di memoria occupata
dal genoma di riferimento:

STAR \--genomeDir /home/bfosso/share/MetaShot_reference/Homo_sapiens
\--genomeLoad Remove

STAR produce un file in formato SAM
(<http://samtools.github.io/hts-specs/SAMtags.pdf>) , che dobbiamo
convertire in BAM (la controparte binaria del file SAM).

-   samtools view -b -S -o SRR6458316_dataAligned.out.bam
    SRR6458316_dataAligned.out.sam

-   samtools view -b -S -o SRR6458317_dataAligned.out.bam
    SRR6458317_dataAligned.out.sam

-   samtools view -b -S -o SRR6458318_dataAligned.out.bam
    SRR6458318_dataAligned.out.sam

Successivamente ordiniamo i file bam e li indicizziamo:

-   samtools sort SRR6458316_dataAligned.out.bam -o
    SRR6458316_dataAligned.out.sorted.bam

-   samtools sort SRR6458317_dataAligned.out.bam -o
    SRR6458317_dataAligned.out.sorted.bam

-   samtools sort SRR6458318_dataAligned.out.bam -o
    SRR6458318_dataAligned.out.sorted.bam

-   samtools index SRR6458316_dataAligned.out.sorted.bam

-   samtools index SRR6458317_dataAligned.out.sorted.bam

-   samtools index SRR6458318_dataAligned.out.sorted.bam

Come per il variant calling dobbiamo eliminare alcuni artefatti della
procedura sperimentale e in particolare, andiamo ad eliminare i
duplicati di PCR.

-   java -jar \$picard MarkDuplicates INPUT=
    SRR6458316_dataAligned.out.sorted.bam OUTPUT= SRR6458316_dep.bam
    METRICS_FILE=metrics.txt

-   java -jar \$picard MarkDuplicates INPUT=
    SRR6458317_dataAligned.out.sorted.bam OUTPUT= SRR6458317_dep.bam
    METRICS_FILE=metrics.txt

-   java -jar \$picard MarkDuplicates INPUT=
    SRR6458318_dataAligned.out.sorted.bam OUTPUT= SRR6458318_dep.bam
    METRICS_FILE=metrics.txt

-   java -jar picard.jar BuildBamIndex INPUT=SRR6458316_dep.bam

-   java -jar picard.jar BuildBamIndex INPUT=SRR6458317_dep.bam

-   java -jar picard.jar BuildBamIndex INPUT=SRR6458318_dep.bam

Sulla base dei dati di mapping andiamo a contare per ciascun gene le
read che vi si allineano contro utilizzando HTSeq-count:

-   htseq-count -f bam -s no -r pos -t gene -i gene_id
    SRR6458316_dep.bam gencode.v21.annotation.gtf \>
    SRR6458318_gene_count

-   htseq-count -f bam -s no -r pos -t gene -i gene_id
    SRR6458317_dep.bam gencode.v21.annotation.gtf \>
    SRR6458317_gene_count

-   htseq-count -f bam -s no -r pos -t gene -i gene_id
    SRR6458318_dep.bam gencode.v21.annotation.gtf \>
    SRR6458316_gene_count

Infine ripuliamo I file prodotti con HTSeq-count ^5^:

-   grep -v GFF SRR6458316_gene_count\|grep -v SAM\|grep -v Warning \>
    SRR6458316_gene_count_cleaned

-   grep -v GFF SRR6458317_gene_count\|grep -v SAM\|grep -v Warning \>
    SRR6458317_gene_count_cleaned

-   grep -v GFF SRR6458318_gene_count\|grep -v SAM\|grep -v Warning \>
    SRR6458318_gene_count_cleaned

Adesso possiamo procedere all' analisi statistica con R. Nella vostra
area di lavoro troverete lo script stat_analysis.R che dovete scaricare
sul vostro computer ed aprire con Rstudio. In questo script sono
eseguiti tutti gli step necessari per confrontare i nostri campioni
utilizzando DESeq2 ^6^.

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
