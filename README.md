# Slurm Feature Constraints
## How to request Node features by using Slurm constraints

As defined in the [SLURM](https://slurm.schedmd.com/archive/slurm-18.08.5/sbatch.html#OPT_constraint) documentation, when a job requires specific hardware features on a compute node, a user may specfiy feature contstraints in their `sbatch` file using the `-C or --contraint` options

```bash
#SBATCH --constraint=<feature list>
```

### Requesting multiple features/constraints

Seperating multiple feature using the logical `AND` and `OR` operators allows the user to specify multiple feature constraints for their job.

Logical Operator | Operator Symbol | Example
:--------------: | :-------------: | -------
AND              | &               | #SBATCH --constraint="cpu_xeon&AVX2"
OR               | \|              | #SBATCH --constraint="opteron_8435\|epyc_7352"

If required, more sopisicated logical constraints may be created using parenthesis and brackets to create grouping of features where parenthesis are used with the `AND` operator and brackets are use with the `OR` operator.

### Example requesting a Xeon node with an M10 GPU
```bash
#!/bin/bash
#SBATCH --job-name=MY_JOB
#SBATCH -n 1
#SBATCH -N 1
#SBATCH -c 1
#SBATCH --mem=1G
#SBATCH --partition=general
#SBATCH --qos=general
#SBATCH --constraint="cpu_xeon&gpu_M10"
#SBATCH --mail-type=ALL
#SBATCH --mail-user=YOUR.EMAIL@uconn.edu
#SBATCH -o %x_%A_%a.out
#SBATCH -e %x_%A_%a.err


echo "host name : " `hostname`
nvidia-smi

```

### Feature List

The following features are currently defined in the Xanadu cluster:

Feature        | Description
-------------- | --------------
cpu_amd        | Nodes with AMD CPUs
opteron_6172   | Nodes with AMD Opteron 6172 CPUs
opteron_6274   | Nodes with AMD Opteron 6274 CPUs
opteron_8435   | Nodes with AMD Opteron 8435 CPUs
epyc_7352      | Nodes with AMD Eypc 7352 CPUs
cpu_xeon       | Nodes with Intel Xeon CPUs
xeon_E52660    | Nodes with Intel Xeon E52660 CPUs
xeon_E52697    | Nodes with Intel Xeon E52697 CPUs
xeon_gold_6230 | Nodes with Intel Xeon Gold 6230 CPUs
gpu_M10        | Nodes with NVIDIA M10 GPUs
gpu_T4         | Nodes with NVIDIA T4 GPUs
gpu_cc_5.2     | Nodes with CUDA Compute Capability of 5.2
gpu_cc_7.5     | Nodes with CUDA Compute Capability of 7.5
AVX            | Nodes with AVX CPU instruction set
AVX2           | Nodes with AVX2 CPU instruction set
AVX512         | Nodes with AVX512 CPU instruction set
SSE            | Nodes with SSE CPU instruction set
SSE2           | Nodes with SSE2 CPU instruction set
SSE3           | Nodes with SSE3 CPU instruction set
SSE4           | Nodes with SSE4 CPU instruction set
SSE41          | Nodes with SSE41 CPU instruction set
SSE42          | Nodes with SSE42 CPU instruction set
SSE4A          | Nodes with SSE4A CPU instruction set
SSSE3          | Nodes with SSSE3 CPU instruction set
