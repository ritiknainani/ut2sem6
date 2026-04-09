# 🎯 System Programming & Compiler Construction (SPCC) — PT-II Complete Guide
## Mumbai University | Computer Engineering | SEM 6 | REV-2019

---

# 📊 PART A: QUESTION BANK ANALYSIS & PRIORITY

## Exam Format
| Parameter | Detail |
|-----------|--------|
| **Total Marks** | 20 Marks |
| **Duration** | 1 Hour |
| **Syllabus** | Compiler Design (Attributes, Parsing, ICG, Optimization), Assemblers, Loaders |
| **Style** | Theory + Diagrams + Parsing Problems |

## 🔥 Topic-Wise Priority

| Priority | Topic | Questions |
|----------|-------|-----------|
| 🔴 **HIGHEST** | Code Optimization Techniques | Q2, Q8 |
| 🔴 **HIGHEST** | Intermediate Code (Quadruples, Triples) | Q10, Q12 |
| 🟠 **HIGH** | Two Pass Assembler | Q4 |
| 🟠 **HIGH** | LL(1)/LR(0)/Predictive/Operator Precedence Parsers | Q11 |
| 🟡 **MEDIUM** | Basic Blocks & Flow Graph | Q3 |
| 🟡 **MEDIUM** | Synthesized & Inherited Attributes | Q1 |
| 🟡 **MEDIUM** | Loaders (Absolute, Direct Linking) | Q5, Q7 |
| 🟢 **STANDARD** | Forward Reference Problem | Q6 |
| 🟢 **STANDARD** | Assembly Language Statements | Q9 |

---

# 📝 PART B: COMPLETE ANSWERS

---

# COMPILER DESIGN

---

## Q.1) Synthesized and Inherited Attributes

### Attributes
**Attributes** are values associated with grammar symbols (terminals and non-terminals) used in **Syntax-Directed Definitions (SDD)** to compute semantic information during parsing.

---

### Synthesized Attributes
**Definition:** An attribute of a **non-terminal** whose value is computed from the attributes of its **children** in the parse tree (bottom-up flow).

- Value flows **upward** (from children to parent)
- Can be evaluated in a **bottom-up** parser (e.g., LR parser)
- **S-attributed SDD** = SDD with only synthesized attributes

**Example — Simple Calculator (E → E1 + T):**

```
Production              Semantic Rule
─────────────           ─────────────
E → E1 + T              E.val = E1.val + T.val
E → T                   E.val = T.val
T → T1 * F              T.val = T1.val * F.val
T → F                   T.val = F.val
F → (E)                 F.val = E.val
F → digit               F.val = digit.lexval
```

**Parse tree for 3 * 5 + 4:**
```
              E.val = 19
             / │ \
       E.val=15 +  T.val=4
          │           │
       T.val=15    F.val=4
       / │ \         │
  T.val=3 * F.val=5  4
     │        │
  F.val=3     5
     │
     3

Values flow UPWARD ↑ (synthesized)
```

---

### Inherited Attributes
**Definition:** An attribute of a non-terminal whose value is computed from the attributes of its **parent** and/or **siblings** in the parse tree (top-down or lateral flow).

- Value flows **downward** or **sideways**
- Cannot be evaluated by pure bottom-up parser
- Used in **L-attributed SDDs** (evaluated left-to-right)

**Example — Type Declaration (D → T L):**
```
Production              Semantic Rule
─────────────           ─────────────
D → T L                 L.inh = T.type        (inherited)
T → int                 T.type = integer
T → float               T.type = float
L → L1, id              L1.inh = L.inh        (inherited)
                        addtype(id.entry, L.inh)
L → id                  addtype(id.entry, L.inh)
```

**Parse tree for "float id1, id2, id3":**
```
               D
              / \
        T.type=  L.inh=float
        float     / │ \
                L.inh=  , id3 → addtype(id3, float)
                float
                / │ \
              L.inh= , id2 → addtype(id2, float)
              float
                │
              id1 → addtype(id1, float)

Type flows DOWNWARD ↓ (inherited)
```

### Comparison:

| Feature | Synthesized | Inherited |
|---------|-------------|-----------|
| **Direction** | Bottom-up (children → parent) | Top-down (parent → children) |
| **Evaluation** | Post-order traversal | Pre-order / left-to-right |
| **Parser type** | Works with LR (bottom-up) | Needs L-attributed evaluation |
| **Example** | Calculating expression value | Propagating type info |

---

## Q.2) Code Optimization Techniques

### Definition
**Code optimization** transforms code to make it **run faster** or **use less memory** while preserving the program's meaning (semantics).

---

### A) Machine-Independent Optimization

**1. Constant Folding:**
```
Before:  x = 2 * 3 + 5
After:   x = 11          (computed at compile time)
```

**2. Constant Propagation:**
```
Before:  x = 5            After:  x = 5
         y = x * 2                y = 10
         z = y + x                z = 15
```

**3. Common Subexpression Elimination (CSE):**
```
Before:  a = b + c        After:  t = b + c
         d = b + c                a = t
                                  d = t
```

**4. Dead Code Elimination:**
```
Before:  x = 10           After:  x = 10
         y = 20                   z = x + 5
         z = x + 5
         (y is never used → remove it)
```

**5. Copy Propagation:**
```
Before:  x = y             After:  (use y directly instead of x)
         z = x + 1                 z = y + 1
```

**6. Loop Optimization:**

**(a) Code Motion / Loop-Invariant Code Motion:**
```
Before:  for(i=0; i<n; i++)     After:  t = n * 5;
           a[i] = n * 5;                for(i=0; i<n; i++)
                                           a[i] = t;
```

**(b) Induction Variable Elimination:**
```
Before:  for(i=0;i<10;i++)      After:  t=0;
           t = i * 4;                   for(i=0;i<10;i++){
                                           // use t directly
                                           t = t + 4;
                                         }
```

**(c) Loop Unrolling:**
```
Before:  for(i=0;i<4;i++)       After:  a[0]=0; a[1]=1;
           a[i]=i;                      a[2]=2; a[3]=3;
```

**7. Strength Reduction:**
```
Before:  x = y * 2        After:  x = y << 1    (shift is faster)
Before:  x = y * 8        After:  x = y << 3
Before:  x = y / 4        After:  x = y >> 2
Before:  x = y ^ 2        After:  x = y * y
```

**8. Function Inlining:**
```
Before:  int sq(int x){ return x*x; }   After:  y = x * x;
         y = sq(x);
```

---

### B) Machine-Dependent Optimization

**1. Register Allocation:**
```
Keep frequently used variables in CPU registers
instead of accessing slower memory.
Example: loop counter i → keep in register
```

**2. Instruction Scheduling / Pipeline Optimization:**
```
Reorder instructions to avoid pipeline stalls
and maximize parallel execution in CPU.
```

**3. Use of Machine-Specific Instructions:**
```
Use specialized instructions like:
  - SIMD (Single Instruction, Multiple Data)
  - Hardware multiply-accumulate (MAC)
  - Conditional move (CMOV) to avoid branches
```

**4. Peephole Optimization (see Q.8):**
```
Optimize small window of instructions:
  - Redundant load/store elimination
  - Algebraic simplification
  - Branch optimization
```

---

## Q.3) Basic Blocks and Flow Graph

### Basic Block
**Definition:** A **basic block** is a sequence of consecutive statements where:
- Control enters **only at the first** statement (leader)
- Control leaves **only at the last** statement
- **No jumps** into or out of the middle

### Rules to Identify Leaders:
1. **First statement** is a leader
2. **Target of any jump** (goto, if-goto) is a leader
3. **Statement immediately after** a jump is a leader

### Example:
```
Three-Address Code:        Leaders & Basic Blocks:

1.  i = 1                 LEADER → Block B1: {1, 2}
2.  j = 1
3.  t1 = 10 * i           LEADER → Block B2: {3, 4, 5, 6, 7}
4.  t2 = t1 + j
5.  t3 = 8 * t2
6.  t4 = t3 - 88
7.  a[t4] = 0.0
8.  j = j + 1             LEADER → Block B3: {8, 9}
9.  if j <= 10 goto 3
10. i = i + 1              LEADER → Block B4: {10, 11}
11. if i <= 10 goto 3
12. i = 1                  LEADER → Block B5: {12, ...}
```

**Why leaders:**
- Line 1: first statement
- Line 3: target of goto (from line 9 and 11)
- Line 8: follows conditional jump at line 7... wait, there's no jump at 7. Line 8: after sequential from B2, actually let me re-check. Line 8 follows line 7 sequentially within the block; line 9 has a conditional goto. Line 10 is the statement after the conditional (line 9).
- Line 10: statement after conditional jump (line 9)
- Line 12: statement after conditional jump (line 11)

### Flow Graph:
```
┌──────┐
│  B1  │ i=1, j=1
└──┬───┘
   │
   ▼
┌──────┐ ←─────────────┐
│  B2  │ t1=10*i...     │
│      │ a[t4]=0.0      │
└──┬───┘                │
   │                    │
   ▼                    │
┌──────┐                │
│  B3  │ j=j+1          │
│      │ if j<=10 ──────┘
└──┬───┘
   │ (j>10)
   ▼
┌──────┐
│  B4  │ i=i+1
│      │ if i<=10 ──────→ B2
└──┬───┘
   │ (i>10)
   ▼
┌──────┐
│  B5  │ ...
└──────┘
```

### Key Terms:
- **Predecessor** of B: block that can transfer control TO B
- **Successor** of B: block that can receive control FROM B
- **Dominator**: Block A dominates B if every path from entry to B goes through A
- **Loop**: Set of blocks with a back edge (edge from block to its dominator)

---

## Q.8) Peephole Optimization

### Definition
**Peephole optimization** examines a small **sliding window** (peephole) of target instructions and replaces them with **shorter/faster** equivalents.

### Techniques:

**1. Redundant Instruction Elimination:**
```
Before:  MOV R0, a          After:  MOV R0, a
         MOV a, R0                  (second removed — redundant)
```

**2. Unreachable Code Elimination:**
```
Before:  goto L2            After:  goto L2
         x = x + 1                  (removed — unreachable)
```

**3. Flow-of-Control Optimization (Jump Chaining):**
```
Before:  goto L1            After:  goto L2
         ...                        (skip intermediate jump)
  L1:    goto L2
```

**4. Algebraic Simplification:**
```
Before:  x = x + 0          After:  (removed — no effect)
Before:  x = x * 1          After:  (removed — no effect)
Before:  x = x * 2          After:  x = x << 1 (strength reduction)
```

**5. Use of Machine Idioms:**
```
Before:  x = x + 1          After:  INC x   (single instruction)
Before:  x = x - 1          After:  DEC x
```

**6. Redundant Load/Store Elimination:**
```
Before:  STORE R0, x        After:  STORE R0, x
         LOAD R0, x                 (LOAD removed — R0 already has x)
```

---

## Q.10) Intermediate Code Representations

### What is Intermediate Code?
An **intermediate representation (IR)** is a machine-independent form used between the front end (parser) and back end (code generator) of a compiler.

### Types of Intermediate Code:

### 1. Three-Address Code (TAC)
Each instruction has **at most 3 addresses** (operands): result = arg1 op arg2

**Example:** For expression `a = b * -c + b * -c`
```
t1 = -c
t2 = b * t1
t3 = -c
t4 = b * t3
t5 = t2 + t4
a = t5
```

### 2. Syntax Tree (AST)
```
Expression: a = b * -c + b * -c

            =
           / \
          a    +
              / \
            *     *
           / \   / \
          b   -  b   -
              |      |
              c      c
```

### 3. DAG (Directed Acyclic Graph)
Like syntax tree but **shares common subexpressions:**
```
            =
           / \
          a    +
              / \
            *     (same node reused)
           / \
          b   -
              |
              c

DAG eliminates redundant computation of b * (-c)
```

### 4. Postfix Notation (Polish)
```
Expression: a + b * c
Postfix:    a b c * +
```

---

## Q.12) Quadruples, Triples, and Indirect Triples

These are **data structures** for representing Three-Address Code.

### Example Expression: `a = b * -c + b * -c`

**Three-Address Code:**
```
(1)  t1 = -c
(2)  t2 = b * t1
(3)  t3 = -c
(4)  t4 = b * t3
(5)  t5 = t2 + t4
(6)  a = t5
```

---

### Quadruples (4 fields: op, arg1, arg2, result)

| # | Op | Arg1 | Arg2 | Result |
|---|-----|------|------|--------|
| (0) | uminus | c | | t1 |
| (1) | * | b | t1 | t2 |
| (2) | uminus | c | | t3 |
| (3) | * | b | t3 | t4 |
| (4) | + | t2 | t4 | t5 |
| (5) | = | t5 | | a |

**Advantage:** Easy to rearrange (each entry is self-contained)
**Disadvantage:** Uses many temporaries

---

### Triples (3 fields: op, arg1, arg2 — NO result field)
Results are referenced by their **statement number/position**.

| # | Op | Arg1 | Arg2 |
|---|-----|------|------|
| (0) | uminus | c | |
| (1) | * | b | (0) |
| (2) | uminus | c | |
| (3) | * | b | (2) |
| (4) | + | (1) | (3) |
| (5) | = | a | (4) |

**Advantage:** No temporary names needed; saves space
**Disadvantage:** Hard to rearrange (position-dependent references)

---

### Indirect Triples
Same as triples but uses an **indirection list** — a separate array of pointers to triple entries.

**Indirection List:**

| # | Statement |
|---|-----------|
| (0) | → (14) |
| (1) | → (15) |
| (2) | → (16) |
| (3) | → (17) |
| (4) | → (18) |
| (5) | → (19) |

**Triple Table:**

| # | Op | Arg1 | Arg2 |
|---|-----|------|------|
| (14) | uminus | c | |
| (15) | * | b | (14) |
| (16) | uminus | c | |
| (17) | * | b | (16) |
| (18) | + | (15) | (17) |
| (19) | = | a | (18) |

**Advantage:** Can rearrange by changing indirection list (without moving triples)
**Disadvantage:** Extra indirection overhead

### Comparison:

| Feature | Quadruples | Triples | Indirect Triples |
|---------|-----------|---------|-------------------|
| **Fields** | 4 (op, arg1, arg2, result) | 3 (op, arg1, arg2) | 3 + pointer list |
| **Temporaries** | Explicit (t1, t2...) | Implicit (by position) | Implicit |
| **Rearrangement** | Easy | Difficult | Easy (change pointers) |
| **Space** | More (temp names) | Less | Medium |
| **Optimization** | Easiest | Hardest | Good |

---

# ASSEMBLER & LOADER

---

## Q.4) Two-Pass Assembler

### Why Two Passes?
The **forward reference problem** — a symbol may be used before it is defined. Two passes resolve all symbol addresses.

### Pass 1: Define Symbols (Build Symbol Table)

**Purpose:** Assign addresses to all symbols; build the **Symbol Table (SYMTAB)** and **Literal Table (LITTAB)**.

**Databases for Pass 1:**

| Database | Purpose |
|----------|---------|
| **SYMTAB** (Symbol Table) | Stores symbol names and their addresses |
| **LITTAB** (Literal Table) | Stores literals and their assigned addresses |
| **OPTAB** (Opcode Table) | Maps mnemonics → opcode + instruction length |
| **Location Counter (LC)** | Tracks current address during assembly |
| **POOLTAB** (Pool Table) | Tracks literal pool boundaries |

**Pass 1 Algorithm:**
```
1. Initialize LC = 0 (or START address)
2. Read next assembly statement
3. If label present → add (label, LC) to SYMTAB
4. If opcode is in OPTAB:
     LC = LC + instruction length
5. If directive:
     START: set LC
     EQU: add symbol = operand value to SYMTAB
     DS/DC: allocate space, update LC
     LTORG/END: assign addresses to pending literals
6. Repeat until END
7. Output: SYMTAB, LITTAB, Intermediate Code
```

### Pass 2: Generate Object Code

**Purpose:** Generate **machine code** using SYMTAB, LITTAB, and OPTAB.

**Databases for Pass 2:**

| Database | Purpose |
|----------|---------|
| **SYMTAB** (from Pass 1) | Look up symbol addresses |
| **LITTAB** (from Pass 1) | Look up literal addresses |
| **OPTAB** | Get opcodes |
| **Intermediate Code** | From Pass 1 |

**Pass 2 Algorithm:**
```
1. Read intermediate code statement
2. If opcode → look up opcode in OPTAB
3. For operands:
     If symbol → look up address in SYMTAB
     If literal → look up address in LITTAB
4. Assemble instruction: opcode + operand address
5. Write to object code file
6. Repeat until END
7. Output: Object Program
```

### Example:
```
Assembly Code:          Pass 1 (SYMTAB):    Pass 2 (Object Code):

START 200               Symbol | Addr       Addr | Code
LOOP  MOVER R1, A       LOOP   | 200        200  | 04 1 210
      ADD R1, B         A      | 210        203  | 01 1 211
      COMP R1, ='5'     B      | 211        206  | 06 1 212
      BC LE, LOOP        ='5'  | 212        209  | 07 2 200
A     DS 1                                  210  | -- (reserved)
B     DC '3'                                211  | 00 00 03
      END                                   212  | 00 00 05
```

---

## Q.5) Absolute Loader

### Definition
An **absolute loader** loads an object program into **fixed memory locations** as specified by the assembler. The load addresses are **predetermined** and cannot be changed.

### How it Works:
```
1. Read Header record → check program name, length
2. Read each Text record:
   - Extract start address and object code
   - Load object code directly at the specified address
3. Read End record → jump to execution start address
```

```
Object Program          Memory
┌──────────────┐        ┌──────────┐
│ H | PROG |   │        │          │
│ 1000 | 200   │        │   ...    │
├──────────────┤        ├──────────┤
│ T | 1000 |   │ ──────>│ 1000: xx │ ← loaded at fixed address
│   obj code   │        │ 1001: xx │
├──────────────┤        │ ...      │
│ T | 1050 |   │ ──────>│ 1050: xx │
│   obj code   │        │ ...      │
├──────────────┤        ├──────────┤
│ E | 1000     │        │          │
└──────────────┘        └──────────┘
                        Start execution at 1000
```

### Advantages:
1. **Simple design** — no relocation or linking needed
2. **Fast loading** — direct placement, no address modification
3. Easy to implement

### Disadvantages:
1. **No flexibility** — program MUST load at fixed address
2. **No relocation** — if address occupied, program cannot load
3. **No linking** — cannot combine multiple object programs
4. **Wasteful** — memory fragmentation if fixed addresses clash
5. Programmer must know exact load addresses

---

## Q.6) Forward Reference Problem

### What is the Forward Reference Problem?
When an assembler encounters a **symbol that hasn't been defined yet** during the first scan, it cannot determine the symbol's address.

```
Example:
        MOV R1, X       ← X is used here
        ADD R1, Y       ← Y is used here
        ...
X       DS 1            ← X is defined LATER (forward reference!)
Y       DC '5'          ← Y is defined LATER
```

At the time of processing `MOV R1, X`, the assembler doesn't know the address of X because X is defined later in the program.

### How is it Solved?

**Solution 1: Two-Pass Assembly**
```
Pass 1: Scan entire program → build complete SYMTAB with all addresses
Pass 2: Use SYMTAB to resolve all references (forward or backward)
```
This is the **most common** and **standard** solution.

**Solution 2: One-Pass Assembly (Backpatching)**
```
1. When forward reference encountered:
   - Leave address field blank (or zero)
   - Add to a "pending" list for that symbol
   
2. When symbol is eventually defined:
   - Go back and fill in (backpatch) all pending references

Example:
  Line 1: MOV R1, X  → address of X unknown → emit 04 1 ???
  Line 2: ADD R1, Y  → address of Y unknown → emit 01 1 ???
  ...
  Line 5: X DS 1     → X = address 210 → backpatch line 1 → 04 1 210
  Line 6: Y DC '5'   → Y = address 211 → backpatch line 2 → 01 1 211
```

---

## Q.7) Direct Linking Loader

### Definition
A **direct linking loader** (or **relocating linking loader**) can load, **relocate**, and **link** multiple independently assembled object programs into a single executable in memory.

### Features:
- Handles **relocation** (adjusts addresses for actual load location)
- Handles **linking** (resolves inter-module references)
- Allows **modular programming**

### Key Concepts:
```
EXTRN — symbols defined in OTHER modules (external references)
ENTRY — symbols defined HERE, available to other modules (public symbols)
```

### How it Works (Two Passes):

**Pass 1: Assign Addresses**
```
For each object module:
1. Read header → get module name, length
2. Assign load address = current next available address
3. Read Define records → add to ESTAB (External Symbol Table)
   ESTAB entries: (symbol, module, address + relocation offset)
4. Update next available address += module length
```

**Pass 2: Load and Relocate**
```
For each object module:
1. Read Text records → load object code at relocated address
2. Read Modification records:
   - Find the address to modify
   - Look up external symbol in ESTAB
   - Add/modify the reference with correct address
3. At end → transfer to execution start address
```

### Example — Linking Two Modules:
```
Module A (length 200):          Module B (length 150):
  ENTRY: ALPHA                    ENTRY: BETA
  EXTRN: BETA                    EXTRN: ALPHA
  ...                             ...
  CALL BETA  ← needs B's addr    CALL ALPHA ← needs A's addr

Loading at address 1000:
  Module A: 1000 - 1199
  Module B: 1200 - 1349

ESTAB:
  ALPHA → 1000 + relative_offset
  BETA  → 1200 + relative_offset

Linker patches:
  In A: CALL BETA → CALL 1200+offset
  In B: CALL ALPHA → CALL 1000+offset
```

### Comparison: Absolute vs Direct Linking Loader:

| Feature | Absolute Loader | Direct Linking Loader |
|---------|----------------|----------------------|
| **Relocation** | No | Yes |
| **Linking** | No | Yes |
| **Flexibility** | Fixed addresses | Any available address |
| **Multi-module** | No | Yes |
| **Complexity** | Simple | More complex |

---

## Q.9) Types of Assembly Language Statements

### Three Types:

### 1. Imperative Statements (Machine Instructions)
**Definition:** Statements that **translate directly** into machine instructions and are **executed** by the processor.

```
Examples:
  MOVER R1, A       → loads value of A into register R1
  ADD R1, B         → adds value of B to R1
  COMP R1, C        → compares R1 with C
  BC GT, LOOP       → branch to LOOP if greater than
  MOVEM R1, RESULT  → stores R1 into RESULT
```

### 2. Declarative Statements (Data Definition)
**Definition:** Statements that **allocate memory** and optionally **initialize** data. NOT executed.

| Directive | Meaning | Example |
|-----------|---------|---------|
| **DS** (Define Storage) | Reserve memory (no initialization) | `A DS 5` → reserves 5 words |
| **DC** (Define Constant) | Reserve + initialize with value | `B DC '25'` → stores value 25 |

### 3. Assembler Directives (Pseudo-opcodes)
**Definition:** Statements that **instruct the assembler** how to process the program. NOT executed and do NOT generate machine code.

| Directive | Purpose | Example |
|-----------|---------|---------|
| **START** | Set starting address | `START 200` |
| **END** | Mark end of program | `END` |
| **ORIGIN** | Set LC to specified address | `ORIGIN 300` |
| **EQU** | Assign value to symbol | `COUNT EQU 5` |
| **LTORG** | Assign addresses to accumulated literals | `LTORG` |
| **USING** | Specify base register | |

---

## Q.11) Parsers — LL(1), LR(0), Predictive, Operator Precedence

### LL(1) Parser

**Definition:** **Top-down** parser. Reads input **Left-to-right**, produces **Leftmost derivation**, with **1** lookahead symbol.

**LL(1) Parsing Table Construction:**
```
1. Compute FIRST sets for all non-terminals
2. Compute FOLLOW sets for all non-terminals
3. Build parsing table M[A, a]:
   For each production A → α:
     For each terminal a in FIRST(α): add A → α to M[A, a]
     If ε ∈ FIRST(α): for each b in FOLLOW(A): add A → α to M[A, b]
4. If any cell has multiple entries → NOT LL(1)
```

**Example Grammar:**
```
E  → TE'
E' → +TE' | ε
T  → FT'
T' → *FT' | ε
F  → (E) | id

FIRST(E) = FIRST(T) = FIRST(F) = { (, id }
FIRST(E') = { +, ε }
FIRST(T') = { *, ε }
FOLLOW(E) = FOLLOW(E') = { ), $ }
FOLLOW(T) = FOLLOW(T') = { +, ), $ }
FOLLOW(F) = { *, +, ), $ }
```

**LL(1) Parsing Table:**

|  | id | + | * | ( | ) | $ |
|--|----|----|---|---|---|---|
| E | E→TE' | | | E→TE' | | |
| E' | | E'→+TE' | | | E'→ε | E'→ε |
| T | T→FT' | | | T→FT' | | |
| T' | | T'→ε | T'→*FT' | | T'→ε | T'→ε |
| F | F→id | | | F→(E) | | |

---

### LR(0) Parser

**Definition:** **Bottom-up** parser. Reads input **Left-to-right**, produces **Rightmost derivation** in reverse, with **0** lookahead.

**LR(0) Item:** A production with a **dot (•)** indicating how much has been parsed.
```
A → •XYZ  (nothing parsed yet)
A → X•YZ  (X has been parsed)
A → XY•Z  (XY parsed)
A → XYZ•  (complete — ready to reduce)
```

**Steps to build LR(0) parser:**
```
1. Augment grammar: add S' → S
2. Build canonical collection of LR(0) item sets (states)
   - I0 = closure({S' → •S})
   - Compute GOTO(I, X) for each state I and symbol X
3. Build ACTION and GOTO tables:
   - If [A → α•aβ] in Ii and GOTO(Ii, a) = Ij → ACTION[i, a] = shift j
   - If [A → α•] in Ii → ACTION[i, a] = reduce A → α (for all terminals)
   - If [S' → S•] in Ii → ACTION[i, $] = accept
```

---

### Predictive Parser

**Definition:** A **recursive descent parser** that uses **1 symbol of lookahead** to decide which production to use. No backtracking. Basically the **implementation** of LL(1) parsing.

**Structure:**
```
- One procedure per non-terminal
- Each procedure looks at current input token
- Chooses the correct production based on FIRST/FOLLOW sets
- Calls other procedures for non-terminals in RHS

procedure E():
   call T()
   call E_prime()

procedure E_prime():
   if lookahead == '+':
      match('+')
      call T()
      call E_prime()
   else:
      // ε production (do nothing)

procedure T():
   call F()
   call T_prime()

procedure F():
   if lookahead == 'id':
      match('id')
   elif lookahead == '(':
      match('(')
      call E()
      match(')')
```

---

### Operator Precedence Parser

**Definition:** A **bottom-up** parser for **operator grammars** (no two adjacent non-terminals, no ε productions). Uses **precedence relations** between operators.

**Three Precedence Relations:**
```
a <· b  →  a has LOWER precedence (a yields to b)
a =· b  →  a has SAME precedence
a ·> b  →  a has HIGHER precedence (a takes precedence over b)
```

**Operator Precedence Table (for +, *, id, $):**

|  | + | * | id | $ |
|--|---|---|----|---|
| **+** | ·> | <· | <· | ·> |
| **\*** | ·> | ·> | <· | ·> |
| **id** | ·> | ·> | | ·> |
| **$** | <· | <· | <· | accept |

**Parsing Algorithm:**
```
1. Push $ onto stack
2. While not ($ on stack and $ in input):
   a. Find rightmost <· on stack (left boundary of handle)
   b. Find matching ·> in input (right boundary)
   c. Reduce the handle between <· and ·>
   d. Apply corresponding production
```

### Comparison of Parsers:

| Feature | LL(1) | LR(0) | Predictive | Operator Prec. |
|---------|-------|-------|------------|----------------|
| **Direction** | Top-down | Bottom-up | Top-down | Bottom-up |
| **Derivation** | Leftmost | Rightmost (rev) | Leftmost | Rightmost (rev) |
| **Lookahead** | 1 | 0 | 1 | N/A (relations) |
| **Power** | Moderate | Weak | = LL(1) | Limited (operators) |
| **Grammar** | No left recursion | SLR/CLR/LALR | No left recursion | Operator grammar |
| **Table** | Parsing table | ACTION/GOTO | Procedures | Precedence table |

---

# 📋 QUICK REVISION CHEAT SHEET

| Topic | Key Points |
|-------|------------|
| **Synthesized Attr** | Bottom-up; children → parent; E.val = E1.val + T.val |
| **Inherited Attr** | Top-down; parent → children; L.inh = T.type |
| **Machine-Indep Opt** | CSE, Dead code, Constant folding/propagation, Loop motion, Strength reduction |
| **Machine-Dep Opt** | Register allocation, Instruction scheduling, Peephole |
| **Peephole** | Small window; redundant load/store, jump chaining, algebraic simplify |
| **Basic Block** | No jump in/out of middle; leaders: first stmt, jump target, after-jump |
| **Flow Graph** | Blocks as nodes; edges = control flow |
| **Two-Pass Assembler** | P1: build SYMTAB/LITTAB; P2: generate object code |
| **Absolute Loader** | Fixed address; simple but inflexible; no relocation/linking |
| **Forward Ref** | Symbol used before defined; Fix: 2-pass or backpatching |
| **Direct Linking Loader** | Relocate + Link; ESTAB; handles EXTRN/ENTRY |
| **Asm Stmt Types** | Imperative (MOV), Declarative (DS/DC), Directive (START/END/EQU) |
| **ICG Forms** | TAC, Syntax Tree, DAG, Postfix |
| **Quadruples** | 4 fields (op,arg1,arg2,result); easy to rearrange |
| **Triples** | 3 fields (op,arg1,arg2); position-dependent |
| **Indirect Triples** | Triples + pointer list; rearrangeable |
| **LL(1)** | Top-down, FIRST/FOLLOW, parse table, no left recursion |
| **LR(0)** | Bottom-up, items with dots, closure, GOTO, ACTION table |
| **Operator Prec** | <· =· ·> relations between operators; reduce handles |

---

> [!IMPORTANT]
> ### Last-Minute Tips for SPCC PT-II:
> 1. **Code optimization types** — memorize 5+ machine-independent techniques with examples.
> 2. **Quadruples vs Triples vs Indirect Triples** — must show comparison table.
> 3. **Two-Pass Assembler** — draw the diagram, list databases for each pass.
> 4. **LL(1) table construction** — practice FIRST/FOLLOW computation.
> 5. **Basic blocks + flow graph** — identify leaders, draw graph with arrows.
> 6. **Draw diagrams** for loader, assembler, and optimization examples.

---

*Prepared for: MU Sem 6 SPCC PT-II | Computer Engineering | REV-2019*
*Last Updated: April 9, 2026*
