# P4SC YANNF-based Comparison Experiments

For running the traffic tests of DPDK-based P4SC comparsion examples, 
we choose two examples of Intel YANNF: Firewall and NAT in our experiments.

This branch maintains the modifications used to reproduce our traffic tests
that based on iperf. For running the two experiments, see OpenP4SC document:
[p4sc-yanff-examples](https://github.com/Emil-501/OpenP4SC/blob/master/docs/DPDK/readme.md#p4sc-yanff-examples).

Besides, we recommend to use the YANNF that is a high-level Network Function 
Framework written in Go language. YANNF provides some high level APIs and 
behaves the similar performance as original DPDK.

We record the modifications here:

2017/10/8:
- Modify the [Firewall.conf](https://github.com/Wasdns/yanff/blob/master/examples/Firewall.conf):
10 missed rules and 1 hit rule.
- Add `p4sc-exps.md` for recording these modifications.
