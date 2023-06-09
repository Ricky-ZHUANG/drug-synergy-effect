# **AI for Drug synergy prediction**

## Introduction

- Why this big topic? 
  - Introduce what is monotheropy and the limitation
  - Drug combination has <ins>better treatment effect</ins> than monotheropy
  - However, using <ins>wrong drug combination may lead to side effect</ins>, also <ins>too many drug combinations</ins> for scientists to detect
  - Solution to the aforementioned issues is `High Throughput Drug Screening`

- Why this small topic?
  - The performance of High Throughput Drug Screening will decrease as the number of data drcrease
  - With less data, those tissues are more under studied

## Literature Review

- How people make prediction on drug synergy effect?
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

## Method

- Re-implement the work of Li Yu and conduct experiment of comparing the performance of GSL solely
- Utilize the work of Sun Kim 1 to generate the after treatment gene
- perform data augamentation using the work of Kim 2 (generating sub strugture of the drug)
- Information propergation via GNN

