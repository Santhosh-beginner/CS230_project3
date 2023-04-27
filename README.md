# CS230_project3

#IMPLEMENTATIONS
  we implemented replacement policies lru,lfu,fifo for LLC cache.
  These files are lfu.llc_repl,lru.llc_repl and fifo.llc_repl in replacement folder.
  we implemented prefetchers - next_line prefetcher for L1I,L1D,L2C,LLC and ip_stride prefetcher for L2C.
  These files are ip_stride.l2c_pref,next_line.l1i_pref,next_line.l1d_pref,next_line.l2c_pref,next_line.llc_pref in prefetcher folder.
  written code for exclusive,inclusive and noninclusive hierarchies. These files are cache_exclusive,cache_inclusive and cache_noninclusive respectively 
  in src folder.






#INSTRUCTIONS TO RUN
STEP-I
# Clone ChampSim repository
```
git clone https://github.com/ChampSim/ChampSim.git
```
STEP-2

There is no cache.cc in uploaded files.
If you want to run for a particular cache policy like inclusive or exclusive or non-inclusive rename that file as cache.cc
and comment out whole code of remaining 2 files.
for example:-   
           to run for inclusive cache 
                change cache_inclusive.cc to cache.cc
                and comment out whole code in cache_exclusive and cache_noninclusive.

STEP-3

ChampSim takes seven parameters: Branch predictor, L1I prefetcher, L1D prefetcher, L2C prefetcher, LLC prefetcher, LLC replacement policy, and the number of cores. 
For example, `./build_champsim.sh bimodal no no no next_line lru 1` builds a single-core processor with bimodal branch predictor, no L1 instruction prefetcher, no L1/L2 data prefetchers, ip-stride LLC prefetcher and the baseline LRU replacement policy for the LLC.
```
$ ./build_champsim.sh bimodal no no no next_line lru 1

$ ./build_champsim.sh ${BRANCH} ${L1I_PREFETCHER} ${L1D_PREFETCHER} ${L2C_PREFETCHER} ${LLC_PREFETCHER} ${LLC_REPLACEMENT} ${NUM_CORE}
```
Note :- use only implemented prefetchers and replacement polices as argumnets in above command.

STEP-4

# Run simulation

Execute `run_champsim.sh` with proper input arguments. The default `TRACE_DIR` in `run_champsim.sh` is set to `$PWD/dpc3_traces`. <br>

* Single-core simulation: Run simulation with `run_champsim.sh` script.

```
Usage: ./run_champsim.sh [BINARY] [N_WARM] [N_SIM] [TRACE] [OPTION]
$ ./run_champsim.sh bimodal-no-no-no-next_line-lru-1core 1 10 600.perlbench_s-210B.champsimtrace.xz

${BINARY}: ChampSim binary compiled by "build_champsim.sh" (bimodal-no-no-no-next_line-lru-1core)
${N_WARM}: number of instructions for warmup (1 million)
${N_SIM}:  number of instructinos for detailed simulation (10 million)
${TRACE}: trace name (600.perlbench_s-210B.champsimtrace.xz)
${OPTION}: extra option for "-low_bandwidth" (src/main.cc)
```
Note :- use only implemented prefetchers and replacement polices as argumnets in above command.

if you want Add your own branch predictor, data prefetchers, and replacement policy
**Copy an empty template**
```
$ cp branch/branch_predictor.cc branch/mybranch.bpred
$ cp prefetcher/l1i_prefetcher.cc prefetcher/mypref.l1i_pref
$ cp prefetcher/l1d_prefetcher.cc prefetcher/mypref.l1d_pref
$ cp prefetcher/l2c_prefetcher.cc prefetcher/mypref.l2c_pref
$ cp prefetcher/llc_prefetcher.cc prefetcher/mypref.llc_pref
$ cp replacement/llc_replacement.cc replacement/myrepl.llc_repl
```

**Work on your algorithms with your favorite text editor**
```
$ vim branch/mybranch.bpred
$ vim prefetcher/mypref.l1i_pref
$ vim prefetcher/mypref.l1d_pref
$ vim prefetcher/mypref.l2c_pref
$ vim prefetcher/mypref.llc_pref
$ vim replacement/myrepl.llc_repl
```

4 Traces are available in "dpc3_traces" folder which we use to obtain the results.
All results we obtained are in "resultoftraces" folder . In this folder results are grouped in 4 different folders for 4 differet traces we used
and in each trace folder we have results for inclusive, exclusive and noninclusive.
if you want to run simulation for other trace add trace to dpc3_traces folder and follow above steps for running.


Simulation results will be stored under "results_${N_SIM}M" as a form of "${TRACE}-${BINARY}-${OPTION}.txt".<br> 

* Multi-core simulation: Run simulation with `run_4core.sh` script. <br>
```
Usage: ./run_4core.sh [BINARY] [N_WARM] [N_SIM] [N_MIX] [TRACE0] [TRACE1] [TRACE2] [TRACE3] [OPTION]
$ ./run_4core.sh bimodal-no-no-no-next_line-lru-4core 1 10 0 600.perlbench_s-210B.champsimtrace.xz \\
  401.bzip2-38B.champsimtrace.xz 403.gcc-17B.champsimtrace.xz 410.bwaves-945B.champsimtrace.xz
```
Note that we need to specify multiple trace files for `run_4core.sh`. `N_MIX` is used to represent a unique ID for mixed multi-programmed workloads. 





#Conclusions from results
Compared different cache hierarchies (different sizes of L1, L2, LLC,inclusive/non-inclusive/Exclusive) and cache replacement policies,
with a baseline cache hierarchy, and which is best i.e improved cache performance.
This is explained in  this "https://youtu.be/xpPgRtaQDPU" video.
presentation used for this video is under this link - "https://iitbacin-my.sharepoint.com/:p:/g/personal/210050162_iitb_ac_in/EcQg3ZaIZM5LpteZEI22XQ4B7Hn6TeCOoLma49Ms6OXX6A?e=hqszBJ&nav=eyJzSWQiOjI1NiwiY0lkIjoyNDI0NTM4MzF9"







