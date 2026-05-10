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
  paginationX: ''
  paginationY: ''
layout: cover
hideInToc: true
class: cover
---

<div class="kicker">CSCWD 2026 · Oral Presentation</div>

# MDC-DAN

## Mechanism-Data Collaborative Domain Adaptation for Sim-to-Real Fault Diagnosis in Digital Twins

<div class="thesis">
Bridging the Sim-to-Real gap by combining physics priors with adversarial domain adaptation.
</div>

Chuanshan Fang, Hongyan Qian, Yongpeng Lin, Sijie Ning, Zhuqing Xu  
Nanjing University of Aeronautics and Astronautics · Nanjing University

<div class="metric-row mt-8">
  <div class="metric"><strong>93.94%</strong><span>Target-domain accuracy</span></div>
  <div class="metric"><strong>0.942</strong><span>Target-domain F1-score</span></div>
  <div class="metric"><strong>4.2 ms</strong><span>Inference per sample</span></div>
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

# Talk roadmap

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

# 1. Sim-to-Real gap limits digital-twin diagnosis

<div class="two-grid wide-left">
  <div>
    <p class="big-statement">A model trained on clean laboratory data may fail on noisy physical assets.</p>
    <ul class="small-list mt-5">
      <li>Digital Twins support predictive maintenance by linking virtual models and physical assets.</li>
      <li>But physical edge data are noisy, dynamic, and usually unlabeled.</li>
      <li>The paper formulates this as a distribution shift: <strong>P(X<sub>s</sub>) ≠ P(X<sub>t</sub>)</strong>.</li>
    </ul>
  </div>
  <DomainGap />
</div>

<!--
English:
The motivation is simple: a model trained on clean laboratory data does not necessarily work on real physical assets. In digital twins, the source domain may be well controlled and labeled, while the target domain is noisy, dynamic, and usually unlabeled. So the first message is that this is a domain adaptation problem, not just a standard classification problem.

中文：
这一页只讲问题本身：在数字孪生场景中，源域通常来自实验台或仿真环境，数据干净且有标签；但目标域是真实设备，噪声更强、工况更复杂，而且通常没有标签。因此这里要先让听众建立共识：这不是普通分类问题，而是一个典型的领域自适应问题。
-->

---
layout: default
---

<div class="kicker">Research Gap</div>

# 2. Pure data-driven alignment lacks physical consistency

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
      <td>Statistical discrepancy can be reduced by matching environmental noise rather than fault semantics.</td>
      <td>Mechanism features anchor the representation before adversarial alignment.</td>
    </tr>
    <tr>
      <td><strong>No mechanism check</strong></td>
      <td>Black-box feature spaces do not explicitly encode bearing kinematic laws or characteristic fault frequencies.</td>
      <td>Φ<sub>phy</sub> introduces rotor-dynamics priors as a frozen network layer.</td>
    </tr>
    <tr>
      <td><strong>Negative transfer</strong></td>
      <td>Under variable speed and noisy edge conditions, unconstrained alignment may hurt target diagnosis.</td>
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

# 3. Unsupervised domain adaptation for bearing faults

<div class="two-grid">
  <div class="paper-card">
    <h3>Training data</h3>
    <p><strong>Source:</strong> D<sub>s</sub> = {(x<sup>s</sup><sub>i</sub>, y<sup>s</sup><sub>i</sub>)} from Digital Twins / laboratory rigs.</p>
    <p class="mt-3"><strong>Target:</strong> D<sub>t</sub> = {x<sup>t</sup><sub>j</sub>} from physical assets, without labels.</p>
  </div>
  <div class="paper-card">
    <h3>Learning goal</h3>
    <p>Learn a robust mapping <strong>f: X → Y</strong> that minimizes target-domain generalization error.</p>
    <p class="mt-3">The representation must be both <em>fault-discriminative</em> and <em>domain-invariant</em>.</p>
  </div>
</div>

<div class="note mt-7">
  Existing pure data-driven DA methods may align statistical noise patterns instead of fault mechanisms, causing negative transfer under variable operating conditions.
</div>

<!--
English:
Here is the formal setting. We have labeled source samples and unlabeled target samples. During training, target labels are strictly hidden. The goal is to learn a representation that is both discriminative for fault classes and invariant across source and target domains.

中文：
这里给出任务形式化。源域样本有故障标签，目标域样本没有标签，训练过程中目标域标签严格不可见。目标是学习一个既能区分故障类别、又能跨源域和目标域保持一致的表示。
-->

---
layout: statement
---

# 4. Key Idea

<div class="big-statement">
Physics first, alignment second: use rotor-dynamics priors to anchor the representation, then use adversarial learning to close the residual domain gap.
</div>

<div class="three-grid mt-10">
  <div class="paper-card"><h3>Mechanism</h3><p>Faults manifest as energy around characteristic bearing frequencies.</p></div>
  <div class="paper-card"><h3>Data</h3><p>Real target data still contain noise and operational variation beyond the physics layer.</p></div>
  <div class="paper-card"><h3>Collaboration</h3><p>MDC-DAN combines fixed physical encoding with trainable domain adaptation.</p></div>
</div>

<!--
English:
The key idea is physics first and alignment second. Instead of sending raw signals directly into a black-box adaptation model, MDC-DAN first extracts a physics-aligned representation using rotor-dynamics priors. Then adversarial learning closes the remaining statistical gap.

中文：
这一页是方法的入口：先物理、后对齐。MDC-DAN 不是直接把原始信号交给黑箱 DA 模型，而是先利用转子动力学先验得到物理一致的表示，再用对抗学习缩小剩余的统计分布差异。
-->

---
layout: default
---

<div class="kicker">Contributions</div>

# 5. Three contributions

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
      <p>Mechanism-aligned features and DANN-style alignment jointly bridge the Sim-to-Real gap.</p>
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

# 6. Overall pipeline before details

<FrameworkDiagram />

<div class="note mt-6">
  First establish a physics-aligned representation, then learn domain-invariant fault features.
</div>

<!--
English:
I will reveal this diagram step by step. First, source and target signals enter the same pipeline. Then the frozen physics layer maps signals to mechanism features. Finally, the trainable module extracts latent features and branches into fault prediction and domain discrimination.

中文：
这一页我会分步讲。第一步只看源域和目标域输入；第二步展示固定的物理编码层，把信号映射到机制特征；第三步再展示可训练模块，包括故障分类器和领域判别器。这样可以避免听众一开始就被完整架构图淹没。
-->

---
layout: default
zoom: 0.9
---

<div class="kicker">Physics-Encoding Layer</div>

# 7. Frozen Physics-Encoding Layer

<div class="physics-badges">
  <div>non-learnable</div>
  <div>frozen forward path</div>
  <div>hard-wired rotor dynamics</div>
</div>

<PhysicsEncoding />

<div class="formula-grid compact-formulas mt-4">
  <FormulaCard title="Layer mapping" note="The layer is frozen and predetermined by rotor dynamics.">
    h<sub>phy</sub> = Φ<sub>phy</sub>(x) = [ψ<sub>stat</sub>(x) ⊕ ψ<sub>mech</sub>(x) ⊕ ψ<sub>freq</sub>(x)]<sup>T</sup>
  </FormulaCard>
  <FormulaCard title="BPFO example" note="N: rolling elements; fr: shaft frequency; d/D: rolling-element and pitch diameters; α: contact angle.">
    f<sub>BPFO</sub> = N/2 · f<sub>r</sub>(1 − d/D · cosα)
  </FormulaCard>
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

# 8. Domain-adversarial learning

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

<FormulaCard class="mt-3 compact-formula-card" title="Training objective" note="The paper uses a dynamic λp = 2/(1+exp(-10p))-1 to stabilize adversarial training.">
  E(θ<sub>f</sub>, θ<sub>y</sub>, θ<sub>d</sub>) = L<sub>y</sub> − λ<sub>p</sub>L<sub>d</sub>
</FormulaCard>

<!--
English:
This module follows the DANN logic. Gf learns latent fault features from hphy. Gy keeps the representation discriminative for source fault labels. Gd tries to distinguish source from target, while the gradient reversal layer makes Gf fool Gd. The dynamic λp schedule gradually strengthens the adversarial signal.

中文：
这一页重点讲 DANN 的对抗逻辑。Gf 从 hphy 中学习潜在故障特征，Gy 保证源域故障分类能力，Gd 判断特征来自源域还是目标域，而 GRL 反转梯度，使 Gf 学到能够欺骗 Gd 的域不变表示。动态 λp 则逐步增强对抗信号，避免训练初期过强对抗造成不稳定。
-->

---
layout: default
---

<div class="kicker">Experiments</div>

# 9. Cross-domain high-speed rail maintenance scenario

<table class="experiment-table mt-5">
  <thead>
    <tr>
      <th>Aspect</th>
      <th>Setting reported in the paper</th>
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
      <td>Uses target data without target labels during training.</td>
    </tr>
  </tbody>
</table>

<div class="note mt-7">
  Baselines are trained on source-domain data and directly evaluated on real target-domain data under a cross-domain setting.
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

# 10. MDC-DAN gains +28.14 pp over ResNet-18

<ResultBars />

<div class="metric-row mt-5">
  <div class="metric"><strong>93.94%</strong><span>MDC-DAN accuracy</span></div>
  <div class="metric"><strong>+28.14 pp</strong><span>vs. ResNet-18 accuracy</span></div>
  <div class="metric"><strong>0.942</strong><span>MDC-DAN F1-score</span></div>
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

# 11. Stable adversarial weight and lightweight inference

<div class="two-grid">
  <figure class="figure-frame">
    <img src="/figures/sensitivity.png" alt="Sensitivity analysis" />
    <figcaption class="caption">Figure: Sensitivity of adversarial trade-off parameter λ on target-domain accuracy.</figcaption>
  </figure>
  <div class="observation-list">
    <h3>Observations</h3>
    <ul class="small-list">
      <li>Optimal performance appears around <strong>λ = 0.5 to 0.7</strong>.</li>
      <li>Performance remains stable across <strong>[0.3, 0.8]</strong>.</li>
      <li>Too-small λ weakens alignment; too-large λ distracts from classification.</li>
      <li>The dynamic λ<sub>p</sub> schedule helps avoid unstable gradients at the early stage of adversarial training.</li>
      <li>Average inference time is <strong>4.2 ms per sample</strong>.</li>
      <li>Compared with heavy 2D-CNN image-conversion pipelines, MDC-DAN reduces computational cost by approximately <strong>60%</strong>.</li>
    </ul>
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
---

<div class="kicker">Interpretability</div>

# 12. t-SNE and SHAP verify physical consistency

<EvidencePair
  left="/figures/tsne.png"
  left-title="t-SNE: features align after MDC-DAN"
  right="/figures/shap.png"
  right-title="SHAP: BPFO/BPFI energy dominates"
/>

<div class="observation-list mt-4">
  <h3>Observation</h3>
  <p><strong>The model makes decisions for the right reason.</strong> After adaptation, source and target samples from the same fault class cluster together; SHAP assigns high importance to mechanism-related energy features, especially BPFO and BPFI.</p>
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

# 13. Conclusion

<div class="takeaway-layout">
  <div class="takeaway-block">
    <h2>Takeaway</h2>
    <p>MDC-DAN bridges the Sim-to-Real gap by combining a non-learnable physics encoding layer with adversarial domain adaptation, achieving accurate and interpretable target-domain fault diagnosis without target labels.</p>
  </div>
  <div class="future-block">
    <h2>Future Work</h2>
    <ul>
      <li>Blind source adaptation when bearing geometry is unknown.</li>
      <li>Diffusion-based generation of physically consistent nonstationary data.</li>
    </ul>
  </div>
</div>

## Thank you

<!--
English:
To conclude, MDC-DAN bridges the Sim-to-Real gap by combining a non-learnable physics encoding layer with adversarial domain adaptation. The result is accurate, lightweight, and interpretable target-domain fault diagnosis without target labels. Future work includes blind source adaptation for unknown bearing geometry and diffusion-based generation of physically consistent nonstationary data.

中文：
最后总结一下，MDC-DAN 通过非可学习的物理编码层和对抗式领域自适应相结合，缩小数字孪生故障诊断中的 Sim-to-Real gap，实现了无目标标签条件下准确、轻量且可解释的故障诊断。未来工作包括未知轴承几何条件下的 blind source adaptation，以及基于扩散模型生成物理一致的非平稳数据。谢谢大家，欢迎提问。
-->
