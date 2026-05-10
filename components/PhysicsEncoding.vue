<template>
  <div class="physics">
    <table class="feature-table">
      <thead>
        <tr>
          <th>Feature group</th>
          <th>Indices</th>
          <th>Feature definitions</th>
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
  </div>
</template>

<style scoped>
.physics {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--card);
  padding: 14px;
}
.feature-table {
  width: 100%;
  border-collapse: collapse;
  font-size: .82rem;
}
th,
td {
  border: 1px solid var(--border);
  padding: 9px 10px;
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
  line-height: 1.32;
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
</style>
