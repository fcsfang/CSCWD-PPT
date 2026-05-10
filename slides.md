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
开场：大家好，我汇报的论文是 MDC-DAN。它关注数字孪生故障诊断中的 Sim-to-Real gap：实验室或数字空间中的高保真数据，与真实列车运行环境中的无标签数据存在明显分布偏移。我们的核心思路是把轴承故障机理作为固定网络层引入，再用领域对抗学习做迁移。
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
这一页只讲问题：数字孪生让我们有源域知识，但源域和真实目标域并不一致。源域是实验台或标准数据，标签充分；目标域是真实高速列车，噪声更强、环境更复杂、标签不可用。这里先让听众接受：这是一个迁移问题，而不是单纯分类问题。
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
这一页回答为什么已有 DA 还不够。重点不是否定 DANN，而是指出纯数据驱动对齐缺少物理一致性约束，可能把噪声也当成可迁移信息。
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
这里把任务形式化。源域有标签，目标域无标签。训练中目标标签严格隐藏，目标是让模型能在目标域上诊断。强调本文不是监督迁移，也不是直接在目标域训练。
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
这一页是方法入口。不要急着展示完整公式，而是先给听众一句话：先用机理约束输入表示，再用对抗学习完成统计对齐。这个顺序是本文区别于纯黑箱 DA 的关键。
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
    </div>
  </div>
  <div class="contribution-row">
    <div class="contribution-index">C2</div>
    <div>
      <h3>Collaborative adversarial adaptation</h3>
      <p>Mechanism-aligned features and DANN-style alignment jointly bridge the Sim-to-Real gap.</p>
    </div>
  </div>
  <div class="contribution-row">
    <div class="contribution-index">C3</div>
    <div>
      <h3>Trustworthy interpretability</h3>
      <p>t-SNE and SHAP verify that the learned decision evidence is physically meaningful.</p>
    </div>
  </div>
</div>

<!--
这一页对应论文引言里的三点贡献。汇报时用每张卡片一句话讲清楚，后续方法和实验会逐一展开这些贡献。
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
这页只讲简化总览，不展示论文原图的全部细节。先让听众记住两阶段流程：Physics-Encoding Layer 负责物理锚定，Domain-Adversarial Module 负责对齐和诊断。后续两页再展开。
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
  <FormulaCard title="BPFO example" note="The paper uses bearing kinematic equations to locate characteristic frequencies.">
    f<sub>BPFO</sub> = N/2 · f<sub>r</sub>(1 − d/D · cosα)
  </FormulaCard>
</div>

<!--
这一页解释 Physics-Encoding Layer。重点不是“做了特征工程”，而是它作为网络输入层是 frozen、non-learnable 的，把 rotor dynamics 作为硬约束嵌入前向计算。机制神经元通过包络谱中特征频率附近的能量比来表达故障机理。
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
这里少讲公式，多讲对抗博弈逻辑。Gf 学故障特征，Gd 判断域标签，GRL 让 Gf 反过来欺骗 Gd。最后只保留总目标公式，说明动态 λp 用于稳定训练。
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
这页讲实验设置。注意所有数字都来自论文：CWRU 12880，有标签；目标域 1274，无标签；600 rpm；窗口 2048；50% overlap；Adam 1e-3；batch size 64；50 epochs。
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
汇报时不要逐行读表。先说 MDC-DAN 93.94%，再说相对 ResNet-18 提升 28.14 个百分点。结论是：简单加深网络不能解决 Sim-to-Real gap，机理锚点和领域对齐的组合才是关键。
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
      <li>Average inference time is <strong>4.2 ms per sample</strong>.</li>
      <li>Compared with heavy 2D-CNN image-conversion pipelines, MDC-DAN reduces computational cost by approximately <strong>60%</strong>.</li>
    </ul>
  </div>
</div>

<!--
这一页补充工程部署价值。第一，λ 不需要非常精细地调，0.3 到 0.8 都比较稳定。第二，推理速度 4.2ms，适合边缘设备或高速列车场景。
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
这一页讲可信性。t-SNE 说明分布确实被对齐；SHAP 说明模型不是靠背景噪声或偶然统计特征，而是更多依赖 BPFO、BPFI 等机理特征。这是本文面向工业部署的重要卖点。
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
总结三点贡献：机理层、对抗迁移、可信解释。未来工作严格按照论文写：未知轴承几何下的 blind source adaptation，以及结合 Diffusion models 生成物理一致的非平稳数据。最后进入提问。
-->
