# HPL tests for whole clusters validation

The subdirectories contain SLURM script and template HPL input file to submit HPL job to validate whole sections of clusters after the downtime.

Each SLURM script needs have one input parameter - number of nodes on the partition to test. This can be obtained by running the `sinfo` command. Each cluster is divided into two partitions - general and owner. Below is the list of commands to start the validation runs on all the clusters. Note that each run must be in its unique directory (the HPL.dat input file is unique).

```
sbatch -N `sinfo -p notchpeak-guest | grep idle | awk '{ print $4 }'` runnp_guest.slr
sbatch -N `sinfo -p notchpeak | grep idle | awk '{ print $4 }'` runnp_gen.slr 
sbatch -N `sinfo -p kingspeak-guest | grep idle | awk '{ print $4 }'` runkp_guest.slr
sbatch -N `sinfo -p kingspeak | grep idle | awk '{ print $4 }'` runkp_gen.slr
sbatch -N `sinfo -p liu-lp | grep idle | awk '{ print $4 }'` runlp_guest.slr
sbatch -N `sinfo -p lonepeak | grep idle | awk '{ print $4 }'` runlp_gen.slr 
sbatch -N `sinfo -p ash-guest | grep idle | awk '{ print $4 }'` runash.slr
```

Note, that if there is an active reservation, the `--reservation` option needs to come before the SLURM script, e.g.
```
sbatch --reservation=downtime-2022-12-06 -N `sinfo -p ash-guest | grep idle | awk '{ print $4 }'` runash.slr
```

Upon valid completion of the run, the `.err` file should be empty, and the `.out` file will have a correct HPL output, e.g. 
```
================================================================================
T/V                N    NB     P     Q               Time                 Gflops
--------------------------------------------------------------------------------
WR11C2R4      445440   192    29    40            3630.54             1.6230e+04
```
