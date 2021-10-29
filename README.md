# The Annotated Corpora of Historical Catalan (HisCat)

This repo brings together all code as well as the necessary source and configuration files used for the development (from pre- to post-processing as well as all annotation) of the annotated corpora of historical Catalan (HisCat), which are deposited on [Zenodo HisCat](https://doi.org/10.5281/zenodo.5615759). 

This corpus is the first step towards the construction of a morpho-syntactically annotated corpus of Old Catalan, a low resource language that lacks syntactically annotated corpora facilitating the study of its syntax diachronically. HisCat – Llibre dels Fets offers a POS-tagged version of _El Llibre dels Fets_, a 13th century Catalan chronicle. The version of the text used for this project is

Bruguera, J. (1991). _El Llibre dels Fets del Rei en Jaume._ Barcelona: Barcino.

as prepared for the Corpus Informatitzat del Català Antic

Torruella, J., Pérez Saldanya, M., & Martines, J. (2009). Corpus Informatitzat del Català Antic. URL: http://cica.cat/.

The corpus counts with 164,096 POS-annotated tokens, of which 60,000 have been manually corrected. Annotation appears in the form of:
- splitting sentences
- tokenisation/segmentation
- POS tagging 
- constituency-based phrase-structure parsing (in Penn-style .psd format; still in progress)

With the right dependencies installed, this repo will allow users to POS-tag their own historical Catalan texts. In addition, it will include code to add metadata and sentenceIDs for those texts that can be (roughly) dated (see planned developments).

If you use any part of the corpus or code, please cite:

Meelen, Marieke & Pujol i Campeny, Afra, (2021) Old Catalan Morphosyntax: developing an annotated corpus' in _Journal of Open Humanities Data_.

and

Pujol i Campeny, Afra & Meelen, Marieke (2021a) 'Annotated Corpora of Historical Catalan (HisCat): Llibre dels Fets', [DOI:](https://doi.org/10.5281/zenodo.5615759)

Pujol i Campeny, Afra & Meelen, Marieke (2021b) 'Old Catalan word embeddings based on Llibre dels Fets', [DOI:](https://doi.org/10.5281/zenodo.5615556)

Note that other texts will be annotated in the same fashion and deposited on Zenodo as soon as they are ready. Links will be updated and added here.

## Getting Started 

The following instructions work in the Mac terminal if the right dependencies are installed, but could be tranferred to any linux system too:

Simply clone and cd to the repo:
```sh
git clone catalancorpora
cd catalancorpora
```

POS tag a single plain text file and write to 'my-file_tagged.txt' with the [TiMBL / MBT](https://languagemachines.github.io/mbt/):
```sh
Mbt -t my-file.txt -s /conf/60000train.txt.settings > 'my-file_tagged.txt'
```

(Note that for the purposes of open data and transparency, settings files of earlier training iterations described in the paper are included here too to facilitate replication of our results.)

For neural-based tagging with with TARGER, please see [the TARGER repo](https://github.com/achernodub/targer). Historical Catalan word embeddings (trained with [FastText](https://fasttext.cc/)) can be found on [Zenodo](https://doi.org/10.5281/zenodo.5615556). Please note that due to very limited access to digitised Old Catalan texts, these embeddings are based on the same text that was used to train the memory-based POS tagger, namely the 13th century historiographic chronicle _Llibre dels Fets_. As soon as more digital texts become available to us, we will create better embeddings.

### Prerequisites & Dependencies

- [TiMBL / MBT](https://languagemachines.github.io/mbt/) (for memory-based tagging)
- [the TARGER repo](https://github.com/achernodub/targer) (for neural-based tagging)

## Preprocessing input files

For memory-based tagging with the MBT, tokens are one per line and sentences should be separated by ```<utt>```.

For neural-based tagging with TARGER, tokens are one per line sentences in input files should be separated by white lines.

For both taggers, any unicode characters are allowed and will be recognised as separate characters. Note that this includes apostrophes and other punctuation marks.

### Sentence segmentation and tokenisation

Utterance boundaries were automatically inserted following full stops in the edition (ADD REF?). This resulted in 4,506 main clauses for the entire _Llibre dels Fets_ corpus.

Tokenisation was partly done based on spaces around words. Any clitics and determiners that were attached to preciding/following tokens were cut off and treated as separate tokens to increase the accuracy of the POS tagger and facilitate more detailed morphosyntactic research. This resulted in a total of 165,538 tokens (including punctuation and folio markers) for the _Llibre dels Fets_ corpus.

### SentenceIDs

SentenceIDs will be added automatically in the next stage of the project.

## POS tagging

The following POS tags were used and saved as a control list in Pyrrha https://dh.chartes.psl.eu/pyrrha/controls/17/read/POS and available here in the conf directory too:

```
!,",-,.,:,;,?,ADJ,ADJ^POS,ADJ^Q,ADV,ASIDEB,ASIDEE,C,COMMA,CONJ,CONJ+NEG,D,DPR,D^DEM,D^POS,D^Q,FOL,FW,INTJ,MAN,N,NEG,NPR,NUM,OLB,OLE,P,P+D,PRO^1^PL,PRO^1^SG,PRO^2^PL,PRO^2^SG,PRO^3^PL,PRO^3^SG,PRO^ADV,PRO^A^1^PL,PRO^A^1^SG,PRO^A^2^PL,PRO^A^2^SG,PRO^A^3^PL,PRO^A^3^SG,PRO^A^NTR,PRO^D^1^PL,PRO^D^1^SG,PRO^D^2^PL,PRO^D^2^SG,PRO^D^3^PL,PRO^D^3^SG,PRO^Q,PRO^RFL^1^PL,PRO^RFL^1^SG,PRO^RFL^2^PL,PRO^RFL^2^SG,PRO^RFL^3^PL,PRO^RFL^3^SG,VB,VBDI^1^PL,VBDI^1^SG,VBDI^2^PL,VBDI^2^SG,VBDI^3^PL,VBDI^3^SG,VBDS^1^PL,VBDS^1^SG,VBDS^2^PL,VBDS^2^SG,VBDS^3^PL,VBDS^3^SG,VBFI^1^PL,VBFI^1^SG,VBFI^2^PL,VBFI^2^SG,VBFI^3^PL,VBFI^3^SG,VBI^1^PL,VBI^1^SG,VBI^2^PL,VBI^2^SG,VBI^3^PL,VBI^3^SG,VBPC^1^PL,VBPC^1^SG,VBPC^2^PL,VBPC^2^SG,VBPC^3^PL,VBPC^3^SG,VBPI^1^PL,VBPI^1^SG,VBPI^2^PL,VBPI^2^SG,VBPI^3^PL,VBPI^3^SG,VBPS^1^PL,VBPS^1^SG,VBPS^2^PL,VBPS^2^SG,VBPS^3^PL,VBPS^3^SG,VG,VN,VNI,WADJ,WADV,WPRO,[,],§,¿
```

## Planned developments

For the next stage of development of the HisCat that is projected to come out in 2022, we are currently preparing the following:

- Automatic sentenceIDs
- Optimise sentence divisions: For the current version of HisCat sentence boundaries are defined automatically following every full stop in the edition by Bruguera (1991) and Torruella (2009). In future versions we might consider splitting sentences in other places too to facilitate parsing, e.g. with direct speech, with semicolons etc.
- Adding parsed/syntactic annotation
- Creating better word embeddings (pending availability of more digitised texts)

## License
This project is licensed under the MIT License - see the LICENSE.md file for details

## Acknowledgements
Research that partially facilitated the creation of this code was funded by the British Academy (PDF grant pf170063) and the Cambridge Humanities Research Grant (Tier 2 Grant, GASR011522).
