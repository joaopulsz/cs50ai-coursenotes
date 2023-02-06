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


## Resolution

A powerful inference rule that states that if one of two atomic propositions in an Or proposition is false, the other has to be true. 

It relies on **Complementary Literals**, two of the same atomic propositions where one is negated and the other is not, such as P and ¬P. Complementary literals allow us to generate new sentences through inferences by resolution. Thus, inference algorithms locate complementary literals to generate new knowledge.

A **Clause** is a disjunction of literals (a propositional symbol or a negation of a propositional symbol, such as P, ¬P). A **disjunction** consists of propositions that are connected with an Or logical connective (P ∨ Q ∨ R). A **conjunction**, on the other hand, consists of propositions that are connected with an And logical connective (P ∧ Q ∧ R). Clauses allow us to convert any logical statement into a **Conjunctive Normal Form (CNF)**, which is a conjunction of clauses, for example: (A ∨ B ∨ C) ∧ (D ∨ ¬E) ∧ (F ∨ G).

Steps in Conversion of Propositions to Conjunctive Normal Form:
- Eliminate biconditionals: turn (α ↔ β) into (α → β) ∧ (β → α).
- Eliminate implications: turn (α → β) into ¬α ∨ β.
- Move negation inwards until only literals are being negated (and not clauses), using De Morgan’s Laws: turn ¬(α ∧ β) into ¬α ∨ ¬β

Here’s an example of converting (P ∨ Q) → R to Conjunctive Normal Form:
- (P ∨ Q) → R
- ¬(P ∨ Q) ∨ R /Eliminate implication
- (¬P ∧ ¬Q) ∨ R /De Morgan’s Law
- (¬P ∨ R) ∧ (¬Q ∨ R) /Distributive Law

Resolving a literal and its negation, i.e. ¬P and P, gives the empty clause (). The empty clause is always false, and this makes sense because it is impossible that both P and ¬P are true. This fact is used by the resolution algorithm.

To determine if KB ⊨ α:
- Check: is (KB ∧ ¬α) a contradiction?
- If so, then KB ⊨ α.
- Otherwise, no entailment.

Proof by contradiction is a tool used often in computer science. If our knowledge base is true, and it contradicts ¬α, it means that ¬α is false, and, therefore, α must be true. More technically, the algorithm would perform the following actions:

To determine if KB ⊨ α:
- Convert (KB ∧ ¬α) to Conjunctive Normal Form.
- Keep checking to see if we can use resolution to produce a new clause.
- If we ever produce the empty clause (equivalent to False), congratulations! We have arrived at a contradiction, thus proving that KB ⊨ α.
- However, if contradiction is not achieved and no more clauses can be inferred, there is no entailment.

Here is an example that illustrates how this algorithm might work:
- Does (A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) entail A?
- First, to prove by contradiction, we assume that A is false. Thus, we arrive at (A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) ∧ (¬A).
- Now, we can start generating new information. Since we know that C is false (¬C), the only way (¬B ∨ C) can be true is if B is false, too. Thus, we can add (¬B) to our KB.
- Next, since we know (¬B), the only way (A ∨ B) can be true is if A is true. Thus, we can add (A) to our KB.
- Now our KB has two complementary literals, (A) and (¬A). We resolve them, arriving at the empty set, (). The empty set is false by definition, so we have arrived at a contradiction.


## First order logic

A type of logic that allows us to express more complex ideas more succinctly than propositional logic. First order logic uses two types of symbols: Constant Symbols and Predicate Symbols. Constant symbols represent objects, while predicate symbols are like relations or functions that take an argument and return a true or false value.

**Universal quantification** is a tool that can be used in first order logic to represent sentences without using a specific constant symbol. Universal quantification uses the symbol ∀ to express “for all.”

**Existential quantification** is an idea parallel to universal quantification. However, while universal quantification was used to create sentences that are true for all x, existential quantification is used to create sentences that are true for at least one x. It is expressed using the symbol ∃.

Existential and universal quantification can be used in the same sentence.

There are other types of logic as well, and the commonality between them is that they all exist in pursuit of representing information. These are the systems we use to represent knowledge in our AI.