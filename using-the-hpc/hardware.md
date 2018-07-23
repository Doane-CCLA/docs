[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [SHPC Condo User Guide](overview.md) → [Hardware Configuration](hardware.md)

# SHPC Condo Hardware Configuration

The SHPC is a commodity cluster that contains a set of [MPPs (Massive Parallel Processors)](https://en.wikipedia.org/wiki/Massively_parallel).

A processor in this cluster is commonly referred to as a node and has its own CPU, memory, and I/O subsystem and is capable of communicating with other nodes.

## Node Information

- **Make**: Cray
- **Model**: CS400

## RAM Information

- **Speed**: DDR4 2133
- **Error correction**: Registered ECC
- **Capacity**: 128–256 GB per node (GPU nodes and high memory nodes have 256 GB of RAM)

## CPU Information

- **Make**: Intel
- **Model**: Xeon E5-2698 v3
- **Speed**: 2.30 GHz base clock, 3.60 GHz Turbo Boost clock
- **Capacity**: 2 CPUs per node
- **CPU layout**: [Click to see image.](screenshots/cpu-layout.png)

## GPU Information

- **Make**: NVIDIA
- **Model**: Tesla K80 (2 GK210 GPUs on each K80)
- **Speed**: 560 MHz base clock
- **VRAM**: 24 GB of GDDR5
- **Error correction**: Registered ECC
- **Capacity**: 2 Tesla K80s per node, 2 GK210 GPUs per K80 (4 total GK210 GPUs per node)

## Network

- InfiniBand Interconnects
