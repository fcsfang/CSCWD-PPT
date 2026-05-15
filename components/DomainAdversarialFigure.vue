<template>
  <div class="domain-module-block">
    <div class="domain-module-layout">
      <figure class="domain-module-figure">
        <img src="/figures/Module.png" alt="Trainable Domain-Adversarial Module" />
        <figcaption class="caption">Figure: Trainable Domain-Adversarial Module.</figcaption>
      </figure>

      <div class="domain-module-explain">
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

        <div class="formula-label">Training objective</div>
        <div class="objective-equation" aria-label="Training objective equation">
          <span class="math-calligraphic">E</span>(θ<sub>f</sub>, θ<sub>y</sub>, θ<sub>d</sub>)
          =
          <span class="math-calligraphic">L</span><sub>y</sub>(θ<sub>f</sub>, θ<sub>y</sub>)
          − λ<sub>p</sub><span class="math-calligraphic">L</span><sub>d</sub>(θ<sub>f</sub>, θ<sub>d</sub>)
        </div>

        <div class="caption">A dynamic λ<sub>p</sub> schedule gradually strengthens adversarial adaptation.</div>
      </div>
    </div>

    <div class="dann-summary">
      MDC-DAN aligns mechanism-aware features h<sub>phy</sub>, rather than raw statistical patterns.
    </div>
  </div>
</template>
