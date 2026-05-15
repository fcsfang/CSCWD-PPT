<template>
  <div class="physics-encoding-block">
    <figure class="physics-module-figure">
      <img src="/figures/mechanism-module.png" alt="Physics-Encoding Layer mechanism module" />
      <figcaption class="caption">Figure: Physics-Encoding Layer maps vibration signals to mechanism-aware features.</figcaption>
    </figure>

    <div class="physics-detail-panel">
      <table class="physics-feature-table">
        <thead>
          <tr>
            <th>Feature group</th>
            <th>Indices</th>
            <th>Feature definitions</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Time statistics</td>
            <td>f<sub>1</sub>-f<sub>6</sub></td>
            <td>RMS, Kurtosis, Skewness, Peak-Peak, Shape Factor, Impulse Factor</td>
          </tr>
          <tr class="mechanism">
            <td>Mechanism energy</td>
            <td>f<sub>7</sub>-f<sub>12</sub></td>
            <td>Energy ratios around BPFO, BPFI, BSF, FTF and 2nd harmonics</td>
          </tr>
          <tr>
            <td>Frequency statistics</td>
            <td>f<sub>13</sub>-f<sub>15</sub></td>
            <td>Spectral Centroid, Spectral RMS, Spectral Variance</td>
          </tr>
        </tbody>
      </table>

      <div class="physics-formula-panel">
        <div class="formula-label">Layer mapping</div>
        <div class="physics-equation">
          h<sub>phy</sub> = Φ<sub>phy</sub>(x)
          = [ψ<sub>stat</sub>(x) ⊕ ψ<sub>mech</sub>(x) ⊕ ψ<sub>freq</sub>(x)]<sup>T</sup>
        </div>
      </div>

      <div class="physics-formula-panel">
        <div class="formula-label">BPFO example</div>
        <div class="physics-equation">
          f<sub>BPFO</sub> = <span class="frac"><span>N</span><span>2</span></span> f<sub>r</sub>
          (1 − <span class="frac"><span>d</span><span>D</span></span> cos α)
        </div>
        <div class="caption">N: rolling elements; f<sub>r</sub>: shaft frequency; d/D: rolling-element and pitch diameters; α: contact angle.</div>
      </div>

      <div class="key-point">
        Key point: frozen Φ<sub>phy</sub> is determined by rotor dynamics, not learned from data.
      </div>
    </div>
  </div>
</template>
