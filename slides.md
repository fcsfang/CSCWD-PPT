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

<div class="cover-summary mt-8">
  Target-domain accuracy: <strong>93.94%</strong> · F1-score: <strong>0.942</strong> · Inference: <strong>4.2 ms/sample</strong>
</div>

<!--
English:
Good morning / afternoon. Today I will present MDC-DAN, a mechanism-data collaborative domain adaptation framework for Sim-to-Real fault diagnosis in digital twins. The central idea is to combine fixed physics priors from bearing dynamics with adversarial domain adaptation, so that the model can transfer from labeled laboratory data to unlabeled real train data.

中文：
大家好，我今天汇报的工作是 MDC-DAN：面向数字孪生 Sim-to-Real 故障诊断的机制-数据协同领域自适应方法。核心思想是把轴承故障机理作为固定的物理先验嵌入网络，再结合对抗式领域自适应，实现从有标签实验室数据到无标签真实列车数据的迁移。
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
English:
I will organize the talk in four parts. First, I introduce the Sim-to-Real gap in digital-twin fault diagnosis. Then I explain the proposed MDC-DAN framework. After that, I present the experimental results and interpretability analysis. Finally, I conclude with the main takeaway and future work.

中文：
今天的汇报分为四部分。首先介绍数字孪生故障诊断中的 Sim-to-Real gap；然后讲解 MDC-DAN 的方法设计；接着展示实验结果、鲁棒性和可解释性分析；最后总结主要结论和未来工作。
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
English:
This slide clarifies the Sim-to-Real gap. The source domain comes from controlled laboratory or digital-twin conditions, where labels are available and signals are cleaner. The target domain comes from physical high-speed train assets, where the signal is noisy, operating conditions change, and labels are unavailable during training. Therefore, the key challenge is target-domain generalization under distribution shift.

中文：
这一页强调 Sim-to-Real gap。源域来自受控实验台或数字孪生环境，数据相对干净并且有标签；目标域来自真实高速列车轴承，噪声更强、工况变化更明显，而且训练阶段没有目标域标签。因此核心挑战不仅是故障分类，而是在分布偏移下实现目标域泛化。
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
English:
Pure data-driven alignment is helpful, but it can be unsafe in a noisy Sim-to-Real setting. It may align noise patterns, it has no explicit check against bearing mechanics, and it may cause negative transfer. This table also previews how MDC-DAN responds: physics encoding anchors the evidence before adversarial alignment.

中文：
这一页解释为什么已有的纯数据驱动 DA 还不够。关键不是否定领域对抗学习，而是指出如果没有物理一致性约束，模型可能对齐的是噪声而不是故障语义，甚至带来负迁移。表格右侧也提前对应了 MDC-DAN 的解决思路：先用物理编码锚定证据，再做领域对齐。
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
English:
Here is the formal setting. We have labeled source samples and unlabeled target samples. The core UDA constraint is highlighted at the bottom: target-domain labels are strictly unavailable during training and used only for final evaluation. The goal is to learn a representation that is both discriminative for fault classes and invariant across source and target domains.

中文：
这里给出任务形式化。源域样本有故障标签，目标域样本没有标签。底部高亮的是 UDA 的核心约束：训练过程中目标域标签严格不可见，只在最终评估时使用。目标是学习一个既能区分故障类别、又能跨源域和目标域保持一致的表示。
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
English:
The key idea is physics first and alignment second. Physics priors first lock mechanism invariants, so adversarial learning does not simply align noise with noise. It instead adapts the residual domain difference after fault evidence has been made mechanism-aware.

中文：
这一页是方法的入口：先物理、后对齐。物理先验先锁定不变量，对抗学习再对齐剩余差异，避免把噪声对齐成噪声。
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
English:
These three contributions directly respond to the three gaps discussed earlier. C1 addresses the lack of mechanism constraints. C2 reduces the risk of aligning noise by aligning physics-grounded features. C3 provides interpretability evidence to check whether the model is using meaningful fault mechanisms.

中文：
这三点贡献和前面的问题形成闭环。C1 解决缺少机理约束的问题；C2 在物理特征基础上做对抗对齐，降低对齐噪声的风险；C3 用 t-SNE 和 SHAP 做可解释性验证，检查模型是否真正依赖有意义的故障机理。
-->

---
layout: default
---

<div class="kicker">MDC-DAN Framework</div>

# Conceptual Pipeline

<FrameworkDiagram />

<div class="note mt-6">
  The simplified pipeline separates physics encoding, latent fault representation, and adversarial alignment.
</div>

<!--
English:
This slide gives a pipeline-level view. Source and target signals first pass through the frozen physics layer and become hphy in a 15-dimensional mechanism feature space. Gf then learns the latent representation z, which branches into fault prediction and adversarial domain alignment.

中文：
这一页给出 pipeline 级别的结构。源域和目标域信号首先经过 frozen 的物理编码层，得到 15 维机制特征 hphy；随后 Gf 学习潜在表示 z，并分支到故障预测和领域对抗对齐。
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
  The full architecture expands the simplified pipeline into two concrete components: a frozen Physics-Encoding Layer and a trainable Domain-Adversarial Module.
</div>

<!--
English:
After the simplified view, this slide presents the full MDC-DAN architecture. The left part corresponds to the physics encoding process, where raw vibration signals are transformed into mechanism-aware features. The right part is the adversarial adaptation module, which aligns source and target representations while preserving fault-discriminative information.

中文：
在简化图之后，这里展示论文中的完整总体架构图。左侧对应物理编码过程，将原始振动信号转化为机制感知特征；右侧对应领域对抗模块，在保持故障分类能力的同时对齐源域和目标域表示。
-->

---
layout: default
zoom: 0.9
---

<div class="kicker">Physics-Encoding Layer</div>

# Physics-Encoding Layer

<PhysicsEncoding />

<div class="formula-grid physics-formula-grid mt-4">
  <FormulaCard title="Layer mapping">
    h<sub>phy</sub> = Φ<sub>phy</sub>(x) = [ψ<sub>stat</sub>(x) ⊕ ψ<sub>mech</sub>(x) ⊕ ψ<sub>freq</sub>(x)]<sup>T</sup>
  </FormulaCard>
  <FormulaCard title="BPFO example">
    f<sub>BPFO</sub> = N/2 · f<sub>r</sub>(1 − d/D · cos α)
  </FormulaCard>
</div>

<div class="caption mt-2">N: rolling elements; f<sub>r</sub>: shaft frequency; d/D: rolling-element and pitch diameters; α: contact angle.</div>

<div class="key-point mt-3">
  Key point: frozen Φ<sub>phy</sub> is determined by rotor dynamics, not learned from data.
</div>

<!--
English:
The important point is that this is not just ordinary feature engineering. Φphy is a frozen, non-learnable network layer determined by rotor dynamics. For example, BPFO depends on the number of rolling elements N, shaft frequency fr, rolling element diameter d, pitch diameter D, and contact angle α. These parameters connect the network input to bearing kinematics.

中文：
这里要强调：Physics-Encoding Layer 不是普通特征工程，而是一个 frozen、non-learnable 的网络层，由转子动力学先验决定。以 BPFO 为例，公式中的 N 是滚动体个数，fr 是转轴转频，d 和 D 分别对应滚动体直径和节圆直径，α 是接触角。这些几何和运动参数把网络输入和轴承故障机理直接联系起来。
-->

---
layout: default
zoom: 0.88
---

<div class="kicker">Domain-Adversarial Module</div>

# Domain-adversarial learning on mechanism-aligned features

<AdversarialModule />

<div class="dann-points">
  <div class="dann-point">
    <h3>Gf learns fault features</h3>
    <p>Physics-aligned 15-D features are mapped into a latent space for diagnosis.</p>
  </div>
  <div class="dann-point">
    <h3>Gd distinguishes domains</h3>
    <p>The discriminator predicts whether a feature comes from source or target.</p>
  </div>
  <div class="dann-point">
    <h3>GRL makes Gf fool Gd</h3>
    <p>Gradient reversal encourages domain-invariant features while Gy preserves fault labels.</p>
  </div>
</div>

<div class="formula-label mt-4">Training objective</div>

$$
\mathcal{E}(\theta_f,\theta_y,\theta_d)
= \mathcal{L}_y(\theta_f,\theta_y)
- \lambda_p \mathcal{L}_d(\theta_f,\theta_d)
$$

<div class="caption mt-2">A dynamic λ<sub>p</sub> schedule gradually strengthens adversarial adaptation.</div>

<div class="dann-summary mt-3">
  MDC-DAN aligns mechanism-aware features h<sub>phy</sub>, rather than raw statistical patterns.
</div>

<!--
English:
This module follows the DANN logic. Gf learns latent fault features from hphy. Gy keeps the representation discriminative for source fault labels. Gd tries to distinguish source from target, while the gradient reversal layer makes Gf fool Gd. The important difference from vanilla DANN is that alignment happens after physics encoding, so the aligned evidence is mechanism-aware instead of purely statistical.

中文：
这一页重点讲 DANN 的对抗逻辑。Gf 从 hphy 中学习潜在故障特征，Gy 保证源域故障分类能力，Gd 判断特征来自源域还是目标域，而 GRL 反转梯度，使 Gf 学到能够欺骗 Gd 的域不变表示。和 vanilla DANN 的关键区别是：这里的对齐发生在物理编码之后，因此对齐的是机制感知特征，而不是原始统计模式。
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
English:
The evaluation uses a practical cross-domain setting. The source domain is CWRU with 12,880 labeled samples, and the target domain is real high-speed train bearing data with 1,274 unlabeled samples around 600 rpm. The target labels are hidden during training, so this is an unsupervised domain adaptation experiment.

中文：
实验设置是一个真实的跨域迁移场景。源域使用 CWRU 数据集，共 12,880 个有标签样本；目标域是真实高速列车轴承数据，约 600 rpm，共 1,274 个无标签样本。训练时目标域标签不可见，因此这是无监督领域自适应实验。
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
English:
The main result is that MDC-DAN reaches 93.94% target-domain accuracy and an F1-score of 0.942. Compared with ResNet-18, the accuracy improves by 28.14 percentage points. This suggests that simply using a deeper neural network is not enough; the combination of physics anchoring and domain alignment is the key.

中文：
这一页不需要逐行读数。重点是 MDC-DAN 在目标域达到 93.94% 准确率和 0.942 的 F1-score，相比 ResNet-18 提升 28.14 个百分点。这说明单纯加深网络并不能解决 Sim-to-Real gap，关键在于物理锚点和领域对齐的协同。
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
English:
This page adds two practical messages. First, the method is not extremely sensitive to λ; performance remains stable from 0.3 to 0.8, with the best region around 0.5 to 0.7. Second, the dynamic λp schedule helps avoid unstable gradients early in adversarial training. The average inference time is 4.2 ms per sample, which is suitable for lightweight deployment.

中文：
这一页补充工程部署价值。第一，方法对 λ 并不极端敏感，在 0.3 到 0.8 范围内表现较稳定，最佳区域大约在 0.5 到 0.7。第二，动态 λp 策略可以避免训练初期对抗梯度过强导致的不稳定。推理速度为每个样本 4.2 ms，适合轻量化部署场景。
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
English:
The interpretability analysis checks whether the model learns the right evidence. t-SNE shows that source and target samples from the same fault class become better aligned after adaptation. SHAP shows that mechanism-related energy features, especially BPFO and BPFI, contribute strongly to the prediction. In short, the model makes decisions for the right reason.

中文：
这一页回答模型是否“学对了”。t-SNE 表明适应后同一故障类别的源域和目标域样本聚得更近；SHAP 表明 BPFO、BPFI 等机理相关能量特征贡献最高。也就是说，模型不是依赖背景噪声或偶然统计模式，而是在用正确的物理原因做决策。
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
  <div class="limitation-block">
    <h2>Limitation</h2>
    <p>Current implementation assumes known bearing geometry; future work addresses unknown-geometry scenarios via blind source adaptation.</p>
  </div>
  <div class="future-block">
    <h2>Future Work</h2>
    <ul>
      <li>Blind source adaptation for unknown-geometry scenarios.</li>
      <li>Diffusion-based generation of physically consistent nonstationary data.</li>
    </ul>
  </div>
</div>

## Thank you. Questions?

<!--
English:
To conclude, MDC-DAN bridges the Sim-to-Real gap by combining a non-learnable physics encoding layer with adversarial domain adaptation. The current implementation assumes known bearing geometry, and future work addresses unknown-geometry scenarios via blind source adaptation. Another direction is diffusion-based generation of physically consistent nonstationary data.

中文：
最后总结一下，MDC-DAN 通过非可学习的物理编码层和对抗式领域自适应相结合，缩小数字孪生故障诊断中的 Sim-to-Real gap。当前实现假设轴承几何参数已知，后续会通过 blind source adaptation 处理未知几何场景；另一个方向是基于扩散模型生成物理一致的非平稳数据。谢谢大家，欢迎提问。
-->
