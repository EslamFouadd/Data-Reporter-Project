# Dataset Description
## Background
The Gene Ontology (GO) is a concept hierarchy that describes the biological function of genes and gene products at different levels of abstraction (Ashburner et al., 2000). It is a good model to describe the multi-faceted nature of protein function.

GO is a directed acyclic graph. The nodes in this graph are functional descriptors (terms or classes) connected by relational ties between them (is_a, part_of, etc.). For example, terms 'protein binding activity' and 'binding activity' are related by an is_a relationship; however, the edge in the graph is often reversed to point from binding towards protein binding. This graph contains three subgraphs (subontologies): Molecular Function (MF), Biological Process (BP), and Cellular Component (CC), defined by their root nodes. Biologically, each subgraph represent a different aspect of the protein's function: what it does on a molecular level (MF), which biological processes it participates in (BP) and where in the cell it is located (CC). See the Gene Ontology Overview for more details.

The protein's function is therefore represented by a subset of one or more of the subontologies.
These annotations are supported by evidence codes, which can be broadly divided into experimental (e.g., as documented in a paper published by a research team of biologists) and non-experimental. Non-experimental terms are usually inferred by computational means. We recommend you read more about the different types of GO evidence codes.

We will use experimentally determined term-protein assignments as class labels for each protein. That is, if a protein is labeled with a term, it means that this protein has this function validated by experimental evidence. By processing these annotated terms, we can generate a dataset of proteins and their ground truth labels for each term. The absence of a term annotation does not necessarily mean a protein does not have this function, only that this annotation does not exist (yet) in the GO. A protein may be annotated by one or more terms from the same subontology, and by terms from more than one subontology.

Ashburner M, et al. Gene ontology: tool for the unification of biology. The Gene Ontology Consortium. Nat Genet (2000) 25(1):25-29.

Training Set
For the training set, we include all proteins with annotated terms that have been validated by experimental or high-throughput evidence, traceable author statement (evidence code TAS), or inferred by curator (IC). More information about evidence codes can be found here. We use annotations from the UniProtKB release of 2022-11-17. The participants are not required to use these data and are also welcome to use any other data available to them.

Test Superset
The test superset is a set of protein sequences on which the participants are asked to predict GO terms.

Test Set
The test set is unknown at the beginning of the competition. It will contain protein sequences (and their functions) from the test superset that gained experimental annotations between the submission deadline and the time of evaluation.

File Descriptions
Gene Ontology: The ontology data is in the file go-basic.obo. This structure is the 2023-01-01 release of the GO graph. This file is in OBO format, for which there exist many parsing libraries. For example, the obonet package is available for Python. The nodes in this graph are indexed by the term name, for example the roots of the three onotlogies are:

subontology_roots = {'BPO':'GO:0008150',
                     'CCO':'GO:0005575',
                     'MFO':'GO:0003674'}
Training sequences: train_sequences.fasta contains the protein sequences for the training dataset.
This files are in FASTA format, a standard format for describing protein sequences. The proteins were all retrieved from the UniProt data set curated at the European Bioinformatics Institute.
The header contains the protein's UniProt accession ID and additional information about the protein. Most protein sequences were extracted from the Swiss-Prot database, but a subset of proteins that are not represented in Swiss-Prot were extracted from the TrEMBL database. In both cases, the sequences come from the 2022_05 release from 14-Dec-2022. More information can be found here.

The train_sequences.fasta file will indicate from which database the sequence originate. For example, sp|P9WHI7|RECN_MYCT in the FASTA header indicates the protein with UniProt ID P9WHI7 and gene name RECN_MYCT was taken from Swiss-Prot (sp). Any sequences taken from TrEMBL will have tr in the header instead of sp. Swiss-Prot and TrEMBL are both parts of UniProtKB.

This file contains only sequences for proteins with annotations in the dataset (labeled proteins). To obtain the full set of protein sequences for unlabeled proteins, the Swiss-Prot and TrEMBL databases can be found here.

Labels: train_terms.tsv contains the list of annotated terms (ground truth) for the proteins in train_sequences.fasta. The first column indicates the protein's UniProt accession ID, the second is the GO term ID, and the third indicates in which ontology the term appears.

Taxonomy: train_taxonomy.tsv contains the list of proteins and the species to which they belong, represented by a "taxonomic identifier" (taxon ID) number. The first column is the protein UniProt accession ID and the second is the taxon ID. More information about taxonomies can he found here.

Information accretion: IA.txt contains the information accretion (weights) for each GO term. These weights are used to compute weighted precision and recall, as described in the Evaluation section. The values of this file were computed using the following code repo.

Test sequences: testsuperset.fasta contains protein sequences on which the participants are asked to submit predictions. The header for each sequence in testsuperset.fasta contains the protein's UniProt accession ID and the Taxon ID of the species this protein belongs to. Only a small subset of those sequences will accumulate functional annotations and will constitute the test set. The file testsuperset-taxon-list.tsv is a set of taxon IDs for the proteins in the test superset.

# Files
train_sequences.fasta - amino acid sequences for proteins in training set
train_terms.tsv - the training set of proteins and corresponding annotated GO terms
train_taxonomy.tsv - taxon ID for proteins in training set
go-basic.obo - ontology graph structure
testsuperset.fasta - amino acid sequences for proteins on which the predictions should be made
testsuperset-taxon-list.tsv - taxon ID for proteins in test superset (Note: you may need to use encoding="ISO-8859-1" to read this file in pandas)
IA.txt - Information Accretion for each term. This is used to weight precision and recall (see Evaluation)
sample_submission.csv - a sample submission file in the correct format


# Data Source:
https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/data
