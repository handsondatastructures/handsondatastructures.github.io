---
title: Activities
nav_order: 5
---

# Activities

Each activity is designed to be quick to set up and easy to run in small groups.

## Day 1 Activity: What Is a Collection? (with playing cards)

### Learning goals

- Articulate what a collection/list promises
- Distinguish operations from representations
- Recognize invariants without formal language yet
- See that the same promises can be satisfied in different ways

### Setup (2 minutes)

- Give each group around 10 to 15 playing cards
- "Pretend these cards are data. You're not playing a game — you're designing ways to work with a collection of items."

### Phase 1: Manipulation (5 minutes)

Prompt: "What are all the things you can do with this collection?"

Rules:

- You can physically manipulate the cards
- No code
- No correctness policing yet

Students will naturally do things like:

- Reorder cards
- Add or remove a card
- Look at the top card
- Pick the third card
- Shuffle
- Split into piles
- Insert a card somewhere
- Count cards

Do not correct them yet.

### Phase 2: From actions to operations (5 minutes)

Ask each group to write down five to eight actions they think any reasonable collection should support. Then, as a class, harvest and normalize language:

| Student says | Normalize to |
| --- | --- |
| "Look at a card" | access / get |
| "Put a card in" | add |
| "Take one out" | remove |
| "See how many" | size |

Emphasize: "Notice we're describing what we can do, not how we do it."

### Phase 3: Promises (8 minutes)

Prompt: "If I say 'this is a collection of cards,' what am I promising you?"

Statements like:

- Cards do not disappear unless you remove them
- If I add a card, it is in there
- There is an order (or: maybe there is not)
- If I ask for the third card, that means something
- The collection does not randomly change

Message: "These are promises the data structure makes to its user."

Invariant proto-definition: "These promises are things that should always be true."

### Phase 4: Representation (5 minutes)

Ask: "Did every group physically arrange the cards the same way?"

Likely responses:

- Some stacked them
- Some spread them in a row
- Some made piles

Say: "Even though you represented the cards differently, you mostly agreed on what the collection does."

Follow-up: "Would all representations make every operation equally easy?"

Echo: "Different representations make different promises easier or harder to keep."

### Phase 5: Explicit tie-back (2 to 3 minutes)

What we just discovered:

- A data structure is a collection of data plus a set of operations plus promises about behavior
- The same promises can be implemented in multiple ways
- Implementation details matter — but after the promises are clear

### Ending: Bridge to A0

"In A0, you'll write down the promises for a List before you implement anything."

## Day 2 Activity: Iteration, Sharing, and Copy Depth (Magnets)

### Context in the course

- Day 1: What is a data structure? Promises, invariants, ADTs
- Day 2: Iteration and sharing vs copying (no new data structures)
- Day 3: Arrays as one concrete representation of a list

This activity deepens students' understanding of iteration, aliasing, and copy depth using a physical model, without introducing new syntax or formal data structures.

### Learning objectives

- Explain iteration as systematically visiting elements
- Distinguish between sharing structure and copying structure
- Predict when changes to one object will affect another
- Articulate why a deep copy must create new underlying structure

### Materials

- Number magnets (or similar manipulatives) representing values
- Whiteboard or large paper for drawing diagrams
- Markers

The key requirement is a manipulable representation of shared and copied structure.

### Activity overview

The instructor introduces a fictional student, Sally, who is counting numbers using physical objects. Students reason about how Sally's data is organized, how it is accessed, and what happens when it is shared or copied.

### Part 1: Sally and the magnets

Setup:

- On the board, write something like: `SallyCountOnes -> 2`
- Physically place two "1" magnets near a labeled area for `Ones`

Gradually expand the representation:

```
Sally
├── Ones -> ● ●
├── Twos -> ●
├── Threes -> (empty)
```

Emphasize:

- Sally is not the numbers
- Sally has references to collections of magnets

No formal definition of "reference" is required.

### Part 2: Iteration (without naming iterators)

Ask students:

> If Sally wants to count everything, what does she have to do?

Students will naturally describe:

- Looking at each pile
- Counting magnets pile by pile

Reframe on the board:

```
for each pile Sally knows about:
    count magnets
```

Key takeaway:

- Iteration means systematically visiting the elements you have access to
- No special machinery is required for the idea itself

### Part 3: Introducing Bobbie (sharing structure)

Introduce a second fictional student, Bobbie.

Scenario A: Shared structure

```
Bobbie
├── Ones   ─┐
├── Twos   ─┼──> same piles as Sally
└── Threes ─┘
```

Explain:

- Bobbie does not create new piles
- Bobbie points to the same piles Sally uses

Physically remove or add a magnet and ask:

- Whose counts changed?

Highlight:

- Both Sally's and Bobbie's counts change
- This is sharing, not copying

### Part 4: Copying structure (deep copy)

Redraw Bobbie with new piles. Ensure the piles are physically distinct.

Modify Bobbie's piles and ask again:

- Whose counts changed?

Key takeaway:

- A deep copy creates new structure
- Changes to one do not affect the other

Explicitly state:

> A deep copy is only a copy if changing one does not change the other.

### Part 5: Common misconception (explicitly addressed)

Call out the misconception directly:

> Copying references is not copying the data.

Write on the board:

```
Copying references ≠ copying structure
```

Reinforce:

> If no new structure exists, no copy exists.

### Part 6: Student exploration

Have students work in small groups with rules such as:

- Bobbie shares all piles with Sally
- Bobbie copies all piles
- Bobbie shares some piles but not others

Ask them to:

- Predict which counts will change
- Test their predictions using the magnets

This phase allows confusion to surface safely.

### Closing and connection forward

End with a synthesis:

> Every confusing bug we will see this semester comes from:
> - sharing when you meant to copy
> - copying when you meant to share
> - not realizing which one you did

Preview future relevance:

> Next, we will see how these ideas matter when lists store many elements and when representations become more complex.

### Key takeaway

If two things change together, they were never separate.

## Day 3 Activity: Name Placards as Array-Backed Lists

### Context in the course

- Day 1: What is a data structure? Promises, invariants, ADTs
- Day 2: Iteration and sharing vs copying
- Day 3: Arrays as one concrete representation of a list

This activity revisits a familiar exercise, but now frames it as a case study in representation rather than an introduction.

### Learning objectives

- Explain how a fixed-size array can represent a list
- Describe the invariants an array-backed list must maintain
- Identify why adding or removing elements is difficult in arrays
- Connect physical constraints to design trade-offs, not mistakes

### Materials

- Name tents (one per student, plus extras)
- Scissors (approximately one per student)
- Rulers (approximately one per student)
- Pencils (approximately one per student)
- Colorful pens and other materials for decorating name tents (shared)

### Directions

When students arrive, directions are written on the board and they are encouraged to begin immediately.

Student instructions:

1. Decide what name you would like to be called in this class (first name, nickname, etc.).
2. Count the number of letters in your name.
3. Allocate exactly one box per letter, each 1 inch wide.
4. Draw all boxes before writing any letters.
5. Cut off any extra paper.
6. Write one letter per box, then decorate as you see fit.

Important constraint:
Once the paper is cut, you may not tape or add more paper.

### Class discussion and reflection

After students finish their name tents and introductions, lead a discussion connecting the activity to array-backed lists.

Framing:

> Last class, we decided what promises a list makes.  
> Today, we are seeing what happens when we try to keep those promises using a fixed physical representation.

Their name tent represents an array-backed list.

### Scenario 1: Duplicate names

> "Oh no — we have two people named Emily. I should have asked you to include your last initial.  
> Can you add it now?"

Discussion points:

- Why is this difficult or impossible?
- What constraint prevented the change?

Introduce the idea of fixed capacity.

### Scenario 2: Missing a letter (e.g., `SOPIA`)

Ask:

- What would it take to fix this?
- Which letters would need to move?

Key takeaway:
Inserting elements in an array requires shifting existing elements.

### Scenario 3: Extra letter (e.g., `SOPHHIA`)

Ask:

- What went wrong?
- When did the mistake happen?

Reinforce:

- The number of usable positions was fixed in advance.

Introduce the invariant:
`size` must be less than `capacity`.

### Scenario 4: Iteration

Ask:

- How would someone read your name out loud?

Connect:

- Left-to-right, one box at a time
- This is iteration, which arrays support very naturally

### Closing and connection forward

Conclude by tying back to earlier work:

> This representation keeps many of the promises we wrote in A0 BUT it struggles when the list needs to change size.

Preview upcoming material:

> Next, we will see how programmers work around this limitation — either by resizing arrays or by using a different representation entirely.

### Key takeaway

Arrays are a simple and fast way to represent lists — until the list needs to change.

## Arrays and dynamic arrays

- **Human array:** Participants stand in numbered positions and exchange cards to model indexing and updates.
- **Resize moment:** Add new participants to show reallocation and copying costs.

## Stacks and queues

- **Stack of plates:** Use cups or cards to model push/pop and LIFO behavior.
- **Queue line:** Participants enqueue/dequeue to model FIFO and head/tail pointers.

## Linked lists

- **Yarn links:** Participants hold a card and connect with yarn to show next pointers.
- **Insertion challenge:** Add a new node and rewire links to highlight constant-time insertion.

## Trees and heaps

- **Human tree:** Participants arrange themselves into a binary tree and perform traversals.
- **Heap swaps:** Use numbered cards to model heapify and priority ordering.

## Graphs and hashing

- **Graph walk:** Tape nodes on the floor and navigate edges to model BFS/DFS.
- **Hash buckets:** Place cards into bins and simulate collisions with chains.

{: .note }
Swap in your exact activity names and facilitator notes.
