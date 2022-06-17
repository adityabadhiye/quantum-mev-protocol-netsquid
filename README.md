
# Simulating Multipartite Entanglement Verification Protocol using NetSquid


The goal of this project is to simulate the Multipartite Entanglement Verification protocol in a quantum network with N participating nodes. The choice of the verifier may be random or fixed.


## Approach
*θ-protocol* which is successor of *xy-protocol* described in [this](https://www.nature.com/articles/ncomms13251.pdf?origin=ppub) paper was implemented.

Flow diagram of protocol is shown below.
![Flow Diagram](https://github.com/adityabadhiye/mev-protocol-netsquid/blob/main/images/flow_diagram.png)

## Implementation
The network scenario we consider consists of a *source* and *n* parties with **1 fixed verifier(at 0 index)**.
Source shares an n-qubit state ρ with n parties. One of the parties, a
‘Verifier’, would like to verify how close this shared state is to
the ideal state and whether or not it contains GME.

### Protocols
#### SourceProtocol
Source shares an n-qubit state ρ with n parties.
#### PartyProtocol
Each party first recives its state from source through a QuantumChannel.
- If the party is verifier, it sends random angles to other parties including itself via ClassicalPrivateChannel and verifies for Entanglement.
- else it recives angle from verifier, measures and sends its state in corresponding basis.

### Channels
#### Quantum Channels
- n *s2p_qcs(Source to Party)* were used for sharing n-qubit state ρ with n parties.
#### Classical Channels
- n-1 *v2p_ccs(Verifier to Party)* were used.
- n-1 *p2v_ccs(Party to Verifier)* were used.

## Result
The verification protocol is then tested for the following input states:

- #### The input state is the N-partite GHZ state.
Protocol succeeds with probability P(Honest) = 1 *(always 1 in all no-loss cases)*
- #### The input state is *|0>* on all N-qubits.
Protocol succeeds with probability P(Dishonest) = 0.55 (for n=4, 100 testcase).

Explanation for the same is given in below image
for *|0>* state, it can be seen that all the states are possible after applying protocol

![Dishonest States](https://github.com/adityabadhiye/mev-protocol-netsquid/blob/main/images/dishonest.png)



but for GHZ state the equation always holds true

![eq](https://latex.codecogs.com/svg.image?%5Cinline%20%5Cdpi%7B110%7D%5Cbg%7Bwhite%7D%5Cbigoplus_%7Bj%7D%20Y_%7Bj%7D%20=%20%5Cfrac%7B1%7D%7B%5Cpi%20%7D%5C%20%5Csum_%7Bj%7D%20%5Ctheta_%7Bj%7D%20%5Chspace%7B5mm%7D%20%20%5Ctextbf%7B(mod%202)%7D)
![Honest State](https://github.com/adityabadhiye/mev-protocol-netsquid/blob/main/images/honest.png)
