# KG20C: A scholarly knowledge graph benchmark dataset
To facilitate research in scholarly data analysis, we constructed the KG20C knowledge graph using data from 20 top computer science conferences. It can serve as a standard benchmark dataset for several tasks, including knowledge graph embedding, link prediction, recommendation systems, and question answering about high quality papers. 

This has been introduced and used in the TPDL'19 paper [Exploring Scholarly Data by Semantic Query on Knowledge Graph Embedding Space](https://arxiv.org/abs/1909.08191) and the PhD thesis [Multi-Relational Embedding for Knowledge Graph Representation and Analysis](https://ir.soken.ac.jp/?action=pages_view_main&active_action=repository_view_main_item_detail&item_id=6334&item_no=1&page_id=29&block_id=155). 

<p align="center">
<img alt="KG20C graph" src="./KG20C_graph.png" width=500px>
<br>
<i><b>Figure 1:</b> Overview of the KG20C knowledge graph.</i>
</p>

## Construction protocol
### Scholarly data extraction
From the [Microsoft Academic Graph](https://academic.microsoft.com/) dataset, we extracted high quality computer science papers published in top conferences between 1990 and 2010. The top conference list are based on A* conferences in the [CORE ranking](http://portal.core.edu.au/conf-ranks/) version 2020. The data was cleaned by removing conferences with less than 300 publications and papers with less than 20 citations. The final list includes 20 top conferences (in alphabetical order): *AAAI, AAMAS, ACL, CHI, COLT, DCC, EC, FOCS, ICCV, ICDE, ICDM, ICML, ICSE, IJCAI, NIPS, SIGGRAPH, SIGIR, SIGMOD, UAI, and WWW*.

### Knowledge graph construction
From the scholarly data, we define the entities, the relations, and construct the triples. The knowledge graph can be seen as a labeled multi-digraph between scholarly entities, with edge labels expressing the relationships between the nodes. We use 5 intrinsic entity types including *Paper, Author, Affiliation, Venue, and Domain*. We also use 5 intrinsic relation types between the entities including *author\_in\_affiliation, author\_write\_paper, paper\_in\_domain, paper\_cite\_paper, and paper\_in\_venue*.

### Benchmark data splitting
The knowledge graph was split uniformly at random into the training, validation, and test sets. We made sure that all entities and relations in the validation and test sets also appear in the training set so that their embeddings can be learned. We also made sure that there is no data leakage and no redundant triples in these splits, thus, KG20C constitutes a challenging benchmark for link prediction similar to WN18RR and FB15K-237.

## Content of dataset
### File format
All files are in tab-separated-values format, compatible with other popular benchmark datasets including WN18RR and FB15K-237. For example, *train.txt* includes "*28674CFA	author_in_affiliation	075CFC38*", which denotes the author with id *28674CFA* works in the affiliation with id *075CFC38*. 

The repo includes these files:
- *all_entity_info.txt* contains *id  name  type* of all entities
- *all_relation_info.txt* contains *id* of all relations
- *train.txt* contains training triples of the form *entity_1_id  relation_id  entity_2_id*
- *valid.txt* contains validation triples
- *test.txt* contains test triples

### Statistics
Data statistics of the KG20C knowledge graph:

Author | Paper | Conference | Domain | Affiliation
:---: | :---: | :---: | :---: | :---:
8,680 | 5,047 | 20 | 1,923 | 692

Entities | Relations | Training triples | Validation triples | Test triples
:---: | :---: | :---: | :---: | :---:
16,362 | 5 | 48,213 | 3,670 | 3,724

### License
The dataset is free to use for research purpose. For other uses, please follow Microsoft Academic Graph license.

## Baseline results
We include the results for link prediction and semantic queries on the KG20C dataset. Link prediction is a relational query task given a relation and the head or tail entity to predict the corresponding tail or head entities. Semantic queries include human-friendly query on the scholarly data. MRR is mean reciprocal rank, Hit@k is the percentage of correct predictions at top k. 

For more information, please refer to the citations.

### Link prediction results
We report results for 4 methods. Random, which is just random guess to show the task difficulty. Word2vec, which is the popular embedding method. SimplE/CP<sub>h</sub> and MEI are two recent knowledge graph embedding methods.

All models are in small size settings, equivalent to total embedding size of 100 (50x2 for Word2vec and SimplE/CP<sub>h</sub>, 10x10 for MEI).

Models | MRR | Hit@1 | Hit@3 | Hit@10
:--- | :---: | :---: | :---: | :---:
Random | 0.001 | < 5e-4 | < 5e-4 | < 5e-4
Word2vec (small) | 0.068 | 0.011 | 0.070 | 0.177
SimplE/CP<sub>h</sub> (small) | 0.215 | 0.148 | 0.234 | 0.348
MEI (small) | **0.230** | **0.157** | **0.258** | **0.368**

### Semantic queries results
The following results demonstrate semantic queries on knowledge graph embedding space, using the above *MEI (small)* model.

Queries | MRR | Hit@1 | Hit@3 | Hit@10
:--- | :---: | :---: | :---: | :---:
Who may work at this organization? | 0.299 | 0.221 | 0.342 | 0.440
Where may this author work at? | 0.626 | 0.562 | 0.669 | 0.731
Who may write this paper? | 0.247 | 0.164 | 0.283 | 0.405
What papers may this author write? | 0.273 | 0.182 | 0.324 | 0.430
Which papers may cite this paper? | 0.116 | 0.033 | 0.120 | 0.290
Which papers may this paper cite? | 0.193 | 0.097 | 0.225 | 0.404
Which papers may belong to this domain? | 0.052 | 0.025 | 0.049 | 0.100
Which may be the domains of this paper? | 0.189 | 0.114 | 0.206 | 0.333
Which papers may publish in this conference? | 0.148 | 0.084 | 0.168 | 0.257
Which conferences may this paper publish in? | 0.693 | 0.542 | 0.810 | 0.976

## How to cite
If you found this dataset or our work useful, please cite us.

For the dataset and semantic query method, please cite:
- *Hung-Nghiep Tran and Atsuhiro Takasu. [Exploring Scholarly Data by Semantic Query on Knowledge Graph Embedding Space](https://arxiv.org/abs/1909.08191). In Proceedings of International Conference on Theory and Practice of Digital Libraries (TPDL), 2019.*
  ```
  @inproceedings{tran_exploringscholarlydata_2019,
    title = {Exploring {Scholarly} {Data} by {Semantic} {Query} on {Knowledge} {Graph} {Embedding} {Space}},
    booktitle = {Proceedings of the 23rd {International} {Conference} on {Theory} and {Practice} of {Digital} {Libraries}},
    author = {Tran, Hung-Nghiep and Takasu, Atsuhiro},
    year = {2019},
    pages = {154--162},
    url = {https://arxiv.org/abs/1909.08191},
  }
  ```

For the extended semantic query method and baseline results, please cite:
- *Hung-Nghiep Tran. [Multi-Relational Embedding for Knowledge Graph Representation and Analysis](https://ir.soken.ac.jp/?action=pages_view_main&active_action=repository_view_main_item_detail&item_id=6334&item_no=1&page_id=29&block_id=155). PhD Dissertation, The Graduate University for Advanced Studies, SOKENDAI, Japan, 2020.*  
  ```
  @phdthesis{tran_multirelationalembeddingknowledge_2020,
    address = {Japan},
    type = {{PhD} {Dissertation}},
    title = {Multi-{Relational} {Embedding} for {Knowledge} {Graph} {Representation} and {Analysis}},
    school = {The Graduate University for Advanced Studies, SOKENDAI},
    author = {Tran, Hung-Nghiep},
    year = {2020},
  }
  ```

For the MEI and MEIM knowledge graph embedding models, please cite:
- *Hung-Nghiep Tran and Atsuhiro Takasu. [Multi-Partition Embedding Interaction with Block Term Format for Knowledge Graph Completion](https://arxiv.org/abs/2006.16365). In Proceedings of the European Conference on Artificial Intelligence (ECAI), 2020.*  
  ```
  @inproceedings{tran_multipartitionembeddinginteraction_2020,
    title = {Multi-{Partition} {Embedding} {Interaction} with {Block} {Term} {Format} for {Knowledge} {Graph} {Completion}},
    booktitle = {Proceedings of the {European} {Conference} on {Artificial} {Intelligence}},
    author = {Tran, Hung-Nghiep and Takasu, Atsuhiro},
    year = {2020},
    pages = {833--840},
    url = {https://arxiv.org/abs/2006.16365},
  }
  ```
- *Hung-Nghiep Tran and Atsuhiro Takasu. [MEIM: Multi-partition Embedding Interaction Beyond Block Term Format for Efficient and Expressive Link Prediction](https://arxiv.org/abs/2209.15597). In Proceedings of the International Joint Conference on Artificial Intelligence (IJCAI), 2022.*  
  ```
  @inproceedings{tran_meimmultipartitionembedding_2022,
    title = {{MEIM}: {Multi}-partition {Embedding} {Interaction} {Beyond} {Block} {Term} {Format} for {Efficient} and {Expressive} {Link} {Prediction}},
    booktitle = {Proceedings of the {Thirty}-{First} {International} {Joint} {Conference} on {Artificial} {Intelligence}},
    author = {Tran, Hung-Nghiep and Takasu, Atsuhiro},
    year = {2022},
    pages = {2262--2269},
    url = {https://arxiv.org/abs/2209.15597},
  }
  ```

For the Microsoft Academic Graph dataset, please cite:
- *Arnab Sinha, Zhihong Shen, Yang Song, Hao Ma, Darrin Eide, Bo-June (Paul) Hsu, and Kuansan Wang. [An Overview of Microsoft Academic Service (MAS) and Applications](http://dx.doi.org/10.1145/2740908.2742839). In Proceedings of the International Conference on World Wide Web (WWW), 2015.*

## See also
- AnalyzeKGE, preliminary experiments and analysis: https://github.com/tranhungnghiep/AnalyzeKGE
- MEI-KGE, Multi-partition Embedding Interaction model: https://github.com/tranhungnghiep/MEI-KGE
