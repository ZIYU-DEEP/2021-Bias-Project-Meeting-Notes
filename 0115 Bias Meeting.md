# Bias Project Meeting on Jan 15, 2021

### 1. Retrospection on Reviews
> 🥳: This paper considers an **important issue** of tuning anomaly detection models in the absence of representative anomalies.  
> 😡: The analysis and experiments provided in the paper are **not surprising**, and **repeat**, although perhaps in more detail, known effects of learning with a non-representative training sample. 
<br>

> 😡: Using the labeled anomaly data to train and validate the trained model of course results in some sort of inductive bias. This is a **fundamental assumption in supervised learning like classification.** In anomaly detection, such bias is often desired in the sense that we want our detectors to identify anomalies similar to those labeled anomaly data. By contrast, there can be novel types of anomalies that can be very different from the known anomalies. Those novel anomalies cannot be detected if fitting only to the known anomalies. Therefore, **this conclusion is straightforward.**
<br>

### 2. Potential Directions for Paper Fix
#### 2.1. Rephrasing Paper Emphasis [to stand out from *common supervised learning*]
Surprise should mostly come from the application side, then from the methodology side.

**Application side**: *Anomaly detection **need supervision**, but must be done right.*
- In recent deep anomaly detection, (either semi- or self-) **supervision** is really popular. 
- It is important to **make use of labeled anomalies** in real world.
- It is not uncommon to use **only a subset of labeled anomalies**, *e.g.* spectrum misuse detection.
- However, all past publications have not recognized the great danger associated with such supervision in anomaly detection.

**Methodology side**: *The **negative effect of supervision** is **unique to anomaly detection**.*

| Classification Type | Known Label Set | Known Target Distribution |
| :---:        |    :----:   |          :---: |
| Imbalanced Sampling | :heavy_check_mark: | :heavy_multiplication_x:| 
| Domain Adaptation | :heavy_check_mark: | :heavy_check_mark: |
|Open Set Domain Adaptation| :heavy_multiplication_x: | :heavy_check_mark: |
| Anomaly Detection | :heavy_multiplication_x: | :heavy_multiplication_x: |

- In anomaly detection, we do not have full information of the **label set** (assuming each sub-type of anomalies have a different label), nor do we have a representative sample set of the **test distribution**.
- This poses a unique challenge to anomaly detection, that we could only use **much limited information to infer bias and debias**, compared to existing classification scenarios.
- To make this part stronger, we need additional theoretical / intuitive analysis texts on the understanding of bias.

*p.s.* "understanding" and "bias" may not be a so surprising title; some naming hints from [I Can't Believe It's Not Better workshop](https://i-cant-believe-its-not-better.github.io/accepted_papers/) @NeurIPS 2020.
- *Less Can Be More in Contrastive Learning*
- *Uses and Abuses of the Cross-Entropy Loss*
- *Selective Classification Can Magnify Disparities Across Groups*
- *Why Are ... Not Better?*
- *Perfect Density Models Cannot Guarantee Anomaly Detection*
- *Rethinking ...*
- *"It Doesn’t Get Better and Here’s Why": ...*
<br>

#### 2.2. Additional Experiments
##### 2.2.1. Datasets with Real-World Applications [to reinforce *issue importance*]
Additional datasets can include [Retinal OCT dataset](https://www.kaggle.com/paultimothymooney/kermany2018) or COVID-19 datasets.

However, it is hard to find a real-world application that we have to **only use a biased subset** of anomalies to train, like the spectrum misuse detection. This makes our findings less useful in practice.

##### 2.2.2. Additional Self-Supervised Models [to alleviate *repeatition*] [to tackle *straightforward conclusion*]
Self-supervised models use **synthetic anomalies** (like **adversarial examples**) generated from normal data to train. 

The synthetic anomalies may help form a **more compact representation for normal data**, but may also potentially mislead the model to focus on **certain features irrelevant** to detect real-world anomalies. It would be interested to study whether those adversarial examples hurt generalizability of anomaly detection models or not.

Relevant papers include  [Tack et al. 2020](https://github.com/alinlab/CSI); [Bergman & Hoshen 2020](https://openreview.net/forum?id=H1lK_lBtvS); [Zaheer et al. 2020](https://openaccess.thecvf.com/content_CVPR_2020/papers/Zaheer_Old_Is_Gold_Redefining_the_Adversarially_Learned_One-Class_Classifier_Training_CVPR_2020_paper.pdf); [Choi & Chung 2020](https://openreview.net/forum?id=ByeNra4FDB); [Hendrycks et al. 2019b](https://papers.nips.cc/paper/2019/hash/a2b15837edac15df90721968986f7f8e-Abstract.html); [Golan & El-Yaniv 2018](https://papers.nips.cc/paper/8183-deep-anomaly-detection-using-geometric-transformations.pdf). Most of them are based on a classifier though, which is different from our baseline.

#### 2.3. Bias Understanding [to add *surprisal*]
##### 2.3.1. Open Set Domain Adaptation Framework
- [Literature Review](https://github.com/ZIYU-DEEP/Paper-List-of-Open-Set-Domain-Adaptation)
- **Existing understanding**: *Supervision can cause bias* when there is unknown class in the target space.
- **Differences from anomaly detection**: The samples in the target (test) domain is usually representative, which allows for effective debias strategy.
- **Theory**: Error bounds on target samples consist of **source risk**, **domain discrepancy**, **open-set risk**, and **shared error on the joint hypothesis**.


##### 2.3.2. Information-Theoretical Framework 
<br>

#### 2.4. Other Future Directions Beyond Reviewers' Suggestions
- Let's jump out and accept the **bias is a known effect and not surprising**, and there exists **an obvious easy strategy** which is to use ensembles with unsupervised model to train, what would be the next?
- Can we design a model which guarantees better performance & lower complexity than ensemble with unsupervised models? That is, a Framework for which **additional labeled dataset will always be valuable**. This is more naturally aligned with human intelligence. (I have a name for it already :) – Almost Harmless Supervised Anomaly Detection.)

<br>

### 3. Flavor of Anomaly Detection Papers in AI Conferences

#### 3.1. ICML Papers 
[ICML-Paper-List-of-Anomaly-Detection](https://github.com/ZIYU-DEEP/ICML-Paper-List-of-Anomaly-Detection)  
Usually a problem, then a model to solve the problem. Only one paper is purely theoretical – [Open Category Detection with PAC Guarantee](https://arxiv.org/pdf/1808.00529.pdf). It may worth to re-phrase the paper like a follow-up of this one, given that we do not have a model.

#### 3.2. IJCAI Papers 
[IJCAI-Paper-List-of-Anomaly-Detection](https://github.com/ZIYU-DEEP/IJCAI-Paper-List-of-Anomaly-Detection)  
Those papers focus mostly on (1) new models or (2) improvement of models on real-world applications. Mostly no theory involved.

<br>

### 4. Discussion on Concrete Next Steps
Let's talk!