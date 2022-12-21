# HPL tests for single node

This directory contains a SLURM script and a template HPL input file to run a HPL calculation on a single node.

If the script is run via SLURM, a correct account/partition needs to be added, e.g
```
sbatch -A account -p partition run1n.slr
```

To run outside of SLURM, simply run the script through bash:
```
bash run1n.slr
```

The script will automatically figure out how many CPUs and memory the node has and run the HPL at 50% of the memory of the node. The memory size percentage can be changed with the `SIZE` parameter inside of the script.

Note that each run must be in its unique directory (the HPL.dat input file is unique).

Upon valid completion of the run, the stdout should have a correct HPL output, e.g. 
```
T/V                N    NB     P     Q               Time                 Gflops
--------------------------------------------------------------------------------
WR11C2R4       78336   192     4     8             249.15             1.2863e+03

```
this result was obtained on a 32 core Skylake node on Notchpeak.
