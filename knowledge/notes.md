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

The process of deriving new sentences from old ones

A way of infering knowledge based on previous knowledge is with a **model checking** algorithm:
To determine if KB ⊨ α (in other words, answering the question: “can we conclude that α is true based on our knowledge base”)
- Enumerate all possible models.
- If in every model where KB is true, α is true as well, then KB entails α (KB ⊨ α)

To run the Model Checking algorithm, the following information is needed:
- Knowledge Base, which will be used to draw inferences
- A query, or the proposition that we are interested in whether it is entailed by the KB
- Symbols, a list of all the symbols (or atomic propositions) used 
- Model, an assignment of truth and false values to symbols


**Knowledge engineering**: The process of figuring out how to represent propositions and logic in AI


## Inference rules

Allow us to generate new information based on existing knowledge without considering every possible model.

- **Modus ponens**: if we know an implication and its antecedent to be true, then the consequent is true as well.

- **And elimination**: if an And proposition is true, then any one atomic proposition within it is true as well.

- **Double negation elimination**: a proposition that is negated twice is true

- **Implication elimination**: an implication is equivalent to an Or relation between the negated antecedent and the consequent

- **Biconditional elimination**: a biconditional proposition is equivalent to an implication and its inverse with an And connective.

- **De Morgan's law**: it is possible to turn an And connective into an Or connective.

- **Distributive property**: a proposition with two elements that are grouped with And or Or connectives can be distributed, or broken down into, smaller units consisting of And and Or.


### Knowledge and search problems:
Inference can be viewed as a search problem with the following properties:

- Initial state: starting knowledge base
- Actions: inference rules
- Transition model: new knowledge base after inference
- Goal test: checking whether the statement that we are trying to prove is in the KB
- Path cost function: the number of steps in the proof