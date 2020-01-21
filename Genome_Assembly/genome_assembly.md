# GENOME ASSEMBLY

## Introduzione
Il sequenziamento di un genoma segue principalmente 4 fasi:  
1. **Isolamento del genoma di interesse**. La qualità del DNA di partenza influenza profondamente il processo di sequenziamento ed assemblaggio del genoma. La qualità del DNA di partenza si misura in termini di **Purezza** e **Integrità strutturale**.  
    * **Purezza**: l’utilizzo di una procedura di estrazione del DNA non appropriata per la matrice di partenza può portare alla presenza di contaminanti come *polisaccaridi*, *proteoglicani*, *proteine*, *metaboliti*, *pigmenti*, etc. Questi influenzano negativamente le procedure di preparazione delle librerie soprattutto per gli approcci PCR-free (**PacBio** e **Nanopore**) e **Mate-Pair** e riducono l’efficienza gli approcci che prevedono passaggi di amplificazione in PCR.  
    * **Integrità strutturale**: la presenza di *fenoli*, *etanolo* e *Sali* (e.g. EDTA) possono danneggiare il DNA. Una inappropriata conservazione del DNA a -20°C in acqua favorisce la degradazione per idrolisi. L’utilizzo di buffer per la conservazione a pH inadeguato favoriscono la formazione di nick.  
2. **Frammentazione del DNA**: La frammentazione può essere ottenuta per *sonicazione*, *nebulizzazione* o *taglio enzimatico*. E’ un passaggio fondamentale perché il DNA presente nelle cellule deve essere frammentato nel modo più casuale possibile al fine di leggere ogni nucleotide ogni nucleotide del genoma ottenendone la migliore rappresentazione;  
3. **Sequenziamento**. La profondità del sequenziamento influenza profondamente la qualità di un assemblaggio. Si utilizza il concetto di coverage per indicare che il numero di volte che in media viene osservato un nt. Quindi una stima della dimensione del genoma è fondamentale per settare adeguatamente i parametri di sequenziamento.  
4. **Analisi Bioinformatica e assemblaggio del genoma**.  
Con il termine **assemblaggio** intendiamo l’operazione di ricostruzione della sequenza completa delle molecole di DNA (cromosomi, organelli e plasmidi) presenti in una cellula.  
Tecnicamente l’operazione consiste nella concatenazione delle read ottenute con il sequenziamento al fine di ottenere dei contigui (**contig** in inglese) di dimensione maggiore.  
Due approcci di sequenziamento ed assemblaggio del genoma sono stati sviluppati nel corso degli ultimi 20 anni, il **“Clone by Clone”** ed il **“Whole Genome Sequencing (WGS)”**.  
Il WGS è oggigiorno il principale approccio utilizzato per il sequenziamento dei genomi, soprattutto a seguito dell’avvento delle tecnologie di sequenziamento di nuova generazione (**Next Generation Sequencing, NGS** o **High Throughput Sequencing, HTS**).  
Nel corso dell’ultimo decennio sono state sviluppate diverse tecnologie per il sequenziamento degli acidi nucleici, distinte in tecnologie di seconda e terza generazione (Buermans and den Dunnen, 2014):  
    *	**II generazione**: **Roche 454** (Dismessa nel 2016), **SOLiD** ed **Illumina**;  
    *	**III generazione**: **PacBio** e **Oxford Nanopore**.  
    

