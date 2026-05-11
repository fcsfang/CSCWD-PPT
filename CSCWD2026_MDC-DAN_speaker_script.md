# CSCWD 2026 MDC-DAN Presentation Speaker Script

Paper: MDC-DAN: Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins

Recommended total duration: about 13 minutes  
Safe range: 12-15 minutes  
Speaking strategy: do not read every word on the slides. Use each slide to deliver one message, then move on.

## Quick Timing Plan

| Slide | Topic | Suggested time |
|---|---:|---:|
| 1 | Title | 35 s |
| 2 | Outline | 25 s |
| 3 | Motivation | 50 s |
| 4 | Research Gap | 50 s |
| 5 | Problem Setting | 50 s |
| 6 | Key Idea | 45 s |
| 7 | Contributions | 45 s |
| 8 | Conceptual Pipeline | 45 s |
| 9 | Full Architecture | 40 s |
| 10 | Physics-Encoding Layer | 65 s |
| 11 | Domain-Adversarial Module | 70 s |
| 12 | Experimental Setup | 45 s |
| 13 | Main Results | 70 s |
| 14 | Robustness & Efficiency | 45 s |
| 15 | Interpretability | 60 s |
| 16 | Conclusion | 35 s |

Total: about 12.9 minutes

---

## Slide 1 - Title

Suggested time: 35 seconds

Main message: introduce the topic and the central thesis.

English script:

Good morning / afternoon, everyone. I am Chuanshan Fang from Nanjing University of Aeronautics and Astronautics. Today I will present our work, MDC-DAN: Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins.

The key problem we address is the Sim-to-Real gap in fault diagnosis. A model trained on clean laboratory or digital-twin data often performs poorly when deployed on noisy physical assets. Our main idea is to combine physics priors from rotor dynamics with adversarial domain adaptation, so that the model can transfer from labeled source data to unlabeled real-world target data.

As a preview, MDC-DAN achieves 93.94% target-domain accuracy, an F1-score of 0.942, and an average inference time of 4.2 milliseconds per sample.

Chinese reminder:

这一页只讲三件事：我是谁、题目是什么、核心思想是什么。不要展开实验细节，结果数字只是 teaser。

Time control:

If running late, skip the author list and only say: "The key idea is to combine physics priors with adversarial domain adaptation."

---

## Slide 2 - Presentation Outline

Suggested time: 25 seconds

Main message: give the audience a roadmap.

English script:

This talk is organized into four parts. First, I will introduce the background and motivation, especially why the Sim-to-Real gap is difficult for digital-twin fault diagnosis. Second, I will present the proposed method, MDC-DAN. Third, I will show the experimental results and analysis, including robustness, efficiency, t-SNE, and SHAP interpretability. Finally, I will conclude with the main takeaway and future work.

Chinese reminder:

目录页要快，不要解释技术细节。给听众一个路线图即可。

Time control:

Keep this under 30 seconds.

---

## Slide 3 - Motivation: Sim-to-Real Gap

Suggested time: 50 seconds

Main message: same fault mechanism, but different data distribution.

English script:

The motivation comes from a common deployment problem in digital-twin diagnosis. In the source domain, we usually have laboratory or digital-twin data. These signals are relatively clean, controlled, and labeled. In the target domain, however, the data come from real physical assets, such as high-speed train bearings. These signals are noisy, unlabeled, and collected under variable-speed operating conditions.

Although the underlying bearing fault mechanism is the same, the data distribution is different. This is why we write it as P of X source is not equal to P of X target. A classifier trained only on the source domain may learn source-specific statistics, and then fail when deployed to the target domain.

So the key challenge is not only fault classification. It is target-domain generalization under distribution shift.

Chinese reminder:

重点解释图的三部分：左边源域 clean/labeled/controlled，中间分布偏移，右边目标域 noisy/unlabeled/variable-speed。核心句是：故障机理相同，但数据分布不同。

Time control:

Do not describe every visual element. Spend most of the time on P(Xs) != P(Xt).

---

## Slide 4 - Research Gap

Suggested time: 50 seconds

Main message: pure data-driven domain alignment can align the wrong evidence.

English script:

Existing domain adaptation methods are useful, but many of them are mainly data-driven. In industrial fault diagnosis, this can be risky.

First, noise alignment may happen. If the model only tries to make source and target features look similar, it may align noise patterns rather than fault semantics. Second, there is no explicit mechanism check. The model does not know whether the aligned features are consistent with bearing kinematics. Third, unconstrained alignment can even cause negative transfer, where adaptation hurts target-domain diagnosis.

MDC-DAN responds to these three issues by adding a physics-based anchor before adversarial alignment. In other words, we do not align raw statistical patterns directly. We first transform the signal into mechanism-aware features.

Chinese reminder:

这一页要把问题讲清楚：不是说 DA 没用，而是说纯数据驱动 DA 在噪声环境中可能对齐错东西。后面方法就是为了解决这个问题。

Time control:

If short on time, summarize the three limitations as: noise alignment, no mechanism check, and negative transfer.

---

## Slide 5 - Problem Setting

Suggested time: 50 seconds

Main message: this is unsupervised domain adaptation.

English script:

Here is the formal problem setting. We have a labeled source domain, denoted as Ds, where each source sample has a fault label. We also have an unlabeled target domain, denoted as Dt, collected from physical assets.

The important assumption is that the marginal distributions are different: P of X source is not equal to P of X target. This distribution shift is caused by speed variation, environmental noise, and differences between laboratory and real operating conditions.

The goal is to learn a diagnostic function that minimizes target-domain risk. However, target-domain labels are unavailable during training and are used only for final evaluation. This is the key constraint of unsupervised domain adaptation.

Chinese reminder:

强调 UDA 的核心：训练时没有目标域标签。目标域标签只能评估用，不能参与训练。公式不要逐字念，只解释含义。

Time control:

Spend no more than 15 seconds on the mathematical notation.

---

## Slide 6 - Key Idea

Suggested time: 45 seconds

Main message: physics first, alignment second.

English script:

The key idea of MDC-DAN is very simple: physics first, alignment second.

We first use physical priors from rotor dynamics to lock mechanism invariants. This produces a mechanism-aligned representation, so that important fault evidence is preserved. Then adversarial adaptation is applied to align the remaining source-target discrepancy.

This order is important. If we align data too early, the model may align noise with noise. But if we first constrain the representation with physical mechanisms, adversarial learning focuses on the residual domain gap rather than arbitrary statistical patterns.

Chinese reminder:

这一页是整篇报告的灵魂。要讲出顺序为什么重要：先物理约束，后对抗对齐。避免把噪声当作故障特征来对齐。

Time control:

Pause briefly after saying "physics first, alignment second."

---

## Slide 7 - Contributions

Suggested time: 45 seconds

Main message: three contributions form a closed loop with the research gaps.

English script:

Our work makes three main contributions.

First, we design a physics-embedded network structure. The Physics-Encoding Layer is frozen and embeds bearing kinematic priors directly into the network input.

Second, we propose collaborative adversarial adaptation. Instead of aligning raw signals, the model aligns the residual source-target discrepancy after physics encoding.

Third, we provide trustworthy interpretability. Through t-SNE and SHAP, we verify that the model relies on physically meaningful evidence rather than environmental noise.

Together, these three contributions correspond to the three gaps discussed earlier: mechanism consistency, safer alignment, and trustworthy decision evidence.

Chinese reminder:

三点贡献要和第 4 页呼应：C1 解决无机理约束，C2 降低噪声对齐，C3 验证没有学偏。

Time control:

Do not over-explain here. Details are in the following method slides.

---

## Slide 8 - Conceptual Pipeline

Suggested time: 45 seconds

Main message: show the high-level data flow before the full architecture.

English script:

This slide gives a simplified pipeline of MDC-DAN.

Both source and target vibration signals first pass through the frozen Physics-Encoding Layer, denoted as Phi-phy. This layer converts the raw signal into a 15-dimensional mechanism-aligned feature vector, h-phy.

Then the feature extractor Gf maps h-phy into a latent representation z. From z, the network has two branches: the label predictor Gy performs fault classification, and the GRL plus domain discriminator Gd performs adversarial domain alignment.

So the whole pipeline is: signal, physics encoding, latent feature learning, and then joint fault prediction and domain adaptation.

Chinese reminder:

这一页讲流程，不讲公式。听众要先知道信号怎么走：Source/Target -> Phi_phy -> h_phy -> Gf -> z -> Gy/Gd。

Time control:

Keep this as a transition slide. The details come next.

---

## Slide 9 - Full Architecture of MDC-DAN

Suggested time: 40 seconds

Main message: connect the conceptual pipeline to the paper architecture.

English script:

Here is the full architecture of MDC-DAN. The left part is the Physics-Encoding Layer. It transforms raw vibration signals into physics-aligned embeddings. The right part is the trainable Domain-Adversarial Module, which learns domain-invariant latent features through adversarial backpropagation.

The key point is the dual-stage design. The first stage is non-learnable and mechanism-driven. The second stage is learnable and data-driven. Their collaboration allows the model to use physical knowledge while still adapting to real target-domain data.

Chinese reminder:

不要细讲图中每一个小模块，讲左右两部分：左边物理编码，右边对抗模块。强调 non-learnable + trainable 的协同。

Time control:

This slide should be short. It prepares for Slide 10 and Slide 11.

---

## Slide 10 - Physics-Encoding Layer

Suggested time: 65 seconds

Main message: Phi-phy is frozen, non-learnable, and determined by rotor dynamics.

English script:

Now let us look at the Physics-Encoding Layer in more detail.

Unlike standard deep models that feed raw signals directly into learnable convolutional layers, MDC-DAN first maps the raw vibration signal into a 15-dimensional physical feature vector. This vector contains three groups of features.

The first group is time-domain statistics, such as RMS, kurtosis, skewness, peak-to-peak value, shape factor, and impulse factor. These describe general vibration severity and impulsiveness.

The second group is mechanism energy features. These are energy ratios around theoretical bearing fault frequencies, including BPFO, BPFI, BSF, FTF, and their second harmonics. This is the most important part because it directly corresponds to bearing fault mechanisms.

The third group is frequency-domain statistics, such as spectral centroid, spectral RMS, and spectral variance.

The mapping can be written as h-phy equals Phi-phy of x, which concatenates statistical, mechanism, and frequency features. Importantly, Phi-phy is frozen. Its calculation paths are determined by rotor dynamics, not learned from data.

For example, BPFO depends on the number of rolling elements N, shaft frequency fr, rolling element diameter d, pitch diameter D, and contact angle alpha. This formula explicitly links the neural input to bearing kinematics.

Chinese reminder:

这一页非常关键。要强调不是普通手工特征，而是 frozen / non-learnable layer。BPFO 公式只解释变量含义，不要推导。

Time control:

This page can take a little longer, but keep it under 70 seconds.

Pronunciation:

BPFO: "B-P-F-O"  
BPFI: "B-P-F-I"  
Phi-phy: "Phi physical" or "Phi phy"

---

## Slide 11 - Domain-Adversarial Module

Suggested time: 70 seconds

Main message: DANN is applied after physics encoding.

English script:

After physics encoding, h-phy is fed into the trainable Domain-Adversarial Module.

This module follows the standard DANN logic. The feature extractor Gf maps the 15-dimensional physics-aligned features into a latent space. The label predictor Gy uses the source-domain labels to preserve fault-discriminative information. The domain discriminator Gd tries to distinguish whether a feature comes from the source domain or the target domain.

The Gradient Reversal Layer, or GRL, creates the adversarial game. During backpropagation, it makes Gf learn features that can fool Gd. As a result, the latent representation becomes more domain-invariant.

The training objective combines the classification loss Ly and the domain adversarial loss Ld. The trade-off parameter lambda-p follows a dynamic schedule. At the beginning of training, lambda-p is close to zero, so the immature discriminator does not introduce unstable gradients. As training progresses, lambda-p increases and domain alignment becomes stronger.

The key difference from vanilla DANN is this: MDC-DAN aligns mechanism-aware features h-phy, rather than raw statistical patterns.

Chinese reminder:

先讲 Gf/Gy/Gd/GRL 的角色，再讲动态 lambda。最后一定要落到区别：不是 raw signal 上做 DANN，而是在物理编码后的特征上做 DANN。

Time control:

If time is short, skip the formula details and keep the Gf-Gy-Gd-GRL logic.

---

## Slide 12 - Experimental Setup

Suggested time: 45 seconds

Main message: source is labeled CWRU; target is unlabeled high-speed train data.

English script:

We evaluate MDC-DAN in a cross-domain high-speed rail maintenance scenario.

The source domain is the public CWRU bearing dataset, with 12,880 labeled samples covering normal, inner race, outer race, and ball faults. The target domain contains 1,274 unlabeled samples from actual high-speed train bearings, around 600 rpm.

For preprocessing, signals are Z-score normalized and segmented using a sliding window of length 2048 with 50% overlap. The model is implemented in PyTorch, trained on an RTX 3090 GPU using Adam with a learning rate of 1e-3, batch size 64, for 50 epochs.

The most important protocol is that target labels are hidden during training and used only for final target-domain evaluation.

Chinese reminder:

这一页的关键是实验协议，不是硬件参数。目标域标签不可见一定要讲清楚。

Time control:

Keep under 45 seconds. Do not read the whole table line by line.

---

## Slide 13 - Main Results

Suggested time: 70 seconds

Main message: MDC-DAN substantially outperforms source-only baselines.

English script:

This is the main quantitative result.

We compare MDC-DAN with traditional machine learning baselines, including SVM and Random Forest, and deep learning baselines, including CNN and ResNet-18. These baselines are trained on source-domain data and directly tested on the target domain.

Traditional machine learning models suffer severely from the domain shift, with accuracy below 50%. CNN and ResNet-18 perform better, but still remain below 70%, which indicates that simply using a deeper neural network is not enough to solve the Sim-to-Real gap.

In contrast, MDC-DAN achieves 93.94% target-domain accuracy and an F1-score of 0.942. Compared with ResNet-18, the accuracy improvement is 28.14 percentage points.

This result supports two hypotheses. First, the Physics-Encoding Layer extracts robust mechanism anchors, such as BPFO and BPFI energy ratios. Second, adversarial adaptation successfully aligns the residual distribution gap for target-domain generalization.

Chinese reminder:

不要逐项读表。先说 baselines 都低，再说 MDC-DAN 93.94% 和 0.942，最后解释为什么：物理锚点 + 对抗对齐。

Time control:

This is one of the most important slides. You can spend about 70 seconds here.

---

## Slide 14 - Robustness and Deployment Efficiency

Suggested time: 45 seconds

Main message: the method is robust to lambda and efficient enough for edge deployment.

English script:

Besides accuracy, we also evaluate robustness and deployment efficiency.

For robustness, we study the adversarial trade-off parameter lambda. The best performance appears around 0.5 to 0.7, and the accuracy remains stable across a relatively wide range from 0.3 to 0.8. If lambda is too small, domain alignment is weak. If lambda is too large, the model may focus too much on confusing the discriminator and hurt classification.

The dynamic lambda-p schedule is also important because it avoids unstable adversarial gradients at the beginning of training.

For efficiency, MDC-DAN achieves an average inference time of 4.2 milliseconds per sample. Compared with heavier 2D-CNN pipelines that require image conversion, the computational cost is reduced by about 60%, which makes the method more suitable for edge deployment.

Chinese reminder:

这里讲两个工程价值：鲁棒性和效率。动态 lambda 是训练稳定性的细节，4.2 ms/sample 是部署价值。

Time control:

If time is short, mention only stable lambda range and 4.2 ms/sample.

---

## Slide 15 - Interpretability: t-SNE and SHAP

Suggested time: 60 seconds

Main message: the model makes decisions based on physically meaningful evidence.

English script:

Finally, we examine whether MDC-DAN learns the right evidence.

First, the t-SNE visualization shows feature distribution alignment. Before adaptation, source and target features are separated, which means the domain gap is large. After MDC-DAN, samples from the same fault class become more tightly clustered, regardless of whether they come from the source or target domain. This indicates that the learned representation is more domain-invariant.

Second, we use SHAP to interpret feature importance. SHAP assigns contribution values to the 15 input features. The most important features are BPFO Energy Ratio and BPFI Energy Ratio, which are directly related to bearing fault characteristic frequencies.

Therefore, MDC-DAN is not only accurate. It also relies on physically meaningful evidence rather than statistical shortcuts or background noise.

Chinese reminder:

这页回答审稿人/听众最关心的可信性问题：模型是不是学对了？t-SNE 看对齐，SHAP 看依据。结论是依赖物理有意义的特征。

Time control:

Do not explain SHAP formula unless asked in Q&A.

---

## Slide 16 - Conclusion

Suggested time: 35 seconds

Main message: summarize the method, limitation, and future work.

English script:

To conclude, MDC-DAN bridges the Sim-to-Real gap in digital-twin fault diagnosis by combining frozen physics priors with adversarial domain adaptation.

The main contributions are: first, a Physics-Encoding Layer that embeds bearing kinematic priors; second, adversarial adaptation that aligns residual source-target discrepancy; and third, interpretability analysis showing physically meaningful decision evidence.

One limitation is that the current implementation assumes known bearing geometry. In future work, we will address unknown-geometry scenarios through blind source adaptation, and improve robustness under non-stationary conditions using diffusion-based generation of physically consistent data.

Thank you for your attention. I am happy to take questions.

Chinese reminder:

结尾要稳，不要加入新内容。局限性要说成“我们已经知道并有未来方案”，避免显得方法不完整。

Time control:

End confidently. Leave time for Q&A.

---

# Q&A Preparation

## Q1: Why not use vanilla DANN directly?

Suggested answer:

Vanilla DANN aligns learned features directly from raw or statistical inputs. In noisy Sim-to-Real diagnosis, this may align noise patterns. MDC-DAN first applies a frozen Physics-Encoding Layer, so the adversarial module aligns mechanism-aware features rather than arbitrary statistical patterns.

中文理解：普通 DANN 可能对齐噪声；MDC-DAN 先用物理机制过滤/锚定，再对齐。

## Q2: Is the Physics-Encoding Layer just handcrafted feature engineering?

Suggested answer:

It is related to feature engineering, but the key difference is how it is integrated. In MDC-DAN, Phi-phy is formulated as a non-learnable network layer and becomes the input stage of an end-to-end domain adaptation architecture. It constrains the representation before adversarial learning.

中文理解：不是单独提特征后分类，而是作为网络结构里的 frozen layer，和 DANN 协同。

## Q3: What if bearing geometry is unknown?

Suggested answer:

The current implementation assumes known bearing geometry for calculating theoretical fault frequencies. This is a limitation. Future work will address unknown-geometry scenarios through blind source adaptation and adaptive frequency learning.

中文理解：承认限制，但强调这是 future work。

## Q4: Why is target accuracy so much higher than ResNet-18?

Suggested answer:

ResNet-18 is trained on source-domain raw signals and can overfit source-specific statistics. MDC-DAN combines mechanism-aware features with adversarial domain alignment, which improves target-domain generalization under distribution shift.

中文理解：不是网络越深越好，关键是物理锚点和跨域对齐。

## Q5: What do t-SNE and SHAP prove?

Suggested answer:

t-SNE provides visual evidence that source and target features become better aligned after adaptation. SHAP provides feature-level evidence that mechanism-related features, especially BPFO and BPFI energy ratios, contribute strongly to the prediction. Together they support both domain alignment and physical consistency.

中文理解：t-SNE 证明对齐，SHAP 证明依据正确。

