main concerns with OpenMP:
***** sequential code
	- amdahl's law (limitations of performance)
	- as small sequential code as possible because anything outside parallel, inside master, single, critical directives is sequential.

***** communication
	- shared memory for openmp means communication = increased memory access costs (takes longer to access data in main memory if temporal/spatial locality not taken advantage of)
	- communication is spread throughout the problem & memory access is expensive

***** cache coherency
	- shared memory programming assumes a shared variable has a uunique value
	- cache = multiple copies of memory location exist. make sure they're synchronized
	- avoid two processors caching diff values of a shared variable
	- snooping: need to invalidate outdated values (usually performed on cache lines in level closest cache) in other copies if current processor has changed it

	- coherency states: exclusive (only valid copy in cache); read-only (valid copy but others can contain it); invalid (out of date, don't use)
	- READ on invalid or absent cache = read-only
	- READ on exclusive cache = read-only
	- WRITE on non-exclusive cache will mark as other copies as INVALID and written line EXCLUSIVE

	- false sharing: invalidate other processor copies along cache line; poor speedup, high, non-determinstic number of cache misses and load imbalance expected

***** load imbalance
	- look at different scheduling types here

***** synchronization
	- omp barrier can be expensive
	- avoid using barries by carefully using NOWAIT clause.
	- parallellize at outermost level possible (ie. reorder loops/ indices)
	- **** when to use critical/ atomic/ lock routines ****

- data affinity: make sure each program uses distinct portion of data throughout program; threads will make excellent use of memory

***** compiler non optimization
	- parallel directives could interfere with sequential optimizations
	- for example, 1-thread parallel code takes longer than sequential code
	- maybe change shared data private or local to a routine *** example ***

analyzing time ./a.out
real - elapsed time total
user - CPU time
sys - CPU time

possible explanation of real time being much higher than CPU time is processor sharing too high load;
if there are enough processors, elapsed time should be less than CPU time
(omp_get_wtime())

- avoid parallellizing inner loops bc incurring overhead on parallel construct
- want to combine communication + computation overlap = make sure time taken is less than sum of time to do each separately


*** what are the disadvantages/ advantages of pure MPI? ***
+ portable to distributed & shared memory machines
+ scales beyond one node
+ no race conditions

- difficult to debug
- high latency, low bandwidth
- explicit communication
- difficult load balancing

*** what are the disadvantages/ advantages of pure openMP? ***
+ easy to implement
+ low latency, high bandwidth
+ implicit communication
+ dynamic load balancing

- only on shared
- scale within one node
- possible race condition
- no specific thread ordering (non deterministic)

^^^ aka they balance each other out

- software trend: hybrid MPI/openMP paradigm using MPI across nodes and openMP within nodes
- avoid communication overhead with MPI within nodes
- openMP adds fine granularity and dynamic load balancing
- offers better scalability than openmp and pure mpi by themselves

HOWEVER, there is then 
- thread creation overhead
- cache coherence probs
- pure openMP code worse than pure MPI 
- MPI communication 
(basically absorbing cons with both)

- see mixpi.c
