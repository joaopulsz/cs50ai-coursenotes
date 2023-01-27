# Knowledge

This lecture looks into the concept of representing knowledge and drawing conclusions from it using AI.

**Sentences** are how AI stores knowledge and uses it to infer new information. It is an assertion about the world in a knowledge representation language.


## Propositional logic

Based on propositions (statements) about the world that can be either true or false

**Propositional symbols** are most often letters (*P, Q, R*) that are used to represent propositions

**Legal connectives** are symbols that connect propositional symbols in order to reason in more complex ways:
- **Not (¬)** inverses the truth value of the proposition. So, for example, if P: “It is raining,” then ¬P: “It is not raining”.
- **And (∧)** connects two different propositions. When these two propositions, P and Q, are connected by ∧, the resulting proposition P ∧ Q is true only in the case that both P and Q are true.
- **Or (∨)** is true as as long as either of its arguments is true. This means that for P ∨ Q to be true, at least one of P or Q has to be true.
- **Implication (→)** represents a structure of “if P then Q.” For example, if P: “It is raining” and Q: “I’m indoors”, then P → Q means “If it is raining, then I’m indoors.” In the case of P implies Q (P → Q), P is called the *antecedent* and Q is called the *consequent*.
- **Biconditional (↔)** is an implication that goes both directions. You can read it as “if and only if.” P ↔ Q is the same as P → Q and Q → P taken together. For example, if P: “It is raining.” and Q: “I’m indoors,” then P ↔ Q means that “If it is raining, then I’m indoors,” and “if I’m indoors, then it is raining.” This means that we can infer more than we could with a simple implication. If P is false, then Q is also false; if it is not raining, we know that I’m also not indoors.

**Models** are assignments of a truth value to every proposition

The **Knowledge Base (KB)** contains knowledge that the AI is provided about the world in the form of propositional logic sentences that can be used to make additional inferences about the world

**Entailment (⊨)**: If α ⊨ β (α entails β), then in any world where α is true, β is true, too.


## Inference
