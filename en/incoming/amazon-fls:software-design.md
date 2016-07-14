# software design
## (1) what problem you're solving?
- does it scale?
- does it use other service efficiently?
- is it secured?
- how to leverage service X?
- how can we simplify?
- are there any other solutions?

## (2) scale problem: resource bottle neck
- disk access time
- network round trip
- CPU cache
- network latency
- service latency
- garbage collector
- file descripter

### Reading:
- [Latency Numbers Every Programmer Should Know](https://gist.github.com/jboner/2841832)
- [What Every Programmer Should Know about Memory](https://www.akkadia.org/drepper/cpumemory.pdf)

## (3) verify design
formal and informal design review


## multi-thread is hard (human brain does not have [MESI protocol](https://en.wikipedia.org/wiki/MESI_protocol)).

###Example: 
AWS IoT message broker
([count down latch](https://stackoverflow.com/questions/17827022/how-is-countdownlatch-used-in-java-multithreading)): only poll the incoming queue when the load is high

distributed programming is harder: no lock, etc.

- [Paxos](https://en.wikipedia.org/wiki/Paxos_(computer_science))
- [Quorum](https://en.wikipedia.org/wiki/Quorum_(distributed_computing))

## Take-aways
### DRY (don't repeat yourself) v.s. Rule of Three
### [Goldilocks rule](https://en.wikipedia.org/wiki/Goldilocks_principle)
packaging software

[square root of complexity](https://stackoverflow.com/questions/33194931/when-can-an-algorithm-have-square-rootn-time-complexity)

###YAGNI (you ain't gonna need it)
add documentation to eliminate YAGNI

## (4) understand your dependency

## (5) KISS

> Written with [StackEdit](https://stackedit.io/).