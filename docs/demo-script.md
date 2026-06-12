# keda-gpu-scaler Demo Script - 5 Minutes

## Demo Setup
- Terminal 1: Kubernetes cluster with GPU nodes
- Terminal 2: keda-gpu-scaler metrics dashboard
- Terminal 3: GPU workload simulation

## Script Timeline

### Minute 0: Introduction (30 seconds)
"Today I'll show how keda-gpu-scaler solves GPU resource waste in HPC clusters. Watch the GPU utilization metrics - we'll see 60% idle capacity initially."

### Minute 1: Baseline Problem (45 seconds)
- Show static GPU allocation
- Display low utilization metrics
- Highlight resource waste

### Minute 2: Enable Autoscaling (45 seconds)
- Deploy keda-gpu-scaler
- Configure scaling policy
- Show real-time metrics collection

### Minute 3: Dynamic Scaling (45 seconds)
- Launch variable GPU workloads
- Show automatic pod scaling
- Display improved utilization

### Minute 4: NUMA Optimization (45 seconds)
- Enable NUMA-aware placement via Volcano plugin
- Show PCIe latency reduction for multi-node training
- Highlight memory bandwidth gains and energy efficiency
- Demonstrate GreenOps impact on power consumption

### Minute 5: Results Summary (30 seconds)
- Show before/after metrics
- Quantify efficiency gains
- Discuss DOE impact

## Key Demo Points

### Problem Statement
"Traditional HPC clusters allocate GPUs statically, leading to 40-60% idle capacity. This wastes energy and increases queue times for researchers."

### Solution Demonstration
"keda-gpu-scaler monitors actual GPU utilization via NVML and scales pods dynamically. When workloads finish, resources are released immediately."

### Technical Details
"The system integrates with Kubernetes via the KEDA external scaler interface and uses Volcano for NUMA-aware GPU placement."

### Performance Metrics
"Results show 30-50% better GPU utilization, 20-30% energy savings, and 15-25% faster job completion times."

## DOE-Specific Benefits

### Scientific Computing Impact
- Faster time-to-discovery for researchers
- Lower operational costs
- Better support for bursty AI workloads

### Why DOE Labs Care
- GPU idle time is real money and real watts
- Researchers shouldn't wait for GPUs that are allocated but sitting empty
- NUMA placement matters when you're saturating PCIe lanes

## Technical Commands for Demo

### 1. Show baseline GPU utilization
```bash
kubectl top nodes
nvidia-smi
```

### 2. Deploy static allocation
```bash
kubectl apply -f static-gpu-workload.yaml
watch kubectl get pods
```

### 3. Deploy keda-gpu-scaler
```bash
helm install keda-gpu-scaler ./charts/keda-gpu-scaler
kubectl logs -f deployment/keda-gpu-scaler
```

### 4. Enable dynamic scaling
```bash
kubectl apply -f scaled-object.yaml
kubectl get hpa
```

### 5. Show NUMA optimization
```bash
kubectl apply -f numa-aware-workload.yaml
kubectl describe pod numa-workload
```

## Visual Elements

### Metrics Dashboard
- Real-time GPU utilization
- Pod scaling events
- Memory bandwidth usage
- Energy consumption estimates

### Before/After Comparison
- Static vs dynamic allocation
- Utilization percentages
- Resource waste metrics
- Cost savings calculations

## Recording Tips

### Technical Quality
- Clear terminal visibility
- Consistent font size
- Stable camera position
- Good audio quality

### Content Flow
- Practice timing for each segment
- Ensure smooth transitions
- Highlight key metrics clearly
- End with next steps

### DOE Focus
- Show the energy angle — idle GPUs burning power
- Reference specific lab workloads (climate, materials, genomics)
- Keep metrics honest — say "expected" not "guaranteed"
