# KG20C: A scholarly knowledge graph benchmark dataset
KG20C is a curated knowledge graph built from the Microsoft Academic Graph (MAG) to support research on scholarly metadata — such as authors, papers, venues, affiliations, and citations. It has been designed for reproducible benchmarking in tasks including link prediction, recommendation, and question answering on scholarly data.

Note: This repository provides the dataset files and basic usage instructions.
A complete description of the dataset construction, schema, and evaluation baselines will appear in our forthcoming peer-reviewed publication.

<p align="center">
<img alt="KG20C graph" src="./KG20C_graph.png" width=500px>
<br>
<i><b>Figure 1:</b> Overview of the KG20C knowledge graph.</i>
</p>

## Dataset contents
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

## How to cite
If you found this dataset or our work useful, please cite us.

For the primilinary data and semantic query method, please cite the thesis:
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

For the MEI and MEIM baseline knowledge graph embedding models, please cite:
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

For the raw Microsoft Academic Graph dataset, please cite:
- *Arnab Sinha, Zhihong Shen, Yang Song, Hao Ma, Darrin Eide, Bo-June (Paul) Hsu, and Kuansan Wang. [An Overview of Microsoft Academic Service (MAS) and Applications](http://dx.doi.org/10.1145/2740908.2742839). In Proceedings of the International Conference on World Wide Web (WWW), 2015.*

## See also
- AnalyzeKGE, preliminary experiments and analysis: https://github.com/tranhungnghiep/AnalyzeKGE
- MEI-KGE, Multi-partition Embedding Interaction model: https://github.com/tranhungnghiep/MEI-KGE
