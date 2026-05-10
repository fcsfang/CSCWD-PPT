<template>
  <div class="physics">
    <div class="flow">
      <div class="flow-item">Raw vibration window x</div>
      <div class="flow-edge"></div>
      <div class="flow-item">Envelope spectrum S<sub>x</sub>(f)</div>
      <div class="flow-edge"></div>
      <div class="flow-item accent">h<sub>phy</sub> = Φ<sub>phy</sub>(x)</div>
    </div>

    <table class="feature-table">
      <thead>
        <tr>
          <th>Feature group</th>
          <th>Indices</th>
          <th>Definitions used in the paper</th>
          <th>Role in diagnosis</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Time statistics</td>
          <td>f<sub>1</sub>-f<sub>6</sub></td>
          <td>RMS, Kurtosis, Skewness, Peak-Peak, Shape Factor, Impulse Factor</td>
          <td>General vibration severity and impulsiveness</td>
        </tr>
        <tr class="mechanism">
          <td>Mechanism energy</td>
          <td>f<sub>7</sub>-f<sub>12</sub></td>
          <td>Energy ratios around BPFO, BPFI, BSF, FTF and 2nd harmonics</td>
          <td>Bearing kinematic fault signatures</td>
        </tr>
        <tr>
          <td>Frequency statistics</td>
          <td>f<sub>13</sub>-f<sub>15</sub></td>
          <td>Spectral Centroid, Spectral RMS, Spectral Variance</td>
          <td>Frequency-distribution shape</td>
        </tr>
      </tbody>
    </table>

    <div class="constraint">
      Φ<sub>phy</sub> is frozen / non-learnable / determined by rotor dynamics.
    </div>
  </div>
</template>

<style scoped>
.physics {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--card);
  padding: 14px;
}
.flow {
  display: grid;
  grid-template-columns: 1fr 44px 1fr 44px 1fr;
  align-items: center;
  margin-bottom: 12px;
}
.flow-item {
  border: 1px solid var(--border);
  border-radius: 4px;
  min-height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text);
  font-size: .84rem;
  font-weight: 620;
  text-align: center;
}
.flow-item.accent {
  border-top: 2px solid var(--accent);
  color: var(--accent);
}
.flow-edge {
  height: 1px;
  background: var(--border);
  position: relative;
}
.flow-edge::after {
  content: "";
  position: absolute;
  right: 0;
  top: -4px;
  border-left: 7px solid var(--border);
  border-top: 4px solid transparent;
  border-bottom: 4px solid transparent;
}
.feature-table {
  width: 100%;
  border-collapse: collapse;
  font-size: .72rem;
}
th,
td {
  border: 1px solid var(--border);
  padding: 8px 9px;
  text-align: left;
  vertical-align: top;
}
th {
  background: #F2F4F7;
  color: var(--text);
  font-weight: 650;
}
td {
  color: var(--muted);
  line-height: 1.28;
}
td:first-child,
td:nth-child(2) {
  color: var(--text);
  font-weight: 620;
}
.mechanism td {
  background: #FFFDFD;
}
.mechanism td:first-child,
.mechanism td:nth-child(2) {
  color: var(--accent);
}
.constraint {
  margin-top: 10px;
  border-left: 3px solid var(--accent);
  padding-left: 10px;
  color: var(--accent);
  font-size: .78rem;
  font-weight: 650;
}
</style>
