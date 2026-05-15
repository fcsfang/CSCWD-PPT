---
theme: academic
title: MDC-DAN CSCWD 2026
info: |
  Academic presentation deck for the paper
  "MDC-DAN: Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins".
drawings:
  persist: false
transition: fade
themeConfig:
  paginationX: ""
  paginationY: ""
layout: cover
hideInToc: true
class: cover
coverDate: ""
---

<div class="cover-logos">
  <img src="/figures/IEEELOGO.png" alt="IEEE logo" class="ieee-logo" />
  <img src="/figures/CSCWDLOGO.gif" alt="CSCWD logo" class="cscwd-logo" />
</div>

<div class="kicker">CSCWD 2026 · Presentation</div>

# MDC-DAN

## Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins

<div class="thesis">
Bridging the Sim-to-Real gap by combining physics priors with adversarial domain adaptation.
</div>

<div class="cover-authors">
<strong>Presenter:</strong> Chuanshan Fang
</div>

<div class="cover-author-list">
Authors: Chuanshan Fang, Hongyan Qian, Yongpeng Lin, Sijie Ning, and Zhuqing Xu
</div>

<div class="cover-affiliations">
  <div>College of Computer Science and Technology</div>
  <div>Nanjing University of Aeronautics and Astronautics</div>
  <div>State Key Laboratory for Novel Software Technology, Nanjing University</div>
</div>

<!--
Slide 1: Title
Time: 40 seconds

Spoken script:
Good afternoon, distinguished professors, teachers, and fellow students. I am Chuanshan Fang from Nanjing University of Aeronautics and Astronautics.

Today, I will present our work entitled MDC-DAN: Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins.

The central problem of this work is the Sim-to-Real gap. In fault diagnosis, a model trained on clean laboratory or digital-twin data often cannot be directly deployed to noisy physical assets, because the source-domain and target-domain data distributions are different.

To address this problem, our key idea is to combine physics priors from rotor dynamics with adversarial domain adaptation. In this way, the model can use labeled source-domain data and unlabeled target-domain data at the same time, and improve target-domain generalization.

Chinese note:
开场要稳。第一页只讲背景和核心思想，不展开方法细节。IEEE 和 CSCWD logo 在右上角，不需要专门解释。
-->

---
layout: default
---

<div class="kicker">Outline</div>

# Presentation Outline

<div class="outline-list">
  <div class="outline-item">
    <div class="outline-num">01</div>
    <div>
      <h3>Background & Motivation</h3>
      <p>Why digital-twin diagnosis suffers from a Sim-to-Real distribution gap.</p>
    </div>
  </div>
  <div class="outline-item">
    <div class="outline-num">02</div>
    <div>
      <h3>Proposed Method: MDC-DAN</h3>
      <p>How physics encoding and adversarial adaptation are combined.</p>
    </div>
  </div>
  <div class="outline-item">
    <div class="outline-num">03</div>
    <div>
      <h3>Experiments & Analysis</h3>
      <p>Cross-domain results, robustness, efficiency, t-SNE, and SHAP.</p>
    </div>
  </div>
  <div class="outline-item">
    <div class="outline-num">04</div>
    <div>
      <h3>Conclusion</h3>
      <p>Main takeaway and future research directions.</p>
    </div>
  </div>
</div>

<!--
Slide 2: Presentation Outline
Time: 30 seconds

Spoken script:
This presentation is organized into four parts.

First, I will introduce the background and motivation, especially why the Sim-to-Real gap is a critical challenge for digital-twin fault diagnosis.

Second, I will present the proposed method, MDC-DAN, including the Physics-Encoding Layer and the Domain-Adversarial Module.

Third, I will show the experimental setup, main results, robustness analysis, efficiency analysis, and interpretability results.

Finally, I will conclude with the main takeaway, current limitation, and future work.

Chinese note:
这一页是路线图，语速可以快一些，但每一项都要读出来。
-->

---
layout: default
---

<div class="kicker">Motivation</div>

# Sim-to-Real gap limits digital-twin diagnosis

<p class="big-statement compact-statement">
Same fault mechanism, different data distribution.
</p>

<div class="motivation-domain">
  <DomainGap />
</div>

<div class="motivation-implication">
  The key challenge is not only fault classification, but target-domain generalization under distribution shift.
</div>

<!--
Slide 3: Motivation
Time: 65 seconds

Spoken script:
This slide explains the motivation of our work.

In digital-twin fault diagnosis, the source domain usually comes from laboratory or digital-twin environments. These data are clean, controlled, and labeled, so they are suitable for supervised training.

The target domain is different. It comes from real physical assets, such as high-speed train bearings. The signals are noisy, the operating speed may vary, and target labels are unavailable during training.

The key observation is shown in the center. The bearing fault mechanism can be the same, but the data distributions are different. In mathematical form, P of X source is not equal to P of X target.

So the challenge is not only fault classification. It is target-domain generalization under Sim-to-Real distribution shift.

Chinese note:
这一页要把图讲完整：左边源域，右边目标域，中间是分布偏移。核心句是：same fault mechanism, different data distribution。
-->

---
layout: default
---

<div class="kicker">Research Gap</div>

# Pure data-driven alignment lacks physical consistency

<p class="big-statement">Distribution alignment is useful, but unsafe when it aligns the wrong evidence.</p>

<table class="research-table mt-6">
  <thead>
    <tr>
      <th>Limitation of pure data-driven DA</th>
      <th>Why it matters in Sim-to-Real diagnosis</th>
      <th>MDC-DAN response</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Noise alignment</strong></td>
      <td>May align noise rather than fault semantics.</td>
      <td>Mechanism features anchor the representation before adversarial alignment.</td>
    </tr>
    <tr>
      <td><strong>No mechanism check</strong></td>
      <td>Lacks explicit bearing kinematic constraints.</td>
      <td>Φ<sub>phy</sub> introduces rotor-dynamics priors as a frozen network layer.</td>
    </tr>
    <tr>
      <td><strong>Negative transfer</strong></td>
      <td>Unconstrained alignment may hurt target diagnosis.</td>
      <td>Domain adaptation is applied after physics-consistent encoding.</td>
    </tr>
  </tbody>
</table>

<!--
Slide 4: Research Gap
Time: 75 seconds

Spoken script:
This slide summarizes the research gap of pure data-driven domain adaptation.

The table has three rows. Each row shows one limitation, why it matters, and how MDC-DAN responds.

First, noise alignment. If a model only tries to make source and target features look similar, it may align noise patterns rather than fault semantics. MDC-DAN responds by using mechanism features as anchors before adversarial alignment.

Second, no mechanism check. Pure data-driven methods usually do not explicitly check whether the learned features follow bearing kinematics. MDC-DAN introduces Phi-phy, a frozen Physics-Encoding Layer, to embed rotor-dynamics priors into the network.

Third, negative transfer. Unconstrained alignment may even hurt target-domain diagnosis. MDC-DAN reduces this risk by applying domain adaptation after physics-consistent encoding.

The main message is: distribution alignment is useful, but it should be guided by physical consistency.

Chinese note:
这一页一定要逐行解释表格，不能只说“有三个问题”。老师指出的就是这里。按三行讲：noise alignment、no mechanism check、negative transfer，每行都解释“问题是什么、为什么重要、MDC-DAN 怎么解决”。
-->

---
layout: default
---

<div class="kicker">Problem Setting</div>

# Unsupervised domain adaptation for bearing faults

<ProblemSetting />

<div class="uda-constraint mt-5">
  Target-domain labels are unavailable during training and used only for evaluation.
</div>

<!--
Slide 5: Problem Setting
Time: 60 seconds

Spoken script:
This slide gives the formal problem setting. The task is unsupervised domain adaptation for bearing fault diagnosis.

On the source-domain side, we have labeled samples. Each source sample contains a vibration signal segment and a fault label.

On the target-domain side, we have unlabeled samples from real operating conditions. During training, target-domain labels are not available.

The central assumption is domain shift: P of X source is not equal to P of X target. This shift comes from speed variation, noise, and the difference between laboratory and real deployment environments.

The goal is to learn a diagnostic function that performs well on the target domain. The highlighted constraint is the key point: target-domain labels are hidden during training and used only for evaluation.

Chinese note:
这页要强调 UDA 设定。目标域标签训练时不可见，这是实验严谨性的关键。
-->

---
layout: statement
---

# Key Idea

<div class="big-statement">
Physics first, alignment second: use rotor-dynamics priors to anchor the representation, then use adversarial learning to close the residual domain gap.
</div>

<div class="idea-flow mt-10">
  <div class="idea-node">Physical prior</div>
  <div class="idea-edge"><span>lock mechanism invariants</span></div>
  <div class="idea-node">Mechanism-aligned representation</div>
  <div class="idea-edge"><span>preserve fault evidence</span></div>
  <div class="idea-node">Adversarial adaptation</div>
  <div class="idea-edge"><span>align residual shift, not noise</span></div>
  <div class="idea-node">Domain-invariant diagnosis</div>
</div>

<div class="idea-explanation mt-8">
  Mechanism priors constrain what should remain invariant; adversarial learning adapts what still differs across domains.
</div>

<!--
Slide 6: Key Idea
Time: 60 seconds

Spoken script:
This slide gives the key idea of MDC-DAN.

The idea is: physics first, alignment second.

First, physical priors from rotor dynamics lock mechanism invariants. For bearing diagnosis, the stable evidence is not arbitrary waveform shape, but energy patterns around theoretical fault frequencies.

Second, the signal is transformed into a mechanism-aligned representation, so important fault evidence is preserved across domains.

Third, adversarial adaptation is applied after physics encoding. Therefore, the model aligns the residual source-target gap in a mechanism-aware feature space.

This order is important. Physics priors reduce the risk of aligning noise with noise, and adversarial learning adapts what still differs across domains.

Chinese note:
这一页是核心思想。要讲清楚顺序为什么重要：先机理、后对齐。
-->

---
layout: default
---

<div class="kicker">Contributions</div>

# Three contributions

<div class="contribution-list">
  <div class="contribution-row">
    <div class="contribution-index">C1</div>
    <div>
      <h3>Physics-embedded network design</h3>
      <p>A frozen Physics-Encoding Layer embeds rotor dynamics directly into the network input.</p>
      <span class="gap-link">Addresses: no mechanism check</span>
    </div>
  </div>
  <div class="contribution-row">
    <div class="contribution-index">C2</div>
    <div>
      <h3>Collaborative adversarial adaptation</h3>
      <p>Aligns residual source-target discrepancy after physics encoding.</p>
      <span class="gap-link">Addresses: noise alignment</span>
    </div>
  </div>
  <div class="contribution-row">
    <div class="contribution-index">C3</div>
    <div>
      <h3>Trustworthy interpretability</h3>
      <p>t-SNE and SHAP verify that the learned decision evidence is physically meaningful.</p>
      <span class="gap-link">Addresses: negative transfer risk</span>
    </div>
  </div>
</div>

<!--
Slide 7: Contributions
Time: 60 seconds

Spoken script:
This slide summarizes three contributions.

First, we design a physics-embedded network structure. The frozen Physics-Encoding Layer embeds bearing kinematic priors at the network input, addressing the lack of mechanism check.

Second, we propose collaborative adversarial adaptation. Instead of aligning raw signals, the model aligns residual source-target discrepancy after physics encoding, reducing the risk of noise alignment.

Third, we provide trustworthy interpretability. t-SNE and SHAP are used to verify whether the decision evidence is physically meaningful.

Together, these contributions connect mechanism consistency, domain adaptation, and trustworthy decision evidence.

Chinese note:
第 7 页和第 4 页要形成闭环：C1 对 no mechanism check，C2 对 noise alignment，C3 对 negative transfer risk。
-->

---
layout: default
---

<div class="kicker">MDC-DAN Framework</div>

# Full architecture of MDC-DAN

<figure class="framework-paper-figure">
  <img src="/figures/framework-paper.png" alt="Full MDC-DAN architecture" />
  <figcaption class="caption">Figure: Overall MDC-DAN architecture.</figcaption>
</figure>

<div class="note mt-4">
  The architecture consists of two concrete components: a frozen Physics-Encoding Layer and a trainable Domain-Adversarial Module.
</div>

<!--
Slide 8: Full Architecture of MDC-DAN
Time: 55 seconds

Spoken script:
This slide shows the full architecture of MDC-DAN.

The architecture has two main parts.

The left part is the Physics-Encoding Layer. It receives raw vibration signals and extracts physics-aligned features. This part is non-learnable, and its calculation paths are determined by rotor dynamics.

The right part is the Trainable Domain-Adversarial Module. It learns domain-invariant latent features while preserving source-domain fault classification ability.

Therefore, MDC-DAN is a dual-stage design: physical laws first constrain the representation, and data-driven adversarial learning then adapts it across domains.


Answer1:

It is related to physical feature extraction, but it is not just a standalone handcrafted feature module.

In MDC-DAN, the Physics-Encoding Layer is integrated into the network as a frozen, non-learnable layer. Its role is to provide physical priors before the trainable feature extractor and adversarial adaptation module.

So the final model is not purely handcrafted. It combines physics priors with data-driven domain adaptation.

Answer2:

Yes, it may reduce some flexibility, but this is intentional.

The frozen layer keeps stable physical fault information. The later feature extractor and adversarial module are still trainable, so they provide the flexibility to adapt to the target domain.

In short, the frozen layer gives physical stability, and the trainable modules give adaptation ability.
-->

---
layout: default
zoom: 0.86
---

<div class="kicker">Physics-Encoding Layer</div>

# Physics-Encoding Layer

<PhysicsEncodingFigure />

<!--
Slide 9: Physics-Encoding Layer
Time: 90 seconds

Spoken script:
Now I will explain the Physics-Encoding Layer in more detail.

The left side shows the physical encoding process. MDC-DAN first converts the vibration signal into mechanism-informed features, instead of directly feeding the raw signal into a fully learnable network.

Starting from the vibration signal, the layer performs envelope spectrum analysis. Bearing geometry provides physical prior information, and the characteristic-frequency formula gives calculated fault frequencies. The model then extracts energy around these meaningful frequency locations.

The right side summarizes the output: a fifteen-dimensional physics-aligned feature vector.

The first row is time statistics, from f-one to f-six, describing vibration severity and impulsiveness.

The second row is mechanism energy, from f-seven to f-twelve. These are energy ratios around BPFO, BPFI, BSF, FTF, and their second harmonics. This is the core physical part.

The third row is frequency statistics, from f-thirteen to f-fifteen, describing the global frequency-distribution shape.

The first formula gives the layer mapping: h-phy equals Phi-phy of x. The second formula gives BPFO as an example. Here, N is the number of rolling elements, f-r is shaft frequency, d and D describe bearing geometry, and alpha is the contact angle.

The key point is that Phi-phy is frozen. It is determined by rotor dynamics, not learned from data.

Chinese note:
这一页现在先讲左侧论文配图：vibration signal、envelope spectrum、bearing geometry、calculated fault frequencies、mechanism energy。然后再讲右侧三类特征和两个公式。重点仍然是 frozen Phi-phy 由轴承动力学决定，不是从数据中学习出来的。
-->

---
layout: default
zoom: 0.88
---

<div class="kicker">Domain-Adversarial Module</div>

# Domain-adversarial learning on mechanism-aligned features

<DomainAdversarialFigure />

<!--
Slide 10: Domain-Adversarial Module
Time: 90 seconds

Spoken script:
After physics encoding, h-phy is fed into the Domain-Adversarial Module.

The left side shows the trainable module cropped from the overall architecture. It starts from the fifteen-dimensional mechanism-aware feature vector produced by the Physics-Encoding Layer.

The input first enters the feature extractor, which maps it into a latent representation. This representation then connects to two objectives.

The upper branch is the label predictor. It predicts the fault category using source-domain labels.

The lower branch is the domain-adversarial branch. It contains the Gradient Reversal Layer and the domain discriminator, which predicts whether a feature comes from source or target.

The adversarial logic is simple: G-d tries to distinguish domains, while GRL makes G-f learn features that fool G-d. As a result, the latent representation becomes more domain-invariant.

The training objective combines classification loss and domain adversarial loss, with lambda-p controlling the alignment strength.

The key difference from vanilla DANN is that MDC-DAN aligns mechanism-aware features, rather than raw statistical patterns.

Chinese note:
这一页现在先讲左侧论文模块图：physics-aligned input、feature extractor、label predictor、GRL、domain discriminator。再讲右侧三点和训练目标。重点强调它不是直接对齐原始信号，而是在 Physics-Encoding Layer 之后对齐机制感知特征。
-->

---
layout: default
---

<div class="kicker">Experiments</div>

# Cross-domain high-speed rail maintenance scenario

<table class="experiment-table mt-5">
  <thead>
    <tr>
      <th>Aspect</th>
      <th>Experimental setting</th>
      <th>Purpose in evaluation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Source domain</strong></td>
      <td>CWRU benchmark bearing data; <strong>12,880 labeled samples</strong>; Normal, Inner Race, Outer Race, Ball faults.</td>
      <td>Provides labeled laboratory / digital-twin knowledge.</td>
    </tr>
    <tr>
      <td><strong>Target domain</strong></td>
      <td>Actual high-speed train bearing data around <strong>600 rpm</strong>; <strong>1,274 unlabeled samples</strong>.</td>
      <td>Tests Sim-to-Real transfer under realistic operating noise.</td>
    </tr>
    <tr>
      <td><strong>Preprocessing</strong></td>
      <td>Z-score normalization; sliding window <strong>L = 2048</strong>; 50% overlap.</td>
      <td>Forms fixed-length vibration windows for physics encoding.</td>
    </tr>
    <tr>
      <td><strong>Training</strong></td>
      <td>PyTorch, RTX 3090, Adam, lr = 1e-3, batch size 64, 50 epochs.</td>
      <td>UDA protocol: target labels are hidden during training and used only for evaluation.</td>
    </tr>
  </tbody>
</table>

<div class="note mt-7">
  UDA protocol: target labels are hidden during training and are used only for final target-domain evaluation.
</div>

<!--
Slide 11: Experimental Setup
Time: 80 seconds

Spoken script:
This slide presents the experimental setup.

The table has four rows: source domain, target domain, preprocessing, and training.

The source domain is the CWRU bearing dataset. It contains twelve thousand eight hundred and eighty labeled samples, including normal, inner race fault, outer race fault, and ball fault. It provides labeled laboratory knowledge.

The target domain is real high-speed train bearing data, around six hundred RPM. It contains one thousand two hundred and seventy-four target samples, treated as unlabeled during training. This tests Sim-to-Real transfer under realistic noise.

For preprocessing, we use Z-score normalization and a sliding window with length L equals two thousand and forty-eight and fifty percent overlap.

For training, the model uses PyTorch, RTX thirty ninety GPU, Adam optimizer, learning rate one e minus three, batch size sixty-four, and fifty epochs.

The key protocol is at the bottom: target labels are hidden during training and used only for final evaluation.

Chinese note:
这一页是表格页，也要逐行解释。特别强调 target labels hidden during training。
-->

---
layout: default
---

<div class="kicker">Main Results</div>

# MDC-DAN gains +28.14 pp over ResNet-18

<div class="results-layout">
  <ResultBars />
  <div class="result-summary">
    <div class="result-item">
      <span>Accuracy</span>
      <strong>93.94%</strong>
    </div>
    <div class="result-item accent">
      <span>Gain over ResNet-18</span>
      <strong>+28.14 pp</strong>
    </div>
    <div class="result-item">
      <span>F1-score</span>
      <strong>0.942</strong>
    </div>
  </div>
</div>

<div class="note mt-5">
  Physics-grounded representation and adversarial alignment jointly improve target-domain generalization under Sim-to-Real shift.
</div>

<!--
Slide 12: Main Results
Time: 95 seconds

Spoken script:
This slide shows the main diagnostic results on the real-world target domain.

The chart compares different methods by target-domain accuracy. The key result is that MDC-DAN achieves ninety-three point nine four percent accuracy, an F-one score of zero point nine four two, and improves over ResNet eighteen by twenty-eight point one four percentage points.

The baselines show the difficulty of the task. SVM reaches forty-two point one five percent, and Random Forest reaches forty-eight point six two percent. These traditional methods suffer strongly from the source-target shift.

CNN improves to sixty-one point three zero percent, and ResNet eighteen reaches sixty-five point eight zero percent. However, deeper source-only networks still cannot solve the domain shift by themselves.

In contrast, MDC-DAN combines mechanism features with domain adaptation. This result suggests that physics-grounded representation and adversarial alignment jointly improve target-domain generalization.

Chinese note:
这一页是结果页，不能只读三个 KPI。要解释每个 baseline 为什么低，以及 MDC-DAN 为什么高。注意说 “percentage points”，不要说 percent improvement。
-->

---
layout: default
---

<div class="kicker">Robustness & Efficiency</div>

# Sensitivity and deployment efficiency

<div class="two-grid">
  <figure class="figure-frame">
    <img src="/figures/sensitivity.png" alt="Sensitivity analysis" />
    <figcaption class="caption">Figure: Sensitivity of adversarial trade-off parameter λ on target-domain accuracy.</figcaption>
  </figure>
  <div class="analysis-groups">
    <div class="analysis-group">
      <h3>Robustness</h3>
      <ul class="small-list">
        <li>Best performance appears around <strong>λ = 0.5 to 0.7</strong>.</li>
        <li>Accuracy remains stable across <strong>[0.3, 0.8]</strong>.</li>
        <li>The dynamic λ<sub>p</sub> schedule stabilizes early adversarial training.</li>
      </ul>
    </div>
    <div class="analysis-group">
      <h3>Efficiency</h3>
      <ul class="small-list">
        <li>Average inference time is <strong>4.2 ms per sample</strong>.</li>
        <li>Computational cost is reduced by approximately <strong>60%</strong> compared with heavy 2D-CNN image-conversion pipelines.</li>
      </ul>
    </div>
  </div>
</div>

<!--
Slide 13: Robustness and Efficiency
Time: 70 seconds

Spoken script:
This slide evaluates robustness and deployment efficiency.

The left figure shows the sensitivity of the adversarial parameter lambda. If lambda is too small, domain alignment is weak. If lambda is too large, the model may focus too much on confusing the discriminator.

The best region appears around zero point five to zero point seven, and accuracy remains stable from zero point three to zero point eight. This means the method is not extremely sensitive to the exact lambda value.

The dynamic lambda-p schedule also helps training. It starts with weaker adversarial pressure and gradually strengthens domain alignment.

For efficiency, the average inference time is four point two milliseconds per sample, and the computational cost is reduced by approximately sixty percent compared with heavier two-D CNN image-conversion pipelines.

So MDC-DAN is accurate, robust, and suitable for lightweight deployment.

Chinese note:
讲清楚 lambda 太小和太大的问题。效率部分要强调 4.2 ms/sample 和 60% reduction。
-->

---
layout: default
zoom: 0.9
---

<div class="kicker">Interpretability</div>

# t-SNE and SHAP verify physical consistency

<EvidencePair
  left="/figures/tsne.png"
  left-title="t-SNE: features align after MDC-DAN"
  right="/figures/shap.png"
  right-title="SHAP: BPFO/BPFI energy dominates"
/>

<div class="observation-list mt-4">
  <div class="evidence-row"><strong>Observation 1</strong><span>t-SNE shows tighter source-target clustering within the same fault class after adaptation.</span></div>
  <div class="evidence-row"><strong>Observation 2</strong><span>SHAP assigns high importance to mechanism-related BPFO/BPFI energy features.</span></div>
  <div class="evidence-row"><strong>Interpretation</strong><span>MDC-DAN relies on physically meaningful evidence rather than statistical shortcuts.</span></div>
</div>

<!--
Slide 14: Interpretability
Time: 80 seconds

Spoken script:
This slide checks whether MDC-DAN learns physically meaningful evidence.

The left figure is the t-SNE visualization. Before adaptation, source and target features are separated. After MDC-DAN, samples from the same fault class become more tightly clustered, even across domains. This indicates better domain-invariant representation.

The right figure is the SHAP analysis. SHAP shows which features contribute most to prediction.

The important result is that BPFO Energy Ratio and BPFI Energy Ratio have high importance. These features are directly related to bearing fault characteristic frequencies.

Therefore, MDC-DAN is not mainly relying on background noise or statistical shortcuts. It relies on physically meaningful evidence.

Chinese note:
这一页的逻辑是：t-SNE 证明域对齐，SHAP 证明依据正确。最后说 trustworthy。
-->

---
layout: end
hideInToc: true
class: end
---

# Conclusion

<p class="conclusion-sentence">
MDC-DAN bridges Sim-to-Real fault diagnosis by combining frozen physics priors with adversarial domain adaptation.
</p>

<div class="conclusion-grid">
  <div class="takeaway-block">
    <h2>Main Contributions</h2>
    <ul>
      <li>Physics-Encoding Layer embeds bearing kinematic priors.</li>
      <li>Adversarial adaptation aligns residual source-target discrepancy.</li>
      <li>t-SNE and SHAP support physically meaningful decision evidence.</li>
    </ul>
  </div>
  <div class="future-block">
    <h2>Future Work</h2>
    <ul>
      <li>Blind source adaptation for unknown-geometry scenarios.</li>
      <li>Diffusion-based generation of physically consistent nonstationary data.</li>
    </ul>
  </div>
</div>

<!--
Slide 15: Conclusion
Time: 50 seconds

Spoken script:
To conclude, this work proposes MDC-DAN for Sim-to-Real fault diagnosis in digital twins.

The main takeaway is that MDC-DAN bridges the Sim-to-Real gap by combining frozen physics priors with adversarial domain adaptation.

First, the Physics-Encoding Layer embeds bearing kinematic priors into the network input.

Second, adversarial adaptation aligns residual source-target discrepancy after physics encoding.

Third, t-SNE and SHAP support that the model uses physically meaningful decision evidence.

For future work, we will further study blind source adaptation for unknown-geometry scenarios, and investigate diffusion-based generation of physically consistent nonstationary data.

Chinese note:
结论页要稳，突出贡献和未来工作即可，不主动展开局限性。
-->

---
layout: end
hideInToc: true
class: end thanks
---

# Thank you.

## Questions?

<div class="contact-email">fcshan@nuaa.edu.cn</div>

<!--
Slide 16: Thank You
Time: 20 seconds

Spoken script:
Thank you very much for your attention.

I am happy to take your questions.

You can also contact me by email at fcshan@nuaa.edu.cn.

Chinese note:
这一页结束后停顿，看老师是否提问。不要急着自己补充内容。
-->
