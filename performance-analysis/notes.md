speedup = serial_time/parallel_time
number of cores = p

ex 4 processors x 25 parallel time => 100/25 = 4 perfect parallelization (25 25 25 25)
if you take synch cost into account 100/35 = 2.85 perfect load balancing (35 35 35 35)
load imbalanace (30 20 40 10)
 vs. 
 load imbalance + sync cost (most realistic scenario) - (30/50  20/50 40/50 10/50)

sources of parallel overhead:
- overhead creating threads/processes
- synchronization
- load imbalance
- commmunication
- memory access (more for openmp b/c shared memory, but applies to both sequential/parallel!)
- extra computation

efficiency: speedup/ processes = (serial_time/parallel_time) /p

time ./a.out
- real time (elapsed - counts everything)
- user time (CPU time - doesn't count I/O or other programs)
- sys time (CPU time)
we focus on CPU time (time spent executing actual lines of code "in" our program)

execution time includes I/O time, CPU time, disk/memory time
CPU time includes user CPU time and system CPU time

execution time:  time between start & completion of task
throughput: total amount of work done in given time

relationship between execution time & throughput: inverse

execution time for sequential program: ET = IC X CPI X CT
CPI = cycles per instruction
IC = instruction count

(seconds/program) = (cycles/program x seconds/cycle)

**** do four examples ****

for multithreaded programs, total number of instructions executed may differ across runs (threads can enter critical sections at different times, etc) -- variation increases with diff number of cores
system-level code accounts for significant part of total execution time

why we want benchmarks?
- measure performance and help identify bottlenecks & performance prediction