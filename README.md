# Ethereum CUDA Miner


### Docker container for Ethereum mining with CUDA.

Simple and easy to run, if you have a Nvidia GPU and want to mine eth.

**Note** This image builds the Genoil ethminer, which is faster than the standard opencl ethminer. [https://github.com/Genoil/cpp-ethereum](https://github.com/Genoil/cpp-ethereum)

### Requirements
- Nvidia drivers for your GPU, you can get them here: [Nvidia drivers](http://www.nvidia.com/Download/index.aspx)
- nvidia-docker (so docker can access your GPU) install instructions here: [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)

### How to run
```
nvidia-docker run -it anthonytatowicz/eth-cuda-miner ARG1 ARG2 ...

# Example
nvidia-docker run -it anthonytatowicz/eth-cuda-miner \
-S us-west1.nanopool.org:9999 \
-O 0x20ad58fe023265577565c7eb44b55c31e7497c33.cSquared/ajtatowicz@gmail.com
```

**Note** --farm-recheck and -U are set by default
**Note** Be sure to change the -O argument to your mining address and email. The format goes like this "address.worker/email"

### Help
```
Genoil's ethminer 0.9.41-genoil-1.1.7
=====================================================================
Forked from github.com/ethereum/cpp-ethereum
CUDA kernel ported from Tim Hughes' OpenCL kernel
With contributions from nicehash, nerdralph, RoBiK and sp_ 

Please consider a donation to:
ETH: 0xeb9310b185455f863f526dab3d245809f6854b4d

Usage ethminer [OPTIONS]
Options:

Work farming mode:
    -F,--farm <url>  Put into mining farm mode with the work server at URL (default: http://127.0.0.1:8545)
    -FF,-FO, --farm-failover, --stratum-failover <url> Failover getwork/stratum URL (default: disabled)
	--farm-retries <n> Number of retries until switch to failover (default: 3)
	-S, --stratum <host:port>  Put into stratum mode with the stratum server at host:port
	-FS, --failover-stratum <host:port>  Failover stratum server at host:port
    -O, --userpass <username.workername:password> Stratum login credentials
    -FO, --failover-userpass <username.workername:password> Failover stratum login credentials (optional, will use normal credentials when omitted)
    --work-timeout <n> reconnect/failover after n seconds of working on the same (stratum) job. Defaults to 180. Don't set lower than max. avg. block time
    -SC, --stratum-client <n>  Stratum client version. Defaults to 1 (async client). Use 2 to use the new synchronous client.
    -SP, --stratum-protocol <n> Choose which stratum protocol to use:
        0: official stratum spec: ethpool, ethermine, coinotron, mph, nanopool (default)
        1: eth-proxy compatible: dwarfpool, f2pool, nanopool
        2: EthereumStratum/1.0.0: nicehash
    -SE, --stratum-email <s> Email address used in eth-proxy (optional)
    --farm-recheck <n>  Leave n ms between checks for changed work (default: 500). When using stratum, use a high value (i.e. 2000) to get more stable hashrate output

Benchmarking mode:
    -M [<n>],--benchmark [<n>] Benchmark for mining and exit; Optionally specify block number to benchmark against specific DAG.
    --benchmark-warmup <seconds>  Set the duration of warmup for the benchmark tests (default: 3).
    --benchmark-trial <seconds>  Set the duration for each trial for the benchmark tests (default: 3).
    --benchmark-trials <n>  Set the duration of warmup for the benchmark tests (default: 5).
Simulation mode:
    -Z [<n>],--simulation [<n>] Mining test mode. Used to validate kernel optimizations. Optionally specify block number.
Mining configuration:
    -G,--opencl  When mining use the GPU via OpenCL.
    -U,--cuda  When mining use the GPU via CUDA.
    -X,--cuda-opencl Use OpenCL + CUDA in a system with mixed AMD/Nvidia cards. May require setting --opencl-platform 1
    --opencl-platform <n>  When mining using -G/--opencl use OpenCL platform n (default: 0).
    --opencl-device <n>  When mining using -G/--opencl use OpenCL device n (default: 0).
    --opencl-devices <0 1 ..n> Select which OpenCL devices to mine on. Default is to use all
    -t, --mining-threads <n> Limit number of CPU/GPU miners to n (default: use everything available on selected platform)
    --allow-opencl-cpu Allows CPU to be considered as an OpenCL device if the OpenCL platform supports it.
    --list-devices List the detected OpenCL/CUDA devices and exit. Should be combined with -G or -U flag
    -L, --dag-load-mode <mode> DAG generation mode.
        parallel    - load DAG on all GPUs at the same time (default)
        sequential  - load DAG on GPUs one after another. Use this when the miner crashes during DAG generation
        single <n>  - generate DAG on device n, then copy to other devices
    --cl-extragpu-mem Set the memory (in MB) you believe your GPU requires for stuff other than mining. default: 0
    --cl-local-work Set the OpenCL local work size. Default is 64
    --cl-global-work Set the OpenCL global work size as a multiple of the local work size. Default is 4096 * 64
    --cuda-extragpu-mem Set the memory (in MB) you believe your GPU requires for stuff other than mining. Windows rendering e.t.c..
    --cuda-block-size Set the CUDA block work size. Default is 128
    --cuda-grid-size Set the CUDA grid size. Default is 8192
    --cuda-streams Set the number of CUDA streams. Default is 2
    --cuda-schedule <mode> Set the schedule mode for CUDA threads waiting for CUDA devices to finish work. Default is 'sync'. Possible values are:
        auto  - Uses a heuristic based on the number of active CUDA contexts in the process C and the number of logical processors in the system P. If C > P, then yield else spin.
        spin  - Instruct CUDA to actively spin when waiting for results from the device.
        yield - Instruct CUDA to yield its thread when waiting for results from the device.
        sync  - Instruct CUDA to block the CPU thread on a synchronization primitive when waiting for the results from the device.
    --cuda-devices <0 1 ..n> Select which CUDA GPUs to mine on. Default is to use all
General Options:
    -v,--verbosity <0 - 9>  Set the log verbosity from 0 to 9 (default: 8).
    -V,--version  Show the version and exit.
    -h,--help  Show this help message and exit.
```

### Questions?
You can leave a comment below or email to `ajtatowicz@gmail.com`. I may have ran into the issue you have.  
If this helped and you'd like to leave a tip --> `0x20ad58fe023265577565c7eb44b55c31e7497c33`
