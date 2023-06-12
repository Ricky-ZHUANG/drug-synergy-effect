# **AI for Drug synergy prediction - Data augmentation to tackle understudied tissue problem**

## Introduction

- Why this big topic? 
  - Introduce what is monotheropy and the limitation
  - Drug combination has <ins>better treatment effect</ins> than monotheropy
  - However, using <ins>wrong drug combination may lead to side effect</ins>, also <ins>too many drug combinations</ins> for scientists to detect
  - Solution to the aforementioned issues is `High Throughput Drug Screening`

- Why this small topic?
  - The performance of High Throughput Drug Screening will decrease as the number of data drcrease
  - With less data, those tissues are more under studied

Monotherapy is widely practiced as a standard treatment regimen for various diseases. However, the effectiveness of this conventional therapy is restricted by several factors, including the complexity of human diseases (Sun et al., 2020), patient heterogeneity, and drug resistance. One of the most significant limitations of using monotherapy is the development of drug resistance, which can arise due to multiple variables associated with the cancer cell line's system. As a result, pharmacy researchers use combinatorial drug therapy as an alternative to address these issues. Combinatorial drug therapy is a treatment approach that utilizes more than one medicine or treatment simultaneously to enhance the therapeutic outcomes of individual drugs. Consequently, this approach has been reported to significantly enhance curative efficacy in treating various diseases, particularly cancer (Sun et al., 2020). 

Despite the tremendous potential of combinatorial drug therapy, drug combinations that are efficient and safe remain elusive. The search for optimal drug pairs is further complicated by several challenges, including systemic toxicity, potential side effects, and tissue understudy. The core of this theropy is the identification of synergy effect, while this procedure can be costly and time-consuming. Therefore scientists have been working for years to tackles this issue. One approach currently being pursued is High Throughput Drug Screening (HTS), a computational method that utilize large scale of drug sensitivity data to make predition on drug response effect. However, the effectiveness of HTS is dependent on a better understanding of tissue biology and addressing issues of tissue understudy. Ultimately, addressing these issues will foster the development of efficient and effective drug combinations, leading to improved treatment outcomes.

## Literature Review

- How people make prediction on drug synergy effect?
  - DeepSynergy
  - MatchMaker  
- Limitation of these model
  - Can not tackle under studies tissue

- How people tackle understudied tissue problem?
  - Kim 1 used <ins>transfer learning</ins> to transfer knowledge from data rich tissue to under studied tissues
  - Li Yu learn representation of drug target and disease via pretrained model and used GSL to generate pseudo edge to refine the graph representation
  - Kim 2 applied GPT to make prediction
- Limitation
  - Kim 1 informaion aggregation is not explainable (solely concating three information and feed forward)
  - The work of Li Yu does not conduct experiment on whether GSL would help.
  - Work of Li Yu does not show that pre-trained model actually helps the prediction.
  - Kim 2 does not embed the knowledge of drug target and disease (they make it as a NLP inference task)
  - Before treatment gene expression is not helping


Traditional methods for training predictors of synergy effects are based on the assumption that the available data is sufficient to train models with high generalizability. 

<ins>However, significant issues arise when dealing with understudied tissues where in vivo experiments are difficult to conduct, leading to an insufficiency of data for model training.</ins> To overcome the challenge of understudied tissues, researchers have been exploring various methods. For instance, Kim 1 (2021) learned the knowledge embedding of drug, cell line from SMILES, MACCS fingerprint, FPKM values and disease type, then utilized transfer learning to transfer knowledge from data-rich tissues to understudied tissues, based on the fact that different tissues share certain biological features, with similar features these tissues might have similar drug response. CancerGPT (Kim et al., 2021) transformed the original task to a natural language inference task and modified the model of GPT-2 and GPT-3 to generate the answer of synergistic and antagonistic based on the knowledge encoded from tabular input of synergy data containing the information of drug cell line drug semsitivity and synergy score. LiYu (Zhang et al., 2020) leveraged pre-trained models to extract biological and chemical information to obtain an initial graph indicating the relationship across drugs, targets, and diseases. Then, through graph structure learning, LiYu was able to obtain the refined graph representation, and through a self-training strategy, this model outperformed other baseline methods.

## Limitation and Improvement
The aforementioned methods [... kim1 CancerGPT LiYu] take solely the gene expression data before the treatment into account. However, (sk append) has indicated that the gene expression profile before treatment does not significantly assist in predicting drug response. Furthermore, the experiment conducted by LiYu did not reveal a strong increase in performance by using pre-trained models. Additionally, the efficacy of solely utilizing graph structure learning has not been specifically examined in any study to date.

method

Netgp show a strong ability of simulating the bilogical process of gene perturbation, and netgp made a good performance in improving the performance of drug response prediction model. Utilizing netgp, we are able to generate post-treatment gene expression profile and utilize it to make synergy effect preidction.
Additionally, the work of sun kim2 is able togenerate sub-structures of molecules. Leveraging this algorithm, it is able to conduct data agumentation for understudied thissues.


## Method

- Re-implement the work of Li Yu and conduct experiment of comparing the performance of GSL solely
- Utilize the work of Sun Kim 1 to generate the after treatment gene
- perform data augamentation using the work of Kim 2 (generating sub strugture of the drug)
- Information propergation via GNN

In this study we introduce a machinanism for drugs data augamentation that used Sum Kim2 to generate the sub-structure of drug molecules and the candidate drugs, then by going through a filter algirithm the reamining drugs data could be used for data augamentation.
In this study we used the work of Sun Kim1 to generate the gene expression profile after treatment.
In this study we used graph convolution network to propogate through the data.
We used self-training because the work of LiYu showed that self-training is able to improve the performance

In this study, we propose a mechanism for drug data augmentation utilizing Sum Kim2 to generate sub-structures of drug molecules and candidate drugs. (introduce sunkim2: ). These generated sub-structures are filtered using (an algorithm: ) to retain the remaining drug data for augmentation purposes. To generate the gene expression profiles after treatment, we employed the netgp developed by Sun Kim1. (introduct netgp: ). Graph convolutional networks were utilized to propagate through the generated data.

Self-training strategy represents a straightforward yet highly effective approach. The strategy involves initially training a model with a particular set of labeled data. Subsequently, the model utilizes the trained information to predict labels for a given set of unlabeled data. Finally, the model retrains and refines itself using a combination of the original labeled data and the newly-predicted labeled data generated through the utilization of the trained model. The self-training strategy has demonstrated its efficacy in numerous studies, making it a popular choice for enhancing model performance. Thus, we utilized self-training as an approach to improve the performance of our proposed mechanism for drug data augmentation.

KPGT    -->drug data

ESM     -->protein

RotatE  -->disease
