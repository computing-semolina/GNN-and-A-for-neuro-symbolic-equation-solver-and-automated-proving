# GNN-and-A-for-neuro-symbolic-equation-solver-and-automated-proving
A hybrid neuro-symbolic math engine combining SLM auto-formalization (Qwen) with Conv GNN-guided A* graph search over ASTs for deterministic proofs .
# Neuro-Symbolic Math Proof Engine (GNN + A* Search)

> ⚠️ **Status:** Research Prototype .

A hybrid neuro-symbolic AI system that combines Large/Small Language Models (auto-formalization) with deterministic Graph Neural Network (GNN) guided search over Abstract Syntax Trees (ASTs) to guarantee 100% sound mathematical proofs without probabilistic hallucination.

### 0. Natural Language Auto-Formalization (Qwen2.5-Math SLM)
- **Natural Language Translation:** Fine-tuned Small Language Model (SLM) that parses informal math word problems into structured symbolic DSL strings.
- **AST Formatting Guardrails:** Normalizes math intent into strict expression trees or `Eq()` equality predicates prior to graph parsing.

### 1. Symbolic AST & Pattern Matching Core
- **Immutable AST Engine:** Represents expressions (`Op`, `Var`, `Num`) and multi-fact logical states (`ProofState`) as immutable trees.
- **Bi-directional Pattern Matching:** Unifies wildcard variables (`?A`, `?B`) across 50+ domain rules while evaluating guard conditions (e.g., non-zero denominators).

### 2. Relational Knowledge Graph Converter
- **PyTorch Geometric Integration:** Transforms AST nodes and logical relations into heterogeneous graphs.
- **Heterogeneous Edges:** Encodes structural hierarchy (`AST_CHILD`) alongside domain-specific predicates (`PARALLEL`, `PERPENDICULAR`, `DIVIDES`, `EQUAL_TO`).

### 3. Deep RL Policy & Value Network (`RLUniversalMathRGNN`)
- **RGCN Backbone:** Multi-layer `RGCNConv` passes message vectors across distinct edge relations.
- **Actor Head (Policy):** Outputs action logits over valid rules, dynamically masked to enforce valid mathematical transformations.
- **Critic Head (Value):** Predicts scalar values estimating remaining search distance to a terminal solved state.

### 4. Neural-Guided Best-First Search ($A^*$)
- **Priority Evaluation:** Evaluates nodes via $f(n) = g(n) + h(n)$, balancing search depth penalties, policy log-probabilities, and value estimates.
- **Terminal Verification:** Validates variable isolation, target predicate proofs, or minimal complexity states.

### 5. Curriculum & Expert Iteration
- **Synthetic Backward Generation:** Applies inverse rewrite rules to construct self-supervised training trajectories.
- **Adaptive Curriculum & Replay:** Automatically scales search depth (1–8) at an 85% success threshold and rescales exploration noise on persistent failure states.

## to Start:
1. Open `neuro-symbolic solver.ipynb` directly in Google Colab.
2. Set runtime type to **T4 GPU**.
3. Run all cells to execute the rules suite, GNN search evaluator, and Qwen auto-formalization pipeline.
