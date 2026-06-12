# Release v0.4.0 - June 8, 2026

## 🚀 Major Features

### HTTP Health Probes
- **Added** `/healthz` and `/readyz` endpoints for Kubernetes liveness/readiness probes
- **Configurable** via `--probe-port` flag (0 to disable)
- **Helm integration** with conditional probe configuration
- **Production ready** for Kubernetes deployments
- **Thanks to** [@ibobgunardi](https://github.com/ibobgunardi) for this excellent contribution!

### PCIe and NVLink Bandwidth Metrics
- **New advanced metrics** for GPU bandwidth monitoring and autoscaling
- **PCIe metrics**: `pcie_tx_kbps`, `pcie_rx_kbps` - CPU↔GPU data transfer throughput
- **NVLink metrics**: `nvlink_tx_mbps`, `nvlink_rx_mbps` - GPU↔GPU communication bandwidth
- **New profile**: `distributed-training` optimized for NVLink systems with sane defaults
- **Hardware-aware** - Graceful handling of non-NVLink hardware (metrics return 0)
- **Comprehensive docs** with practical examples and hardware-specific guidance
- **Thanks to** [@venkata22a](https://github.com/venkata22a) for this outstanding implementation!

## 📚 Documentation & Configuration

### Complete metricType Reference
- **Full table** of all 10 supported metric types with units and descriptions
- **Advanced metrics section** explaining PCIe vs NVLink use cases
- **Practical examples** with realistic bandwidth targets
- **Hardware guidance** for NVLink vs PCIe system optimization

### Prometheus Metrics Enhancement
- **New gauges**: PCIe/NVLink throughput with `direction` labels
- **Device count** metric for cluster monitoring
- **Complete coverage** of all GPU telemetry

## 🔧 Infrastructure & Quality

### Testing & Reliability
- **100% test coverage** for new features
- **Dedicated test functions** for PCIe/NVLink extraction
- **Distributed training profile** validation
- **All tests pass** ✅ | **Lint clean** ✅

### Community Contributions
This release features significant contributions from two community members:
- **Bobi Gunardi** (CodeLabs Indonesia) - Health probes implementation
- **Venkata Edara** - PCIe/NVLink metrics with comprehensive documentation

## ⚠️ Important Notes

### Hardware Compatibility
- **NVLink metrics** return 0 on hardware without NVLink (T4, A10, etc.) - this is normal behavior
- **PCIe metrics** work on all GPU systems and are recommended for non-NVLink hardware
- **Automatic detection** - scaler adapts to available hardware capabilities

### Configuration Changes
- **Health probes** are disabled by default (set `--probe-port=8081` to enable)
- **New metric types** expand scaling possibilities for enterprise workloads
- **Backward compatible** - all existing configurations continue to work

## 🎯 Use Cases Enabled

### Data-Parallel Training
- **NVLink bandwidth monitoring** for distributed training workloads
- **Communication bottleneck detection** when GPU utilization appears low
- **Automatic scaling** based on inter-GPU communication saturation

### Enterprise GPU Monitoring
- **PCIe bandwidth tracking** for CPU↔GPU data transfer bottlenecks
- **Hardware utilization insights** beyond basic GPU utilization
- **Cost optimization** through precise autoscaling decisions

## 📦 Installation

```bash
# Helm install with health probes enabled
helm install keda-gpu-scaler ./deploy/helm/keda-gpu-scaler \
  --set probes.enabled=true \
  --set probes.port=8081

# Example distributed training ScaledObject
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: distributed-training
spec:
  scaleTargetRef:
    name: training-app
  triggers:
  - type: external
    metadata:
      scalerAddress: "keda-gpu-scaler.keda.svc.cluster.local:6000"
      profile: "distributed-training"
      targetValue: "800"
      activationThreshold: "100"
```

## 🏛️ Industry Recognition & Standards

### CNCF TAG Infrastructure — AI Technical Community Group
This project is actively contributing to the **CNCF TAG Infrastructure — AI Technical Community Group** to advance GPU-aware autoscaling capabilities in the cloud native ecosystem.

**Community Engagement:**
- **CNCF TOC Submission**: [GPU-Aware Autoscaling in Cloud Native AI Infrastructure](https://github.com/cncf/toc/issues/2188)
- **Whitepaper in Progress**: "GPU-Aware Autoscaling in Cloud Native AI Infrastructure" - Technical deep-dive addressing GPU scaling blind spots in Kubernetes
- **TAG Infrastructure AI TCG**: Active participant in shaping AI/ML workload orchestration standards


**Industry Impact:**
- Addressing critical GPU telemetry gaps in Kubernetes
- Building production-ready solutions for enterprise AI workloads
- Contributing to cloud native GPU scheduling standards
- Establishing GPU autoscaling as a first-class HPC concern

## 🙏 Acknowledgments

Special thanks to our community contributors for making this release possible:
- **[@ibobgunardi](https://github.com/ibobgunardi)** - Health probes implementation with comprehensive test coverage
- **[@venkata22a](https://github.com/venkata22a)** - Advanced GPU metrics with exceptional documentation

## 📊 Stats

- **Files changed**: 10
- **Lines added**: 310+
- **Test coverage**: 100% for new features
- **Contributors**: 2 community members
- **New metrics**: 4 advanced bandwidth metrics
- **New profiles**: 1 (distributed-training)

---

**Previous release**: [v0.3.0](https://github.com/pmady/keda-gpu-scaler/releases/tag/v0.3.0)  
**Full changelog**: [CHANGELOG.md](https://github.com/pmady/keda-gpu-scaler/blob/main/CHANGELOG.md)
