# lab_okd

day zero and day one of the okd installation

## Rationale

This lab is not meant for a quick peek at okd, this lab is meant to practise automating a real working environment deployment.
This deployment will initially be done with 3 master nodes which will initially be configured as worker nodes.
Since it is already expensive enough to use 3 real machines for this I will try to use only tools that are free to use for everybody.

After this is done I will address the following issues.

- adding worker nodes
- removing the worker role from the master nodes
- setting up gitops for the management of the cluster (argocd/git)
- adding storage (using csi)
- configuring the local registry to use that storage
- adding ldap authentication (external freeipa)
- adding certificates (using letsencrypt)

>If you just want a quick peek at okd, use the [code ready containers](https://www.okd.io/crc/) version for that.  
A nice instruction can be found [here](https://fedoramagazine.org/okd-on-fedora-workstation-with-crc/)
for setting up the okd environment with crc.

## The lab

```graphviz
digraph finite_state_machine {
    rankdir=LR;
    size="8,5"

    node [shape = doublecircle]; S;
    node [shape = point ]; qi

    node [shape = circle];
    qi -> S;
    S  -> q1 [ label = "a" ];
    S  -> S  [ label = "a" ];
    q1 -> S  [ label = "a" ];
    q1 -> q2 [ label = "ddb" ];
    q2 -> q1 [ label = "b" ];
    q2 -> q2 [ label = "b" ];
}
```

```graphviz
digraph switches {
  sw1 [ label="Switch 1\n192.168.1.101" ];
  sw2 [ label="Switch 2\n192.168.1.102" ];
  sw3 [ label="Switch 3\n192.168.1.103" ];
  sw4 [ label="Switch 4\n192.168.1.104" ];
  sw1 -> sw2;
  sw1 -> sw3;
  sw1 -> sw4;
  sw3 -> sw4;
  sw2 -> sw3;
}
```
