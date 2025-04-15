Turing machine can be formally defined as a 7-tuple $M = ⟨Q, \Gamma, b, \Sigma, \delta, q_0, F⟩$ where:
- $\Gamma$ is a finite, non-empty set of tape alphabet symbols
- $b \in \Gamma$ is the blank symbol
- $\Sigma \subseteq \Gamma \textbackslash \{b\}$ is the set of input symbols
- $Q$ is a finite, non-empty set of states
- $q_0 \in Q$ is the initial state
- $F \subseteq Q$ is the set of final states
- $\delta: (Q \textbackslash F) \times \Gamma \rightharpoonup Q \times \Gamma \times \{L, R\}$ is a partial function called the transition function, where L is left shift, R is right shift.