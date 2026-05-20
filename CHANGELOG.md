# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [v0.1.0] - 2026-05-19

### Added

- KEDA External Scaler gRPC server implementing `externalscaler.ExternalScalerServer`
- Direct NVML GPU metrics collection via `go-nvml` C-bindings
- 6 GPU metrics: utilization, memory utilization, memory used (MiB and %), temperature, power draw
- Pre-built scaling profiles: `vllm-inference`, `triton-inference`, `training`, `batch`
- Multi-GPU aggregation: `max`, `min`, `avg`, `sum`
- Scale-to-zero support via KEDA activation thresholds
- Per-GPU index targeting (`gpuIndex` parameter)
- Mock GPU collector for development and testing without hardware
- DaemonSet deployment manifests and Helm chart
- Unit tests for profiles, metric aggregation, and gRPC server
- E2E tests for full gRPC scaling path (no GPU required)
- CI pipeline: build, unit tests, e2e tests, lint, Helm lint, Docker build + push
- OpenSSF Best Practices badge

[v0.1.0]: https://github.com/pmady/keda-gpu-scaler/releases/tag/v0.1.0
