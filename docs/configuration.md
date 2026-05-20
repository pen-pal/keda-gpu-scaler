# Configuration

Everything goes in the ScaledObject trigger `metadata`. No config files or extra CRDs needed.

## Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `profile` | Pre-built scaling profile name | (none) |
| `metricType` | GPU metric to scale on | `gpu_utilization` |
| `targetValue` | Target metric value for scaling | `80` |
| `targetGpuUtilization` | Shorthand for GPU utilization target | (none) |
| `targetMemoryUtilization` | Shorthand for VRAM utilization target | (none) |
| `activationThreshold` | Value below which scale-to-zero activates | `0` |
| `gpuIndex` | Specific GPU index to monitor | `-1` (all GPUs) |
| `aggregation` | Multi-GPU aggregation: `max`, `min`, `avg`, `sum` | `max` |
| `pollIntervalSeconds` | Metric polling interval | `10` |

## Scaling Profiles

Profiles bundle defaults for common workloads. Override any parameter in the trigger metadata.

| Profile | Primary Metric | Target | Activation | Use Case |
|---------|---------------|--------|------------|----------|
| `vllm-inference` | Memory % | 80 | 5 | vLLM / LLM serving with scale-to-zero |
| `triton-inference` | GPU Util | 75 | 10 | NVIDIA Triton Inference Server |
| `training` | GPU Util | 90 | 0 | Training jobs (no scale-to-zero) |
| `batch` | Memory % | 70 | 1 | Batch inference with aggressive scale-down |

### Using a profile

```yaml
triggers:
  - type: external
    metadata:
      scalerAddress: "keda-gpu-scaler.keda.svc.cluster.local:6000"
      profile: "vllm-inference"
```

### Overriding a profile parameter

```yaml
triggers:
  - type: external
    metadata:
      scalerAddress: "keda-gpu-scaler.keda.svc.cluster.local:6000"
      profile: "vllm-inference"
      targetValue: "90"          # override the default 80
```

### Using raw metrics (no profile)

```yaml
triggers:
  - type: external
    metadata:
      scalerAddress: "keda-gpu-scaler.keda.svc.cluster.local:6000"
      metricType: "gpu_utilization"
      targetValue: "85"
      activationThreshold: "10"
      gpuIndex: "0"
      aggregation: "max"
```

## Multi-GPU Aggregation

On multi-GPU nodes, `aggregation` controls how per-GPU values are reduced to one number:

- **max** (default) — scale when any GPU hits the threshold. Good for inference where one hot GPU means overload.
- **avg** — scale on average utilization. Good for training where GPUs should be evenly loaded.
- **min** — scale when the least-loaded GPU hits the threshold. Conservative.
- **sum** — total utilization. Useful for capacity-based decisions.

## Scale-to-Zero

Set `activationThreshold` to enable scale-to-zero. When all GPU metrics drop below this value, KEDA reports the scaler as inactive and scales the deployment to zero replicas.

```yaml
triggers:
  - type: external
    metadata:
      scalerAddress: "keda-gpu-scaler.keda.svc.cluster.local:6000"
      metricType: "gpu_utilization"
      targetValue: "80"
      activationThreshold: "5"    # scale to zero when GPU util < 5%
```

## Examples

Check `deploy/examples/` for ScaledObject manifests:

- `vllm-scaledobject.yaml` — vLLM inference with scale-to-zero
- `custom-gpu-utilization.yaml` — raw GPU utilization scaling
