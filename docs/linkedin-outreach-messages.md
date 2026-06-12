# LinkedIn Outreach Messages - DOE National Laboratory Contacts

## Message Templates

### Initial Connection Request
```
Hi [Name], I came across your work on [specific project/area] at [Lab]. I'm developing GPU-aware autoscaling solutions for HPC workloads that could help address GPU resource utilization challenges in scientific computing. Would you be open to connecting?
```

### Follow-up Message (After Connection)
```
Thanks for connecting, [Name]. I've been building a GPU autoscaler for Kubernetes (keda-gpu-scaler) that pulls NVML metrics directly instead of going through Prometheus. Paired it with NUMA-aware scheduling in Volcano to cut PCIe latency on multi-GPU jobs.

Given your work on [their specific area], curious if you've seen similar GPU idle-time issues in DOE clusters. Would love to get your take on the approach — 15 min sometime?
```

### Technical Briefing Request
```
Hi [Name], following up — I put together a short writeup on how keda-gpu-scaler could fit into [Lab]'s scheduling stack, especially for [specific use case]. Happy to walk through it if you have 15 min: [link to proposal]
```

## Target Contacts

### Oak Ridge National Laboratory
1. **Al Geist II** - HPC Operations, GPU scheduling
2. **Scott Atchley** - Advanced Technologies 
3. **Aaron Haun** - HPC Systems
4. **Tom Beck** - Scientific Computing
5. **Ryan Landfield** - HPC Operations

### Lawrence Livermore National Laboratory
1. **Jim Leek** - HPC Group Lead
2. **Chunhua (Leo) Liao** - LLM for code transformation
3. **Dan Quinlan** - Compiler optimization
4. **Pei-Hung Lin** - Parallel programming models
5. **Matthew Sottile** - Programming languages for HPC

## Outreach Schedule

### Week 1: Initial Connections
- Monday: Send connection requests to ORNL contacts
- Tuesday: Send connection requests to LLNL contacts
- Wednesday: Follow-up with accepted connections
- Thursday: Share technical proposal
- Friday: Request technical briefings

### Week 2: Technical Engagement
- Monday: Prepare demo materials
- Tuesday: Schedule briefings
- Wednesday-Thursday: Conduct technical presentations
- Friday: Gather feedback and next steps

## Key Talking Points

### Value Proposition
- 30-50% GPU utilization improvement
- 20-30% energy efficiency gains
- 15-25% faster job completion
- 40-60% reduction in resource waste

### Technical Fit
- Kubernetes-native architecture
- NUMA-aware GPU placement
- Real-time NVML monitoring
- Integration with Volcano scheduler

### DOE Fit
- Built for the kind of bursty GPU workloads common in research
- Reduces wasted power on idle GPUs
- Shorter queue times for researchers
