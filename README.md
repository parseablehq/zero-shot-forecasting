# Zero‑Shot Forecasting Artifacts

## Contents at a glance

- Forecast plots: `Forecast Plots/`
- CSV summaries: `CSV Files/`

## Series & Windows

- Prometheus memory: 10s, 5m, 10m windows
- OpenSearch CPU: 10s, 5m, 10m windows

## Forecast Horizons

- 64, 128, 256, 336 steps

## Baselines & Models

- Baselines: "t" (current value) and "t-1" (last value)
- Chronos: default quantiles 0.1–0.9 to produce fan charts
- Toto: varied sampling; (32, 4) highlighted as speed/quality sweet spot

## Metrics

- MASE: point-forecast accuracy versus naïve
- CRPS: calibrated uncertainty quality for predictive distributions

## Evaluation Protocol

- Rolling forecast origin
- Fixed final test window
- Latency recorded per horizon for each method

## Data & File Structure

- Series naming: `<metric>_<window>_<source>`
  - Examples: `mem_util_5m_prometheus`, `cpu_util_10s_opensearch`
- CSV files: `<prediction_length>_<data_used>.csv`
  - Example: `512_mem_util_5m_prometheus.csv`
- Plot folders: `<prediction_length>_<data_used>/` containing two plots per series
  - Files: one "chronos" plot and one "toto" plot
- Root paths in this repo:
  - Plots under `Forecast Plots/`
  - CSVs under `CSV Files/`

## CSV Header Dictionary

- Toto Time: Toto inference time for the horizon (ms or s, as exported)
- Chronos Time: Chronos inference time for the horizon
- Toto MASE: MASE for Toto’s point forecast vs naïve
- Chronos MASE: MASE for Chronos’s point forecast vs naïve
- Toto CRPS: CRPS for Toto’s predictive distribution
- Chronos CRPS: CRPS for Chronos’s predictive distribution
- Input Length: Context length used for inference

---

Notes

- Time units in exported CSVs may be milliseconds or seconds depending on source tool.
- Chronos fan charts are rendered from the 0.1–0.9 quantiles.
- Toto results reflect different sampling configs; (32, 4) is a good trade‑off.
